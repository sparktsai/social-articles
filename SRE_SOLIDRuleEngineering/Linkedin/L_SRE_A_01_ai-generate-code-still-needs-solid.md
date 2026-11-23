# AI Generate Code 這麼容易，我們還需要 SOLID 嗎？

AI Coding Agent 已經能在幾分鐘內建立專案骨架、產生完整功能、補上 Test，甚至重寫一個設計不良的 Module。

如果程式碼壞了，可以要求 AI 修正；如果架構不理想，也可以要求 AI Refactor；如果整個實作不滿意，甚至可以重新生成。

在這種情況下，我們還需要 SOLID 嗎？

這個問題看似合理，卻把「產生程式碼」與「維護軟體」當成同一件事。

## Code 變便宜，不代表 Change Risk 變便宜

AI 確實降低了 Code Production Cost。

過去需要數天完成的功能，現在可能在數小時內產生；過去因實作成本過高而不敢進行的 Refactoring，現在也能快速得到候選方案。

但軟體修改的成本不只有打字與產生 Code。

每次需求改變，團隊仍然要回答：

- 哪些既有行為不能改變？
- 哪些資料必須保持一致？
- 哪些外部契約不能破壞？
- 哪些 Module 會受到影響？
- 哪些 Test 代表真正需求？
- 哪些風險可以接受？
- 誰能確認修改後的結果仍符合業務目的？

AI 可以快速重寫程式，卻不能只靠重寫本身回答這些問題。

```text
Code Generation Cost 下降
≠
Requirement Change 與 Verification Cost 消失
```

## SOLID 原本處理的就不是打字成本

SOLID 經常被簡化成五條程式結構規則：

- Class 不要太大；
- Function 不要太長；
- 多使用 Interface；
- 避免 Concrete Dependency；
- 使用 Design Pattern 隔離變動。

但 SOLID 真正關心的是：當需求改變時，修改影響是否會不必要地擴散。

例如：

- 新增一種付款方式，是否必須修改穩定的訂單流程？
- Email 格式改變，是否會影響付款交易？
- 更換資料庫，是否會迫使 Business Policy 跟著改寫？
- 新的 Subtype 是否破壞原本 Caller 依賴的契約？
- 不同 Client 的需求是否被綁在同一個大型 Interface？

這些問題不會因為 AI 能快速產生 Code 而消失。

## AI 甚至可能放大修改問題

AI 可以讓每次局部修改變得很便宜。

這也可能讓團隊更容易接受：

- 再增加一個 Branch；
- 再加入一個 Dependency；
- 再補一個 Mode Flag；
- 再建立一層抽象；
- 再產生幾個 Adapter；
- 再複製一組相似流程。

每一次修改都可以通過 Test，也可能在當下看起來合理。

但當修改數量增加，真正的問題會變成：這些修改是否仍然沿著正確的需求邊界發生？

如果答案不清楚，AI 只是在更快地累積設計債務。

## 重新生成不等於重新理解

有人可能認為，既然 AI 能重新產生程式，Architecture 是否可維護已經不重要。

但重新生成仍然需要輸入：

- 完整 Requirement；
- Business Rule；
- Acceptance Criteria；
- Data Constraint；
- Integration Contract；
- Security 與 Reliability Requirement；
- 過去已接受的 Trade-off。

如果這些內容不完整，重新生成只會得到另一個基於不完整 Context 的實作。

AI 能重新產生 Code，不能重新產生從未被保存的業務知識。

## Test 通過也不代表容易維護

Test 可以證明某些輸入仍得到預期結果，卻不一定能回答：

- 為什麼兩個 Function 應該分開？
- 為什麼某些步驟必須位於同一個 Transaction？
- 哪個 Stakeholder 擁有某項 Policy？
- 為什麼當初刻意沒有建立共同 Abstraction？
- 下一項需求改變時，哪些部分應該一起修改？

一個系統可以通過所有 Test，同時變得越來越難修改。

SOLID 處理的正是這種不會立即表現成 Failure，卻會提高未來 Change Cost 的設計問題。

## AI 時代，SOLID 的理由正在改變

過去，我們常說 SOLID 是為了讓下一位 Human Developer 更容易理解與修改程式。

這個理由仍然成立，但已經不完整。

今天的下一位維護者可能是另一個 AI Agent。它需要知道：

- 這個邊界為什麼存在？
- 這個 Interface 隔離什麼變動？
- 哪些相似 Code 其實代表不同 Policy？
- 哪些操作必須共同維持一致性？
- 哪些設計只是暫時折衷？

所以 SOLID 的價值不再只是讓 Code 看起來清楚，而是讓修改仍能沿著正確的需求與責任邊界發生。

## 我們仍然需要 SOLID，但不能只看外觀

AI 時代最危險的做法，是要求模型「遵守 SOLID」，然後用 Class 數量、Function 長度與 Interface 數量判斷結果。

這可能得到形式上漂亮、實際上沒有需求根據的架構。

真正需要保留的是 SOLID 背後的問題：

> 當需求改變時，如何讓修改維持在可理解、可驗證與可控制的範圍？

AI 讓 Code Generation 變得容易，沒有讓 Requirement Change、Impact Analysis 與 Design Judgment 變得容易。

所以答案不是放棄 SOLID，而是重新確認 SOLID 的位置：

```text
不是限制 AI 產生多少 Code
而是限制需求變動如何擴散到 Code
```

下一個問題是：如果 AI 能產生程式，它是否也能自己維護？

