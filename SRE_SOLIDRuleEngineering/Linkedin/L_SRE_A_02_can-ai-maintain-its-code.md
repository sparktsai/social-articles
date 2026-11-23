# AI 會產生程式，但它真的能自己維護嗎？

AI Coding Agent 不只會產生新程式。

它也能讀取 Repository、尋找相關檔案、修改既有邏輯、執行 Test，並根據失敗結果繼續修正。

從表面上看，AI 已經具備維護程式碼的能力。

但「修改 Code」和「維護 Software」並不是同一件事。

## 修改 Code 的流程很清楚

一次典型的 AI 修改任務可能是：

```text
取得新要求
→ 搜尋相關 Code
→ 產生 Diff
→ 執行 Test
→ 修正 Failure
→ 完成任務
```

這個流程可以有效完成 Bug Fix、功能新增與局部 Refactoring。

但軟體維護還需要另一組能力：

```text
理解既有需求
→ 理解設計理由
→ 辨識新的 Change Driver
→ 評估修改影響
→ 保留既有契約
→ 修改實作
→ 驗證需求仍然成立
```

兩個流程的差異，不在 AI 是否能寫出正確 Syntax，而在它是否知道什麼不能被修改，以及為什麼。

## AI 維護通常從結果反推原因

第一次開發系統時，團隊可能同時掌握：

- 原始 Requirement；
- Use Case 與 Acceptance Criteria；
- Architecture Decision；
- 評估過但放棄的替代方案；
- Transaction 與 Reliability Constraint；
- 不同 Stakeholder 的 Change Driver。

幾個月後，負責維護的 AI Agent 通常只能看到：

- 現有 Code；
- Current Diff；
- 局部 Test；
- 新的需求 Prompt；
- 部分文件。

這時 AI 不是從完整需求推導設計，而是從目前設計反推可能的需求語意。

```text
原始需求與設計理由
    ↓
目前程式結構
    ↓
AI 從 Code 反推語意
    ↓
AI 依推測修改設計
```

如果設計理由沒有被保存，AI 只能使用 Code Shape 作為替代證據。

## Code 能告訴 AI 什麼？

AI 可以從 Code 確認：

- 哪些 Function 互相呼叫；
- 哪些 Class 實作 Interface；
- 哪些 Branch 執行不同操作；
- 哪些 Test 覆蓋目前行為；
- 修改 Signature 會影響哪些 Caller；
- 哪些程式片段看起來相似。

但 Code 不一定能告訴 AI：

- 為什麼兩個相似 Function 必須分開；
- 為什麼某個操作必須位於 Transaction 外；
- 哪個 Actor 擁有某項 Policy；
- 為什麼沒有建立共同 Interface；
- 哪個錯誤可以被忽略，哪個錯誤必須 Rollback；
- 哪些未來需求不應影響目前核心。

程式保存實作結果，不一定保存完整設計原因。

## 前一個 Agent 的推論，會成為下一個 Agent 的事實

AI 自我維護最大的風險，不一定是某一次修改立即產生 Bug。

更長期的問題是：一次錯誤推論會改變 Repository，而新的結構會成為下一次推論的基礎。

```text
缺少原始語意
→ Agent A 從 Code 推測責任
→ 進行一次不當拆分或合併
→ 新 Test 與 Dependency 建立在新結構上
→ Agent B 將它視為既有設計意圖
→ 偏差逐步固化
```

例如，Agent A 發現兩個 Function 使用相似公式，因此抽取共同實作。

但兩個 Function 其實分別代表取消政策與退貨政策，未來由不同法規和團隊維護。

Agent B 看到兩者使用同一個 Helper，便更有理由相信它們屬於相同概念。當其中一項政策改變時，它在共同 Function 中加入 Flag。

下一次修改又加入另一個例外。

最後形成一個表面上高度共用、實際上混合不同 Change Driver 的大型單元。

## 相反方向也會發生

AI 也可能將一個需要共同完成的 Transaction 拆成多個 Service。

下一個 Agent 看到數個 Service 後，為它們建立 Interface 與 Factory；再下一個 Agent 為跨 Service 的一致性建立 Coordinator、Event 與補償流程。

原本簡單而凝聚的行為，逐步變成難以理解的過度設計。

每一次修改在局部看起來都合理，整體設計卻持續偏離原始需求。

## Test 通過為什麼還不夠？

Test 可以驗證選定輸入與輸出，也可以保護重要行為。

但 Test 不一定記錄：

- Responsibility 為何分離；
- Boundary 為何存在；
- Policy 的 Ownership；
- 哪些設計是刻意避免的；
- 哪些修改方向會提高未來 Change Cost。

所以 AI 可以在所有 Test 通過時，破壞 Responsibility Boundary、Substitution Contract 或 Dependency Policy。

系統仍然運作，但下一次需求修改會變得更廣、更難、更危險。

## 語意侵蝕

當 Requirement 與 Design Rationale 沒有被保留，後續 AI 只能不斷從最新 Code 重新解釋設計。

每次重新解釋都可能：

- 遺失一部分原始 Constraint；
- 把 Inference 當成 Fact；
- 把偶然結構當成設計理由；
- 把局部整潔當成整體正確；
- 把 Test 通過當成語意仍然一致。

程式可能持續運作，需求與 Code 的對應卻逐步消失。

這可以稱為「語意侵蝕」。

## AI 要自己維護，需要的不只是更多 Code Context

讓 AI 讀取更多檔案確實有幫助，但完整 Repository 仍然主要呈現「現在如何實作」。

AI 還需要取得：

- Requirement Context；
- Business Policy；
- Architecture Decision；
- Change Driver；
- Boundary Rationale；
- Accepted Trade-off；
- Known Uncertainty。

只有這些資訊可被下一次執行取得，AI 才能區分：

- 現有結構是刻意設計，還是歷史偶然；
- 相似 Code 應該共用，還是必須分離；
- 大型流程是 God Function，還是完整的 Consistency Boundary；
- 新需求應建立抽象，還是只需要局部實作。

## AI 可以維護，但維護能力來自可取得的語意

AI 能不能自己維護程式，不只取決於 Model Capability。

也取決於 Repository 與 Engineering Workflow 是否保存足夠的需求和設計資訊。

```text
AI Maintenance
≠
反覆修改直到 Test 通過
```

更完整的定義應該是：

```text
AI Maintenance
= 理解新的需求變動
+ 保存既有契約
+ 控制修改影響
+ 維持需求與設計的對應
```

要理解這件事為什麼與 SOLID 有關，我們必須回到 SOLID 最初想解決的問題。

