AI 能讀取 Repository、修改既有邏輯、執行 Test，並持續修正到全部通過。

這代表 AI 已經能自己維護程式碼嗎？

「修改 Code」可能只是：

```text
新要求 → 產生 Diff → Test 通過
```

「維護 Software」還需要理解既有需求、辨識 Change Driver、保留契約，並知道某個設計邊界為什麼存在。

如果這些理由沒有被保存，AI 只能從目前 Code 反推語意。前一個 Agent 的推論，又可能成為下一個 Agent 認定的事實。

我在這篇 Article 中討論 AI Maintain Code、推論偏差如何逐步固化，以及 Test 通過為什麼仍可能伴隨語意侵蝕。

Article：〔發布後補上連結〕

你認為 AI 要能真正維護軟體，除了 Code 與 Test，還必須長期取得哪些資訊？

