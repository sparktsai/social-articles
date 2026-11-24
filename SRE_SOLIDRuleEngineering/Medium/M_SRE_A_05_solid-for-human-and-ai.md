# SOLID for Human 與 SOLID for AI，關鍵差異不是誰寫程式

傳統 SOLID 的五項原則不包含一套完整分析程序。

「一個 Class 應該只有一個變動原因」沒有指定到哪裡尋找這個原因；「依賴抽象」也沒有列出什麼證據足以建立抽象。

這不是原則的缺陷。

因為 SOLID 原本預設使用者是掌握需求、參與討論並對設計負責的人類。

當使用者變成 AI，真正改變的不是誰輸入程式碼，而是這個隱含前提不再可靠。

## SOLID for Human 的隱含前提

傳統 SOLID 預設人類開發者可以：

- 與 Stakeholder 討論需求；
- 理解業務背景；
- 知道設計決策的歷史；
- 辨識哪些政策可能改變；
- 對模糊資訊提出問題；
- 記得團隊接受的 Trade-off；
- 在原則衝突時作出情境判斷；
- 對錯誤設計承擔責任。

因此，一句高度濃縮的原則可能已經足夠：

> A class should have only one reason to change.

「Reason」從哪裡來，預設由人類透過需求、經驗與組織參與理解。

SOLID for Human 可以表示為：

```text
Design Principles
+ Human Semantic Judgment
```

## AI 只能使用可取得的 Context

AI 通常只能使用當次執行中可存取的：

- Prompt；
- Code；
- Test；
- Issue；
- 文件；
- Current Diff；
- Repository 內可搜尋的資訊。

如果設計理由存在於：

- 人類記憶；
- 過去會議；
- Slack 或即時通訊；
- 未記錄的架構決策；
- 已離職開發者的經驗；
- 沒有被載入 Context 的需求文件；

對當次 AI 而言，這些資訊實際上不存在。

模型看到「one reason to change」時，可能只能從 Class、Branch、Dependency、Caller 與 Test 猜測 Reason。

## SOLID for Human 與 SOLID for AI 的差異

| 面向 | SOLID for Human | SOLID for AI |
|---|---|---|
| 語意來源 | 人類理解需求與業務背景 | 受限於當次可取得的 Context |
| Change Driver | 可由溝通、經驗與組織知識辨識 | 必須被提供，否則只能標示為推論 |
| 原則用途 | 引導人類設計判斷 | 同時約束模型的推論與生成行為 |
| 面對模糊 | 可以詢問、討論並承擔判斷 | 容易自行補全缺少的語意 |
| 設計記憶 | 存在人員與團隊的長期記憶 | 不一定跨 Session 或 Agent 保留 |
| 常見偏差 | 受經驗、時間與個人偏好影響 | 容易依常見 Pattern 過度一般化 |
| 維護對象 | 主要服務下一位人類 | 同時服務 Human 與下一個 AI |
| 核心產物 | 可維護的 Code Structure | Code Structure 加上可取得的 Semantic Context |

這不是說 Human 一定理解需求，而 AI 一定無法理解需求。

人類同樣會忘記理由、誤用 Pattern、過度設計或只看 Code。AI 也能在取得充分 Context、Decision Record 與 Evidence 後作出很好的判斷。

真正差異是：

> 人類可以透過組織參與、經驗與持續溝通取得大量未文件化語意；AI 的判斷更直接受限於當次可存取的 Context。

## Human 是理解後判斷，AI 容易看 Code 猜需求

理想的人類流程是：

```text
理解需求
→ 辨識變動原因
→ 建立責任與依賴邊界
→ 使用 SOLID 評估設計
→ 產生程式結構
```

SOLID 位於需求理解之後。

AI 常見的實際流程則是：

```text
讀取現有 Code
→ 辨識結構 Pattern
→ 推測責任與變動
→ 套用 SOLID
→ 拆分或建立抽象
```

SOLID 被套用在需求語意確認之前。

這容易形成封閉循環：

```text
目前程式結構
→ 推測變動性
→ 使用推測出的變動性
   證明目前結構需要改變
```

## AI Maintain Code 會累積推論偏差

第一次生成程式碼時，需求 Prompt 可能仍在 Context 中。

數個月後，另一個 Agent 接手維護時，通常只看得到目前 Code、局部 Test、新需求與部分文件。

它會從設計結果反推設計原因：

```text
原始需求與設計理由
    ↓
目前程式結構
    ↓
AI 從程式反推語意
    ↓
AI 根據推測重新拆分、合併或抽象
```

一次偏差可能成為下一次維護的依據：

```text
缺少原始語意
→ Agent A 依 Code 推測責任
→ 產生不適當拆分或合併
→ Agent B 將新結構視為既有設計意圖
→ 建立更多 Dependency、Test 與 Abstraction
→ 偏差逐步固化
```

每次局部修改都可能合理，整體設計卻逐步偏離原始需求。

## 測試通過不代表語意被保存

Test 可以證明選定輸入仍產生選定結果，卻不一定記錄：

- 為什麼兩個 Function 必須分離；
- 為什麼某些步驟必須在同一個 Transaction；
- 哪個 Stakeholder 擁有某項 Policy；
- 為什麼當初刻意沒有建立共用抽象；
- 哪些未來變動不應影響穩定核心。

因此，AI 可以在所有 Test 通過時，破壞 Responsibility Boundary、Substitution Contract 或 Dependency Policy。

功能沒有立即失效，下一次需求變動卻會更廣、更難與更危險。

這就是可維護性的退化。

## 語意侵蝕

當 Requirement 與 Design Rationale 沒有和 Code 一起保存，後續 AI 只能從最新結構重新解釋系統。

每次重新解釋都可能：

- 遺失一部分原始 Constraint；
- 把 Inference 當成 Fact；
- 把偶然結構當成設計理由；
- 把局部整潔當成整體正確；
- 把通過 Test 當成語意仍然一致。

程式持續運作，業務邊界卻逐步消失。這可以稱為「語意侵蝕」。

AI Maintain Code 的風險不只是產生 Bug，也包括 Requirement 與 Code 的對應逐次漂移。

## 可維護性的對象已經改變

### SOLID for Human

主要問題是：

> 下一位人類開發者是否能理解、修改與測試這套程式？

### SOLID for AI

還需要增加：

> 下一個 AI Agent 是否能取得足夠語意，知道某個邊界為什麼存在？

因此，AI 時代的可維護性包含兩種 Legibility：

1. **Human Legibility**：人類能理解 Code 與設計。
2. **Agent Legibility**：AI 能取得 Requirement、Constraint 與 Boundary Rationale。

只有 Code 可讀，並不足以讓 AI 正確維護。

## SOLID 在 AI 時代的新地位

SOLID 不會因 AI 能寫程式而過時。

但它的地位需要轉變。

### 過去：Human Coding Guideline

```text
Human 理解需求
→ Human 進行設計
→ SOLID 協助組織 Code
```

### 現在：AI Generation Constraint

```text
需求描述
→ AI 推論設計
→ SOLID 限制產生的程式結構
```

### 未來：Requirement–Design Alignment Principle

```text
需求語意
→ Change Driver
→ Responsibility / Variation Boundary
→ 程式結構
→ 持續驗證兩者是否對應
```

SOLID 不應只在 Code Review 最後檢查 Class 與 Interface，而應進入 Requirement、Design、Generation 與 Maintenance 之間。

## SOLID for AI 需要增加什麼？

可以將兩者的差異表示為：

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
```

### Accessible Requirement Context

AI 必須能取得 Actor、Use Case、Policy、Constraint、Acceptance Criteria 與 Change Scenario。

### Bounded Inference

模型需要區分 Code Fact、Requirement Fact 與 Semantic Inference，不能把可能性直接當成事實。

### Traceable Evidence

Responsibility、Variation Point 與 Abstraction 應能追溯到需求或已確認的變動來源。

### Explicit Uncertainty

缺少 Context 時，正確結果可能是「目前無法確認」，而不是強迫產生完整設計結論。

## 從寫出好 Code，轉向保存設計理由

AI 可以重新產生大量 Code。

但如果 Design Rationale 遺失，新產生的 Code 只能重新猜測需求。

因此，未來更稀缺的資產可能不是程式碼，而是：

- Requirement Context；
- Architecture Decision；
- Change Driver；
- Boundary Rationale；
- Accepted Trade-off。

## 最後的轉變

SOLID for Human 假設人類先理解需求，再使用原則設計程式。

SOLID for AI 容易先讀取程式，再從結構推測需求與變動。

因此，AI 時代的 SOLID 不能只問程式是否具有某種結構。它還必須持續確認：

- Responsibility 是否有 Requirement Source；
- Variation Point 是否有真實 Change Driver；
- Abstraction 是否隔離已知變動；
- 程式邊界是否仍與需求語意相符；
- 缺少 Context 時是否保留不確定性。

SOLID 過去主要保護程式碼，避免需求變動造成失控。

SOLID for AI 還必須保護需求語意，避免它在程式生成與反覆維護中被模型重新解釋。

相關 Repository：[NextEvoEco/solid-rule-engineering](https://github.com/NextEvoEco/solid-rule-engineering.git)
