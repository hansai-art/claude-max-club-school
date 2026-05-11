---
layout: default
title: "React Hook 回調裡不能呼叫 Hook 本身回傳的方法"
parent: fishtvlvoe
grand_parent: 貢獻者
date: 2026-05-11
still_relevant: true
permalink: /contributors/fishtvlvoe/005-react-hook-callback-closure/
---

# React Hook 回調裡不能呼叫 Hook 本身回傳的方法

## 問題

Claude 在 React hook 的回調（`onConnect`、`onOpen`、`onMessage` 等）裡直接呼叫同一個 hook 回傳的方法（如 `conversation.sendUserMessage()`）。程式碼看起來完全合理，但功能靜默失敗——沒有 error、沒有 warning，什麼都沒發生。

真實案例：`useConversation` hook 回傳 `conversation` 物件，Fish 在 `onConnect` 回調裡呼叫 `conversation.sendUserMessage('hello')`。WebSocket 連線成功，但 `hello` 訊息永遠沒有被發送。Console 完全乾淨，WebSocket frames 也看不到對應的 message。

## 原因

閉包（closure）抓到的是 hook **初始化時的舊值**。在 `onConnect` 被觸發的時間點，`conversation` 還是初始化未完成的空物件（或 null）。JavaScript 沒有報錯，因為呼叫 null 的方法在某些框架包裝下會被吞掉，或者物件存在但 method 是 no-op。

這是 React hooks 的經典陷阱：callback 在創建時捕獲的 closure，不會因為之後的 state 更新而自動更新。

## 解決方案

callback 內**只更新 state**，後續動作改用 `useEffect` 監聽該 state 的變化來觸發。

```tsx
// 錯誤：onConnect 裡的 conversation 是舊 closure
const { conversation } = useConversation({
  onConnect: () => {
    conversation.sendUserMessage('hello') // 靜默失敗！
  }
})

// 正確：callback 只更新 state
const [connected, setConnected] = useState(false)
const { conversation } = useConversation({
  onConnect: () => setConnected(true)
})

useEffect(() => {
  if (connected) {
    conversation.sendUserMessage('hello') // 此時 conversation 是最新值
  }
}, [connected])
```

## 症狀辨識

- 功能完全不動
- Console 無任何 error
- WebSocket frames（或 Network）看不到預期的 message/request
- 程式碼邏輯看起來完全正確

這三個特徵同時出現 → 優先懷疑 closure 問題。

## 可複用的 CLAUDE.md 規則

```markdown
### React Hook 閉包陷阱
- Hook 回傳物件的 callback（onConnect、onOpen、onMessage 等）內，禁止呼叫同一 hook 回傳的方法
- 閉包抓到初始化未完成的舊值 → 靜默失敗無錯誤
- 正確做法：callback 只更新 state，後續動作用 useEffect 監聽該 state 觸發
- 症狀：功能不動、Console 無 error、Network/frames 看不到對應請求
```
