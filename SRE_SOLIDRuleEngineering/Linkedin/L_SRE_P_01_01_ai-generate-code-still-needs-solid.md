AI 已經可以在幾分鐘內產生完整功能、Test 與 Refactoring。

如果設計不好，可以叫 AI 重寫；如果程式壞了，也可以叫 AI 修正。

那麼，我們還需要 SOLID 嗎？

關鍵在於：

```text
Code Generation Cost 下降
≠
Requirement Change 與 Verification Cost 消失
```

AI 可以快速重新產生 Code，卻不能重新產生從未被保存的 Business Rule、Constraint 與 Design Rationale。

SOLID 原本處理的也不是打字成本，而是需求改變時，修改是否會不必要地擴散。

我在這篇 Article 中討論：當 Code 變得便宜，SOLID 是否仍然有價值，以及它在 AI Generate Code 時代應該位於哪裡。

Article：〔發布後補上連結〕

如果 AI 可以隨時重寫程式，你認為「可維護的設計」會變得更重要，還是逐漸失去價值？

