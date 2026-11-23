# AI 看見 Branch，卻不一定看見變動原因

假設 AI 在一個 Method 中看見兩個 Branch：

```text
if customer is enterprise
    apply enterprise pricing
else
    apply standard pricing
```

它可能作出以下判斷：

1. 系統存在兩種定價策略。
2. 未來可能增加更多客戶類型。
3. 這個 Method 違反 OCP。
4. 應該建立 `PricingStrategy` Interface。

這是一個合理的設計方向，但它不是從 Code 必然得到的結論。

Branch 是事實；「存在會持續擴充的獨立變動軸」是推論。

這個差異，是 AI 使用 SOLID 時最容易被忽略的地方。

## 兩種不同的推論

AI 分析軟體時，至少存在兩種推論路徑：

1. 程式推論；
2. 需求語意推論。

兩者都可能使用 Code，但回答的問題不同。

## 程式推論：系統現在如何實作？

程式推論主要觀察：

- Class、Method 與 Function；
- Branch 與控制流程；
- Dependency 與 Call Graph；
- Parameter、Return Value 與 Exception；
- Interface、Inheritance 與實作關係；
- Duplicate Code；
- Test 與 Caller。

它適合回答可定位的結構問題：

- 哪些 Caller 使用這個 Method？
- 哪些 Class 實作這個 Interface？
- 哪個 Branch 呼叫了外部服務？
- 修改 Signature 會直接影響哪些位置？
- 哪些程式片段在語法上相似？
- 哪些 Test 覆蓋目前行為？

這些是重要的工程事實。

但它們仍無法單獨回答：

- 兩個 Branch 是否由不同 Business Policy 驅動？
- 兩段相似程式是否會因相同需求改變？
- 某個 Concrete Dependency 是否真的需要替換？
- 某組操作是否必須位於同一個 Transaction？
- 哪個 Actor 會要求這段行為改變？
- 某個未來變體是否值得現在建立 Extension Point？

Code 呈現的是設計結果，不一定保存形成設計的全部原因。

## 需求語意推論：系統為什麼改變？

需求語意推論從另一組證據開始：

- Actor 與 Stakeholder Goal；
- Use Case；
- Acceptance Criteria；
- Business Rule 與 Policy；
- Quality Attribute；
- Regulatory Constraint；
- Failure、Compensation 與 Consistency Requirement；
- Ownership 與 Release Cadence；
- Change Scenario 與 Requirement History。

它要回答：

- 誰會要求改變？
- 為什麼改變？
- 哪一項 Policy 會改變？
- 哪些行為必須一起改變？
- 哪些行為應該彼此獨立？
- 改變時哪些契約必須保持？
- 哪些變動已有證據，哪些只是想像？

回到定價案例，如果 Enterprise Pricing 由獨立合約、不同 Ownership 與不同發布節奏驅動，那麼建立獨立策略可能有充分理由。

但如果兩個 Branch 只是同一項法規公式中的兩段條件，而且必須共同變更，將它們拆成可獨立替換的 Strategy 可能反而隱藏真正的一致性。

相同 Code Shape 可以對應不同需求語意。

## AI 為什麼容易過度推論？

LLM 的能力之一，是從可見 Pattern 推測缺少的內容。

這對 Code Generation 很有用。需求沒有明確寫出資料結構、錯誤處理或測試案例時，模型仍能產生合理答案。

但在設計判斷中，同一種能力也可能把結構訊號延伸得太遠：

```text
存在 Branch
→ 存在多個變體
→ 未來還會新增變體
→ 應建立 Strategy
```

```text
存在多個 Dependency
→ 存在多個責任
→ 應拆成多個 Service
```

```text
存在相似程式碼
→ 代表相同概念
→ 應建立共同 Abstraction
```

第一行可能是 Code Fact，後面幾行卻已變成 Semantic Inference。

真正問題不是 AI 使用了推論，而是推論經常以確定結論呈現。

## 語法相似不等於語意相同

假設 `calculateCancellationFee` 與 `calculateReturnFee` 目前使用相同百分比公式。

從 Code 來看，它們是重複程式碼。

但取消費可能由訂房政策決定，退貨費則由商品類別、物流成本與消費法規決定。今天公式相同，不代表它們具有相同 Change Driver。

如果抽取成共同的 `calculateFee`，未來其中一項政策改變時，共用抽象可能需要加入 Flag、Type Check 或例外參數。

原本看似消除重複，最後卻把兩項獨立政策耦合在一起。

## 操作很多不等於責任很多

假設 `completePayment` 執行：

1. 驗證付款狀態；
2. 寫入付款紀錄；
3. 更新訂單；
4. 建立交易事件；
5. 提交 Transaction。

它具有多個操作與 Dependency，但所有步驟可能共同維持一項不可分割的支付結果。

只因操作數量多就拆分，可能破壞 Transaction 與 Invariant。

反過來，一個只有數行的 Method 也可能依據 Mode Flag 實作兩個由不同 Actor 擁有的 Policy。

程式大小只能指出值得檢查的位置，不能決定責任數量。

## 語意分解與程式分解不是一對一

需求語意可以被分解成：

- Business Capability；
- Use Case；
- Observable Outcome；
- Policy；
- Invariant；
- Change Driver。

程式可以被分解成：

- Package；
- Module；
- Class；
- Interface；
- Method；
- Function。

一個 Use Case 可能需要多個 Object 協作，一個 Class 也可能參與數個 Use Case。

兩者不必一對一，但必須能說明彼此的對應：

```text
Requirement Semantic Unit
    ↕ traceability
Implementation Unit
```

如果只有語意分解，沒有程式位置，就無法實作與驗證。

如果只有程式分解，沒有需求來源，就無法證明某個邊界代表真正的責任或變動軸。

## 需要區分四種資訊

AI 進行設計分析時，至少應區分：

### Code Fact

可以由 Repository 直接定位，例如某個 Method 呼叫三個 Dependency。

### Requirement Fact

由正式需求、Acceptance Criteria、Issue 或已確認決策支持，例如 Email 失敗不得 Rollback Payment。

### Semantic Inference

根據 Code、Caller 與 Test 推測，例如某個 Branch 可能代表不同 Business Policy。

### Missing Context

缺少的資訊可能改變結論，例如外部 Caller 不可見，或無法確認兩個 Policy 是否由不同團隊擁有。

這四者不能混在一起。

## 程式推論不是錯，而是不足以單獨決定設計

沒有程式推論，我們無法知道實際 Dependency、Caller 與修改範圍。

沒有需求語意推論，我們則無法知道這些結構是否反映真正的變動來源。

合理方向不是用 Requirement 取代 Code，而是建立雙向關係：

```text
Requirement / Policy / Change Driver
    ↕
Package / Class / Interface / Method
```

最重要的問題也因此改變：

> 不是「這段 Code 看起來可能怎麼變」，而是「哪一項需求證明這種變動值得被設計？」

下一篇將討論：當設計找不到這個需求來源時，如何形成無根的變動性，以及為什麼它能同時造成過度設計與功能過大。

