---
layout: default
title: "React hook callback 的閉包陷阱：靜默失敗無 error"
parent: fishtvlvoe
grand_parent: 貢獻者
tags: [React, 診斷不足]
date: 2026-04-01
still_relevant: true
permalink: /contributors/fishtvlvoe/028-react-hook-closure/
---

# React hook callback 的閉包陷阱：靜默失敗無 error

## 問題

在 React hook 回傳物件的 callback 裡（例如 `useConversation` 的 `onConnect`、`useWebSocket` 的 `onOpen`），呼叫了 hook 本身回傳的方法（例如 `conversation.sendUserMessage()`）。

結果：功能完全不動，但 console 沒有任何 error。WebSocket frames 也看不到對應的 message。一切看起來沒問題，但就是不運作。

## 原因

這是 JavaScript 閉包的經典問題。

Hook 的 callback（`onConnect`、`onOpen`）在 hook **初始化階段**被建立。此時 hook 回傳的方法（`conversation.sendUserMessage` 等）還沒有完全初始化，是 `undefined` 或舊版本。

callback 閉包「抓住」了初始化時的舊值，即使後來 hook 狀態更新了，callback 裡的引用還是指向舊值。呼叫 `undefined()` 在某些情況下靜默失敗，沒有拋出 error。

```tsx
// ❌ 這樣會閉包到舊的 conversation.sendUserMessage
const { conversation } = useConversation({
  onConnect: () => {
    conversation.sendUserMessage("hello") // 此時 conversation 可能是初始值
  }
})
```

## 解決方案

**正確做法：callback 只更新 state，後續動作用 `useEffect` 監聽**

```tsx
const [isConnected, setIsConnected] = useState(false)

const { conversation } = useConversation({
  onConnect: () => {
    setIsConnected(true) // callback 只更新 state
  }
})

useEffect(() => {
  if (isConnected) {
    conversation.sendUserMessage("hello") // useEffect 拿到最新的 conversation
  }
}, [isConnected, conversation])
```

`useEffect` 的依賴陣列確保每次 `conversation` 更新時都能拿到最新引用。

**症狀總結（遇到這三個同時出現，優先懷疑閉包問題）：**
- 功能不動
- Console 無 error
- WebSocket frames / network 看不到對應 request

## 可複用的 CLAUDE.md 規則

把這段貼進你的 CLAUDE.md：

```markdown
- React hook 回傳物件的 callback（onConnect、onOpen 等）內，禁止呼叫 hook 本身回傳的方法。
  閉包抓到初始化未完成的舊值 → 靜默失敗無 error。
  改法：callback 只更新 state，後續動作用 useEffect 監聽該 state 觸發。
```
