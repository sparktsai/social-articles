# SOLID for AI 不只是把五項原則寫進 Prompt

如果 AI Generate Code 仍然需要 SOLID，最直接的做法似乎是把五項原則加入 Prompt：

> 請遵守 SRP、OCP、LSP、ISP 與 DIP，產生容易維護的程式碼。

AI 通常能理解這段要求，也能產生看起來合理的 Class、Interface 與 Dependency Structure。

但這還不是 SOLID for AI。

因為 SOLID 的關鍵概念——Responsibility、Reason to Change、Extension、Substitution、Client 與 Policy——都需要需求語意才能判斷。

## SOLID for Human 的隱含前提

傳統 SOLID 預設使用者是人類開發者。

人類可以：

- 與 Stakeholder 討論需求；
- 理解業務背景；
- 知道過去的設計決策；
- 辨識可能的 Change Driver；
- 對模糊資訊提出問題；
- 記得團隊接受的 Trade-off；
- 在原則衝突時作出情境判斷。

所以一句「一個 Class 應該只有一個變動原因」可以保持高度濃縮。

Reason 從哪裡來，預設由人類理解。

```text
SOLID for Human
= Design Principles
+ Human Semantic Judgment
```

## AI 缺少同樣的語意來源

AI 只能使用當次執行中可取得的：

- Prompt；
- Code；
- Test；
- Issue；
- 文件；
- Current Diff；
- Repository 內可搜尋資訊。

如果 Design Rationale 存在人類記憶、過去會議、Chat 或沒有載入的文件，對當次 AI 而言，它實際上不存在。

於是模型只能從 Code Shape 推測 Responsibility 與 Change Driver。

這就是 SOLID for AI 必須處理的核心差異。

## 第一個轉變：從 Code-first 到 Requirement-first

一般 AI SOLID Review 可能採用：

```text
讀取 Code
→ 找出 Branch、Dependency 與大型 Method
→ 推測 Responsibility 與 Variation
→ 建議拆分或抽象
```

SOLID for AI 應該改為：

```text
取得 Requirement、Actor、Policy 與 Constraint
→ 辨識 Change Driver
→ 映射到程式單元
→ 檢查 Responsibility 與 Variation Boundary
→ 評估修改影響
```

Code 仍然是必要證據，但不能成為需求語意的唯一來源。

## 第二個轉變：區分程式推論與需求語意推論

AI 能從 Code 看見：

- Branch；
- Dependency；
- Call Graph；
- Duplicate Code；
- Method 大小；
- Interface 與 Inheritance。

這些是結構訊號。

需求語意則需要回答：

- 誰會要求改變？
- 為什麼改變？
- 哪一項 Policy 會改變？
- 哪些行為必須一起改變？
- 哪些行為應該彼此獨立？
- 哪些契約必須保持？

因此，AI 的設計判斷至少要區分：

### Code Fact

可以由 Repository 直接確認的事實，例如某個 Method 呼叫三個 Dependency。

### Requirement Fact

由 Requirement、Acceptance Criteria 或已確認決策支持的事實。

### Semantic Inference

從 Code、Test 與 Caller 推測的語意，例如某個 Branch 可能代表不同 Policy。

### Missing Context

可能改變結論，但目前無法取得的資訊。

AI 不能把「存在 Branch」直接寫成「存在獨立 Strategy」。

## 第三個轉變：每一項變動性都必須有根

每個 Responsibility、Variation Point、Extension Point 與 Abstraction，都應該可以回答：

> 它來自哪個 Actor、Requirement、Policy、Constraint 或 Change Scenario？

```text
Requirement Source
→ Change Driver
→ Design Boundary
→ Code Structure
```

如果找不到 Requirement Source，這項變動性可能只是從 Code Shape 想像出來的。

```text
Branch / Similar Code / Large Method
→ 推測未來可能改變
→ 建立 Abstraction
→ 找不到 Requirement Source
```

這是無根的變動性。

它會讓系統為沒有證據的未來，先付出今天的複雜度。

## 第四個轉變：允許不確定性

AI 通常被期待提供完整答案。

但設計分析經常缺少：

- 外部 Caller；
- Business Policy；
- Ownership；
- Change History；
- Transaction Constraint；
- 完整 Requirement。

在這些情況下，合理結論可能是：

> 目前可以確認結構訊號，但不足以證明存在獨立變動軸。

SOLID for AI 必須允許 Unknown 與 Uncertain，而不是把缺少 Context 自動轉換成 Pass 或 Fail。

## 第五個轉變：保存 Design Rationale

AI 維護需要的不只是最新 Code。

它還需要：

- Requirement Context；
- Architecture Decision；
- Change Driver；
- Boundary Rationale；
- Accepted Trade-off；
- Known Uncertainty。

否則下一個 Agent 仍然只能從 Code 重新猜測需求。

AI 可以重新產生 Code，卻不能重新產生從未被保存的 Design Rationale。

## 第六個轉變：同時支援 Human 與 Agent Legibility

傳統可維護性主要關心：

> 下一位 Human Developer 是否能理解與修改系統？

AI 時代還要增加：

> 下一個 AI Agent 是否能取得足夠語意，知道邊界為什麼存在？

因此，可維護性包含：

1. **Human Legibility**：人類能理解 Code、Design 與 Change Impact。
2. **Agent Legibility**：AI 能取得 Requirement、Constraint 與 Boundary Rationale。

只有固定的程式結構，不代表 Agent Legibility。真正重要的是結構與需求之間的關係是否可取得。

## SOLID for AI 的組成

可以將兩者的差異整理為：

```text
SOLID for Human
= Design Principles
+ Human Semantic Judgment
```

```text
SOLID for AI
= Design Principles
+ Accessible Requirement Context
+ Bounded Inference
+ Traceable Evidence
+ Explicit Uncertainty
+ Persistent Design Rationale
```

### Accessible Requirement Context

讓 AI 能取得 Actor、Use Case、Policy、Constraint、Acceptance Criteria 與 Change Scenario。

### Bounded Inference

限制模型不能把結構訊號直接當成需求事實。

### Traceable Evidence

讓 Responsibility 與 Abstraction 能追溯到需求或已確認的變動來源。

### Explicit Uncertainty

缺少 Context 時，保留未知，而不是創造確定答案。

### Persistent Design Rationale

讓下一個 Agent 不必重新猜測某個 Boundary 為什麼存在。

## SOLID 的新地位

SOLID 過去主要是一套 Human Design Principle：

```text
Human 理解需求
→ Human 進行設計
→ SOLID 協助組織 Code
```

AI 時代，SOLID 需要進一步成為 Requirement–Design Alignment Principle：

```text
需求語意
→ Change Driver
→ Responsibility / Variation Boundary
→ 程式結構
→ 持續驗證兩者是否對應
```

這不是增加更多規則，也不是要求 AI 產生更多 Class 與 Interface。

它要求我們把過去存在人類腦中、會議中與團隊經驗中的語意，轉換成 Human 與 AI 都能取得的工程 Context。

## 最後的問題

SOLID for AI 的重點，不是讓 AI 更像一位熟悉 Design Pattern 的開發者。

而是讓它在做出設計判斷前，能回答：

- 這項 Responsibility 的需求來源是什麼？
- 這個 Variation Point 的 Change Driver 是什麼？
- 這個 Abstraction 隔離哪一種已知變動？
- 哪些內容只是推論？
- 哪些資訊目前仍然缺少？

SOLID 過去協助 Human 控制需求變動造成的程式修改。

SOLID for AI 還必須控制模型如何推論變動，並保存 Requirement 與 Design 之間的關係。

相關 Repository：[NextEvoEco/solid-rule-engineering](https://github.com/NextEvoEco/solid-rule-engineering.git)
