---
layout: default
title: "React hook callback 的閉包陷阱：靜默失敗無錯誤"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [前端開發, 診斷不足]
date: 2026-05-04
still_relevant: true
permalink: /contributors/fishtvlvoe/010-react-hook-stale-closure/
---

# React hook callback 的閉包陷阱：靜默失敗無錯誤

## 問題

在 hook 回傳物件的 callback（如 `useConversation` 的 `onConnect`、`useWebSocket` 的 `onOpen`）內，呼叫 hook 回傳的方法（如 `conversation.sendUserMessage()`）。

功能完全不動，Console 沒有任何 error，WebSocket frames 看不到對應 message，彷彿程式碼根本沒執行到。

## 原因

這是 JavaScript 閉包（stale closure）問題。`onConnect` callback 在 hook 初始化時建立，閉包裡抓到的 `conversation` 是初始化**未完成前**的舊值（通常是 `undefined` 或空物件）。

呼叫 `conversation.sendUserMessage()` 時，`conversation` 指向的是舊的未完成版本，方法要不是不存在就是失效，但因為 JavaScript 的錯誤處理，這個失敗被靜默吞掉，不拋出 error。

症狀特徵：
- 功能不動
- Console 無 error
- WebSocket frames 看不到對應 message

## 解決方案

**錯誤做法**：
```javascript
const { conversation } = useConversation({
  onConnect: () => {
    conversation.sendUserMessage('hello') // 閉包抓到舊值
  }
})
```

**正確做法**：callback 只更新 state，後續動作用 `useEffect` 監聽 state 觸發：
```javascript
const [isConnected, setIsConnected] = useState(false)
const { conversation } = useConversation({
  onConnect: () => setIsConnected(true) // 只更新 state
})

useEffect(() => {
  if (isConnected) {
    conversation.sendUserMessage('hello') // useEffect 中 conversation 是最新值
  }
}, [isConnected, conversation])
```

## 可複用的 CLAUDE.md 規則

```markdown
## React hook callback 規則
- hook 回傳物件的 callback（onConnect/onOpen 等）內，禁止呼叫同一 hook 回傳的方法
- 原因：閉包抓到初始化未完成的舊值 → 靜默失敗無 error
- 正確做法：callback 只更新 state，後續動作用 useEffect 監聽 state 觸發
- 症狀識別：功能不動 + Console 無 error = 優先懷疑 stale closure
```
