# AI 讓程式碼變便宜之後，SOLID 還重要嗎？

AI Coding Agent 可以在幾分鐘內建立專案骨架、產生數個 Module、補上 Test，甚至完成一次跨檔案 Refactoring。

當程式碼不再主要依靠人類逐行撰寫，我們自然會問：

> 為人類撰寫與維護程式碼而形成的 SOLID，是否已經過時？

這個問題預設 AI 改變了軟體工程的根本問題。

但 AI 改變的主要是 Code Production，而不是 Requirement Change。

## AI 沒有消除需求變動

即使所有程式都由 AI 產生，系統仍然會因為以下原因改變：

- 使用者需要新功能；
- Business Policy 改變；
- 法規與安全要求更新；
- 外部 API 或資料格式改版；
- 效能與可靠性目標提高；
- 產品進入新的市場；
- 不同客戶需要不同變體；
- 原本的需求理解被證明不完整。

SOLID 原本處理的問題仍然存在：當需求改變時，修改是否會擴散？契約是否會被破壞？高階政策是否被技術細節牽制？

AI 不只沒有消除這些問題，還可能因為提高程式碼產量而放大它們。

## 傳統開發中，理解與實作通常一起發生

在人類主導的開發流程中，理解需求、形成設計與撰寫程式通常互相交錯。

```text
理解需求
→ 建立初步設計
→ 撰寫部分程式
→ 發現理解不足
→ 修正需求與設計
→ 繼續實作
```

撰寫程式本身也是理解問題的過程。

開發者在命名、拆分 Function、處理錯誤、設計 Interface 與撰寫 Test 時，會不斷面對原本需求沒有說清楚的地方。

這個過程很慢，但它讓設計者逐步形成 Domain 與 Architecture 的 Mental Model。

## AI 可以跳過理解形成的可見過程

AI Generate Code 的流程更接近：

```text
輸入一段需求描述
→ AI 推論缺少的細節
→ 產生完整程式結構
→ 產生 Test
→ 人類檢查結果
```

模型可以快速補全：

- 尚未定義的資料結構；
- 未說明的錯誤處理；
- 看似合理的分層；
- 常見 Design Pattern；
- 預期的 Test Case；
- 可能需要的 Interface。

這些補全能力讓 AI 很有生產力，但也帶來新的不對稱：

> Code 形成得比團隊對設計的共同理解更快。

人類看到的是完成後的 Repository、Pull Request 或 Diff，不一定經歷每個設計決定形成的過程。

## Code Throughput 提高，Judgment 沒有自動增加

過去的限制往往是實作速度。現在，AI 可以同時產生更多 Code、Test 與 Refactoring Proposal。

但以下資源沒有同比增加：

- Stakeholder 可以提供的時間；
- Reviewer 的注意力；
- 團隊對 Domain 的共同理解；
- Production Evidence；
- 對風險與 Trade-off 的判斷能力。

因此，瓶頸會從「如何產生程式」移向：

- 要求是否正確？
- AI 補全了哪些沒有被說明的語意？
- Design Boundary 是否有需求依據？
- Test 驗證的是需求，還是 AI 自己產生的假設？
- 誰能接受剩餘風險？

OpenAI 對 Agent-first Engineering 的實務記錄也指出，提高 Code Throughput 後，團隊需要投入更多工作讓 Domain、Architecture、Tool 與 Evidence 對 Agent 可見；對執行中的 Agent 而言，無法取得的知識實際上近似不存在。

參考：[Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)

## AI 很容易產生「SOLID 的外觀」

LLM 熟悉大量軟體設計文章、範例與常見 Pattern。

要求它「使用 SOLID 重構」，通常可以迅速得到：

- 更小的 Class；
- 更多 Interface；
- Repository Pattern；
- Factory；
- Strategy；
- Dependency Injection；
- 清楚的資料夾分層。

這些結構可能正確，也可能只是形式完整。

例如，一個支付系統目前只有一個固定 Provider，短期內沒有替換計畫，也沒有測試隔離問題。AI 仍可能建立：

```text
PaymentProvider
DefaultPaymentProvider
PaymentProviderFactory
PaymentProviderResolver
PaymentProviderStrategy
```

這個結構看起來符合 OCP 與 DIP，但它隔離的是哪一項已知變動？

如果找不到 Requirement、Policy 或 Change Scenario，抽象只是把「未來可能改變」具體化成今天必須維護的複雜度。

## AI 也可能選擇最短修改路徑

AI 並不總是過度抽象。

當任務是「加入一個功能」而不是「改善設計」時，模型可能找到現有最接近的 Function，直接加入一個 Branch、Dependency 或 Side Effect。

```text
新需求
→ 找到相近 Function
→ 加入條件與操作
→ 補上 Test
→ 任務完成
```

每一次修改都可能很小，也能通過 Test。但數次迭代後，同一個 Function 可能同時處理 Policy、Persistence、Notification、Formatting 與多種錯誤語意。

所以 AI 可能同時放大兩個相反問題：

- 被要求改善架構時，產生過度設計；
- 被要求快速加入功能時，形成 God Function 或 God Class。

## 問題不在 AI 是否知道 SOLID

模型通常可以正確解釋五項原則。

真正問題是：它是否知道某個設計單元為什麼會改變？

SOLID 中的許多關鍵詞都依賴需求語意：

- Responsibility
- Reason to change
- Extension
- Substitution
- Client
- Policy
- Detail

這些概念不能只由程式結構完整決定。

如果 AI 只能看到 Code，它會使用 Branch、Dependency、相似度與命名推測語意。這些推測有時正確，但不能自動被視為需求事實。

## SOLID 沒有過時，而是位置必須前移

傳統流程常在 Code Review 時問：

> 這個實作是否符合 SOLID？

AI 時代更需要提前問：

> 這次需求包含哪些 Change Driver？哪些行為必須一起改變？哪些政策應該彼此隔離？

SOLID 不應只是生成完成後的結構檢查，而應位於 Requirement、Design 與 Generation 之間。

```text
需求語意
→ 變動來源
→ 設計邊界
→ AI 產生程式
→ 驗證邊界是否仍與需求相符
```

## AI 時代更需要 SOLID，但不是原本的使用方式

AI 讓程式碼變得便宜，沒有讓修改風險變得便宜。

它可以快速重寫大量 Code，但如果需求語意、契約與設計理由不清楚，重寫只會更快地產生另一個未經證明的結構。

因此，AI 時代的 SOLID 不應被定位為：

> 一組讓 AI 產生更多 Class 與 Interface 的規則。

它應該被定位為：

> 一組幫助 Human 與 AI 對齊需求變動、設計邊界與修改影響的原則。

下一篇將進一步討論：程式推論與需求語意推論究竟有什麼差異，以及為什麼 AI 看見 Branch，卻不一定看見真正的變動原因。

