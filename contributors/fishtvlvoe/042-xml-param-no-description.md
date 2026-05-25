---
layout: default
title: "Agent tool call XML 參數值不能夾雜描述文字"
parent: fishtvlvoe
grand_parent: 貢獻者
permalink: /contributors/fishtvlvoe/042-xml-param-no-description/
tags: [Agent, tool call, XML, 格式, 派工]
date: 2026-05-18
still_relevant: true
---

# Agent tool call XML 參數值不能夾雜描述文字

## 問題

Claude 在撰寫 Agent tool call 的 XML 格式時，把說明文字夾雜在 `<parameter>` 標籤之間：

```xml
<parameter name="subagent_type">general-purpose</parameter>（這個代理負責讀截圖...）
<parameter name="model">haiku
```

XML parser 的行為是：`</parameter>` 之後、下一個 `<parameter>` 之前的所有文字，都會被吞進**前一個**參數的值裡。

結果：
- `subagent_type` 的值變成 `general-purpose（這個代理負責讀截圖...）`（無效值）
- `model` 的值被截斷或格式錯誤
- Tool call 失敗或用了錯誤的參數值，且沒有明顯的錯誤訊息（靜默失敗）

## 原因

Claude 習慣在輸出中夾帶說明，讓用戶理解每個參數的用途。在一般文字輸出中這是好習慣，但放進 XML 標籤之間就變成格式污染。

## 解決方案

Tool call 的說明只能寫在 XML 標籤**之外**的文字輸出裡：

**錯誤寫法：**

```xml
<use_mcp_tool>
<parameter name="subagent_type">general-purpose</parameter>（用來讀截圖）
<parameter name="model">haiku</parameter>
</use_mcp_tool>
```

**正確寫法：**

先在文字中說明，再寫乾淨的 XML：

```
我將派一個 haiku 子代理來讀取截圖並分析內容。

<use_mcp_tool>
<parameter name="subagent_type">general-purpose</parameter>
<parameter name="model">haiku</parameter>
</use_mcp_tool>
```

**規則：** XML 標籤內只放參數值，說明文字放在 tool call 區塊之外。

## 可複用的 CLAUDE.md 規則

```markdown
## Agent tool call XML 格式

- XML parameter 標籤內只能放純參數值，禁止夾帶任何說明文字
- 說明文字只能寫在 tool call 區塊之外的文字輸出裡
- 錯誤：`<parameter name="model">haiku</parameter>（速度快省 token）`
- 正確：先在文字說明，再寫乾淨的 `<parameter name="model">haiku</parameter>`
- XML parser 會把標籤間的意外文字吞進前一個參數值，導致 tool call 靜默失敗
```
