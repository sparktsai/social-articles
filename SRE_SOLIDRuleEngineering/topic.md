# SOLID Rule Engineering：從設計原則到 AI 可執行的工程判定契約

## 文件定位

這是一份跨平台共用的繁體中文內容概要，先定義要傳達的核心觀念與完整論述，不針對 LinkedIn、X 或 Medium 的篇幅、語氣及格式進行改寫。

後續各平台版本應從這份概要選擇內容，而不是各自重新定義主張。

---

## 一句話主張

> SOLID 的目的不是讓程式碼符合某種外觀，而是提高物件導向軟體面對需求變動時的可維護性；面對 AI 產生與維護的程式碼，我們需要把 SOLID 轉換成一套以需求與變動原因為起點、要求證據、允許不確定性，並能分別判斷符合性、實際影響與修正必要性的工程契約。

這套契約還需要保存需求語意與程式結構的對應，避免後續 AI 只從當前 Code 反推設計意圖，並在反覆維護中累積不當的拆分、合併與抽象。

全文最重要的區分是：**程式推論只能觀察目前如何實作；需求語意推論才能說明系統為什麼改變。** 如果語意分解與程式分解失去對應，設計所宣稱的變動性就沒有需求來源，成為「無根的變動性」。

---

## 論述起點：從 OO、RUP 到 SOLID

這個主題不應直接從「AI 如何檢查 SOLID」開始。

如果沒有先說明物件導向設計試圖處理什麼問題，SOLID 很容易被理解成五條程式碼格式規則；如果沒有把設計放回需求變動的脈絡，也很難解釋為什麼需要分析 Change Driver。

完整的論述起點應該是：

```text
需求會持續改變
    ↓
軟體必須能被理解、修改、測試與擴充
    ↓
OO 使用物件與邊界組織行為和狀態
    ↓
RUP 將 Use Case、架構、迭代與風險放進開發流程
    ↓
SOLID 進一步提供控制修改影響的設計原則
    ↓
AI 時代需要把原則轉換成有證據的工程判定規則
```

這不是要宣稱 SOLID 源自 RUP，也不是把 OO、RUP、SOLID 描述成一條嚴格的歷史繼承線。

它們位於不同層次：

- OO 是組織軟體模型與程式結構的方式；
- RUP 是以 Use Case、Architecture、Iteration 與 Risk 管理開發的 Process Framework；
- SOLID 是降低物件導向設計修改成本與耦合風險的一組原則；
- SOLID Rule Engineering 則試圖讓 AI 能依據需求與程式證據執行這些判斷。

把它們連接起來的共同問題是：**如何面對需求變動。**

---

## OO：把可能改變的行為與狀態放進可管理的邊界

物件導向不只是把 Function 放進 Class，也不只是使用 Inheritance。

OO 的重要價值之一，是使用 Object、Responsibility、Collaboration 與 Interface，把系統中的行為和狀態組織成可以理解與替換的邊界。

### Encapsulation

Encapsulation 不只是把欄位設為 `private`。

更重要的是，物件隱藏內部決策，只透過穩定契約與外部協作。當內部演算法、資料表示或狀態管理改變時，修改不必任意擴散到所有使用者。

### Abstraction

Abstraction 讓設計聚焦於使用者真正需要的能力，而不是每個實作細節。

但抽象不是越多越好。只有當多個使用者確實依賴穩定語意，或存在需要隔離的變動來源時，抽象才具有工程價值。

### Polymorphism

Polymorphism 允許系統在維持共同契約的情況下替換行為。它可以降低新增變體時修改既有核心流程的需要，但前提是不同實作真的能遵守相同契約。

因此，OO 的核心問題不是：

> 系統裡有多少個 Class？

而是：

> 當某項需求改變時，哪個物件應該知道、哪個邊界應該承擔修改，以及哪些其他部分不應受到影響？

OO 提供了建立邊界的語言，但不保證邊界一定正確。Class 仍可能混合不相關責任，Inheritance 仍可能破壞替換契約，Interface 也可能迫使 Client 依賴不需要的能力。

這正是後續設計原則存在的原因。

---

## RUP：需求不是一次寫完，而是在迭代中被釐清與改變

Rational Unified Process（RUP）提供了一個重要的工程視角：軟體開發不是先把所有需求完全寫完，再一次完成設計與實作。

RUP 通常被描述為：

- Use-case driven；
- Architecture-centric；
- Iterative and incremental；
- Risk-driven。

這四個特性與可維護性有直接關係。

### Use Case 連接需求與設計

Use Case 描述 Actor 如何透過系統達成目標，讓設計不只是從 Class Diagram 或技術分層開始，而是能追溯到使用情境與可觀察結果。

當我們判斷一個 Method 是否有單一責任時，不能只數內部步驟。需要先知道它支持哪個 Use Case、完成什麼結果，以及不同操作是否由同一組需求驅動。

### Architecture 提供承受變動的骨架

Architecture 不是把所有未來情境都預先抽象化，而是建立足以支撐重要 Use Case、品質屬性與主要風險的結構。

它需要回答：

- 哪些決策應該穩定？
- 哪些部分預期會改變？
- 哪些 Dependency 應該被隔離？
- 哪些 Consistency Boundary 不可以被任意拆開？

### Iteration 讓設計接受反覆驗證

在反覆迭代中，需求理解會改變，設計假設會被驗證，新的風險也會出現。

這代表設計不是一次性的完成品。可維護的設計必須讓團隊能在每次需求變動時，以可控制的範圍修改系統，而不必重新理解或重寫所有內容。

### Risk 決定何處需要更強的邊界

不是所有程式都需要相同程度的抽象與隔離。

高變動、高成本或高風險的部分，通常更需要明確契約與獨立邊界；穩定且影響有限的部分，過度抽象反而可能增加理解與維護成本。

這也說明為什麼 SOLID Finding 不能自動等於立即重構。設計決策必須同時考慮需求變動的可能性、影響、成本與風險。

---

## SOLID 的目的：讓需求變動維持在可控制的範圍

SOLID 經常被教成五項獨立定義，但五項原則可以放回同一個問題理解：

> 當需求改變時，系統能否以合理成本完成修改，而不讓影響不必要地擴散？

這裡所說的可維護性，不只是程式容易閱讀，也包括：

- 能找到應該修改的位置；
- 能理解修改的業務理由；
- 能限制修改影響的範圍；
- 能保留既有契約與行為；
- 能獨立測試受到影響的部分；
- 能新增合理變體，而不持續破壞穩定核心；
- 能判斷哪些部分不應該一起改變。

### SRP：分離不同的變動原因

SRP 的重點不是一個 Class 只能做一件技術動作，而是不要讓不同 Actor、Policy 或 Requirement 的變動被迫修改同一個設計單元。

所以判斷責任之前，必須先辨識 Change Driver。

### OCP：讓已知的變動軸可以擴充

OCP 不是要求所有程式都預先建立 Extension Point，而是當某種變動已被證實會反覆發生時，讓新增變體不必持續修改穩定政策。

沒有變動證據的抽象，可能只是 Speculative Generality。

### LSP：替換不應破壞既有需求契約

如果 Subtype 改變前置條件、結果、副作用或錯誤行為，呼叫端就必須因實作差異而修改。這表示表面上的抽象沒有真正隔離變動。

### ISP：不同 Client 的需求不應被綁在一起

Interface 應該由使用者需要的能力形成，而不是把提供者能做的所有事情集中在同一份契約。當不相關 Client 被綁在一起，一方需求改變就可能影響另一方。

### DIP：穩定政策不應受易變技術細節控制

高階政策代表系統更核心、更接近業務目的的決策。資料庫、網路、Framework 或 Vendor API 改變時，不應迫使核心政策跟著重寫。

但 DIP 也不等於每個 Concrete Class 前都必須加上一個 Interface。依賴反轉必須對應真實的政策邊界、替換需求或隔離需求。

五項原則的共同目的，不是追求某種結構外觀，而是讓不同需求的改變保持相對獨立。

---

## 可維護性來自對需求變動的理解

如果不知道系統會因什麼原因改變，就無法可靠判斷什麼設計比較容易維護。

所謂 Change Driver，可能來自：

- 不同 Actor 或 Stakeholder；
- 不同 Business Policy；
- 不同法規或合規要求；
- 不同資料來源或外部系統；
- 不同失敗與補償規則；
- 不同效能、可靠性或安全性需求；
- 不同發布節奏與 Ownership；
- 已知即將加入的產品變體。

兩段程式碼現在一起改變，不代表永遠屬於同一責任；兩段程式碼現在看起來相似，也不代表未來會因相同需求而改變。

反過來說，一個設計單元包含多個操作，也不代表它一定有多個變動原因。它們可能共同維持同一項 Invariant、Transaction 或完整的 Use Case Result。

因此，可維護性不能只從目前的 Code Shape 推導。它必須建立在 Requirement、Use Case、Acceptance Criteria、Business Rule、Quality Attribute 與已知 Change Scenario 上。

這也是 SOLID Rule Engineering 選擇 Requirement-first，而不是 Code-smell-first 的根本原因。

---

## 兩種 AI 推論：程式推論與需求語意推論

AI 分析軟體設計時，至少存在兩種不同的推論路徑。

它們都會使用 Code，但推論的起點、可以回答的問題，以及容易產生的錯誤並不相同。

### 程式推論：從可見結構猜測設計意圖

程式推論主要觀察：

- Class、Method 與 Function 的結構；
- Branch 與控制流程；
- Dependency 與 Call Graph；
- Parameter、Return Value 與 Exception；
- Interface、Inheritance 與實作關係；
- Duplicate Code 與命名相似度；
- Test 所覆蓋的目前行為。

它可以可靠回答部分事實問題：

- 哪些 Method 呼叫了這個 Dependency？
- 哪些 Class 實作了這個 Interface？
- 修改這個 Signature 會直接影響哪些 Caller？
- 哪些 Branch 目前執行不同操作？
- 哪些程式片段在語法上相似？

但它無法只靠 Code 可靠回答：

- 兩個 Branch 是否代表不同 Business Policy；
- 兩個相似 Function 是否會因相同需求而改變；
- 某個 Interface 是否對應真實的替換需求；
- 某組操作是否必須維持同一個 Transaction；
- 哪個 Actor 或 Stakeholder 會要求這段行為改變；
- 哪種未來變化值得預先建立 Extension Point。

Code 呈現的是已經做出的設計結果，不一定保存做出設計決定時的需求理由。

### 為什麼程式推論容易過度

LLM 擅長從可見 Pattern 延伸可能解釋。當它看見 Branch、Dependency、相似程式碼或大型 Method 時，很容易進一步推論：

```text
存在 Branch
→ 存在多個變體
→ 未來還會增加變體
→ 應建立 Strategy

存在多個 Dependency
→ 存在多個責任
→ 應拆成多個 Service

存在相似程式碼
→ 代表同一概念
→ 應建立共同 Abstraction
```

第一步可能是可觀察的程式事實，後面幾步卻已經變成未經需求支持的語意推測。

這就是程式推論容易「過度」的原因：它會把目前結構中可能存在的變動，延伸成設計必須支援的變動軸。

問題不是 AI 使用了推論，而是它沒有清楚標示從 Code Fact 跨越到 Requirement Inference 的位置。

### 需求語意推論：尋找變動的來源

需求語意推論從以下證據開始：

- Actor 與 Stakeholder Goal；
- Use Case 與 User Journey；
- Acceptance Criteria；
- Business Rule 與 Policy；
- Quality Attribute；
- Regulatory Constraint；
- Failure、Compensation 與 Consistency Requirement；
- Ownership 與 Release Cadence；
- 已知 Change Scenario 與 Requirement History。

它要回答的不是「Code 看起來可能怎麼變」，而是：

- 誰會要求改變？
- 為什麼改變？
- 哪一項政策會改變？
- 哪些行為必須一起改變？
- 哪些行為應該彼此獨立？
- 改變時哪些契約必須保持不變？
- 哪些變動已經有證據，哪些只是想像？

需求語意推論才能為 Change Driver 提供來源。

例如，Code 中出現兩個 Branch，只能證明目前存在兩條執行路徑。若需求顯示它們分別由不同法規、不同客戶類型或不同發布節奏驅動，才有理由把它們視為獨立變動軸。

反過來，如果兩個 Branch 共同維持同一項 Business Invariant，它們在結構上不同，也不代表應該拆成兩個可獨立替換的策略。

### 變動性必須有根

SOLID 設計經常使用以下語言：

- 這裡可能改變；
- 這裡需要擴充；
- 這裡應該可替換；
- 這裡要隔離變動；
- 這裡需要一個抽象。

但每一項變動性都應該可以追問：

> 這個變動來自哪一項 Requirement、Actor、Policy、Constraint 或已知 Change Scenario？

如果無法回答，這項變動性可能只是從程式結構想像出來的。

```text
有根的變動性
Requirement / Actor / Policy / Change Scenario
    ↓
Change Driver
    ↓
Responsibility 或 Variation Boundary
    ↓
Class / Interface / Method / Dependency Design
```

相對地：

```text
無根的變動性
Branch / Dependency / Similar Code / Large Method
    ↓
推測未來可能改變
    ↓
建立 Abstraction 或拆分
    ↓
找不到對應的 Requirement Source
```

無根的變動性會造成 Speculative Generality：系統為沒有證據的未來付出當下的複雜度。

### 語意分解與程式分解必須能相互追溯

需求語意可以被分解為：

- Business Capability；
- Use Case；
- Observable Outcome；
- Policy；
- Invariant；
- Change Driver。

程式可以被分解為：

- Package；
- Module；
- Class；
- Interface；
- Method；
- Function。

兩者不需要一對一，但必須能說明彼此的對應關係。

```text
Requirement Semantic Unit
    ↕ traceability
Implementation Unit
```

如果只有語意分解，沒有對應到程式位置，就無法落實設計、修改與驗收。

如果只有程式分解，沒有對應到需求語意，就無法證明某個邊界代表真實責任或真實變動軸。

因此，SOLID Rule Engineering 的重點不是讓 AI 對 Code 做更多推論，而是約束它：

1. 先區分 Code Fact 與 Semantic Inference。
2. 為每個 Change Driver 尋找 Requirement Source。
3. 把語意單元映射到實作單元。
4. 找不到來源時標示 `uncertain`，而不是創造變動性。
5. 只有在變動性有根時，才據此建議拆分、抽象或依賴反轉。

---

## 只從 Code 出發，會同時導致過度設計與功能過大

過度設計與功能過大看起來是兩個相反問題：

- 過度設計把簡單需求拆成太多 Layer、Interface、Pattern 與 Extension Point；
- 功能過大則把越來越多行為持續堆進同一個 Function、Class 或 Module。

但兩者往往具有相同根因：**設計判斷只從現有 Code Shape 出發，沒有回到 Requirement、Use Case、Change Driver 與 Consistency Boundary。**

Code 可以顯示系統現在如何實作，卻不一定能完整回答：

- 哪些行為代表同一個業務目的？
- 哪些政策會因不同需求而獨立改變？
- 哪些步驟必須保持在同一個 Transaction？
- 哪些變體已經存在，哪些只是推測未來可能出現？
- 哪些 Client 真正需要替換能力？
- 哪些相似程式碼只是偶然相似？
- 哪些修改風險值得建立抽象邊界？

缺少這些答案時，設計很容易朝兩個極端移動。

### 極端一：由 Code Smell 推動的過度設計

如果設計只根據程式外觀，常見推論會是：

```text
Method 很長
→ 必須拆成多個 Method 或 Class

Dependency 很多
→ 每個 Dependency 都需要 Interface

出現條件分支
→ 必須套用 Strategy Pattern

兩段程式碼相似
→ 必須抽取共同 Abstraction

目前只有一種實作
→ 先建立 Factory，為未來擴充做準備
```

這些做法有時正確，但不能只由 Code Smell 得出。

如果沒有已知變動軸、替換需求、獨立 Client 或風險隔離需求，新增抽象可能只會帶來：

- 更多需要命名與理解的概念；
- 更多間接呼叫與追蹤成本；
- 實作分散在過多檔案；
- 修改簡單行為時需要跨越多層；
- 實際業務流程被技術 Pattern 隱藏；
- 未來需求與預測不同時，錯誤抽象反而更難修改。

過度設計不是因為開發者「太重視品質」，而是抽象沒有對應可證明的變動需求。

### 極端二：由現有流程累積出的功能過大

另一個方向是只觀察目前程式是否可以完成工作。

每次新增需求時，開發者或 AI 找到目前最接近的 Function，直接加入新的判斷、Dependency、Side Effect 與例外處理：

```text
新需求進來
→ 找到目前可以完成相近工作的 Function
→ 在原有流程加入一個 Branch 或 Step
→ 測試通過
→ 下一個需求繼續加入同一處
```

長期下來可能形成：

- God Function；
- God Class；
- 依 Mode Flag 切換多種業務目的的 Method；
- 同時處理 Policy、Persistence、Formatting 與 Notification 的流程；
- 不同 Actor 的需求集中修改同一個單元；
- 任何小修改都必須重新驗證整個巨大範圍。

問題不只是程式很長，而是不同 Change Driver 被累積在同一個邊界裡。

如果只看現有 Code，所有行為可能因為「現在都在這裡」而被誤認為同一責任。這是一種由實作反推需求的循環論證：

> 它們屬於同一責任，因為它們寫在同一個 Class；它們寫在同一個 Class，因為我們認為它們屬於同一責任。

只有回到需求來源、Actor、Policy、Failure Semantics 與 Change History，才能打破這個循環。

### 拆得太多與放得太多，不能只靠結構判斷

面對一個大型 Method，正確問題不是：

> 超過多少行就必須拆分？

而是：

> 這些操作是否共同完成一個不可分割的 Use Case Result，還是分別實作由不同需求驅動的政策？

面對數個小型 Class，正確問題也不是：

> Class 越小是否越符合 SRP？

而是：

> 每個邊界是否對應真實且相對獨立的變動原因，還是只把同一項凝聚行為拆散？

因此，需求驅動分析不是一味要求拆分，也不是替大型 Function 辯護。它要避免兩種錯誤：

1. **False Split**：把應該共同改變、共同維持一致性的行為拆開。
2. **False Cohesion**：把只是目前放在一起、實際由不同需求驅動的行為視為同一責任。

### AI 會放大這兩種問題

AI 很容易依照 Prompt 中可見的局部訊號採取行動：

- 被要求「改善架構」時，它可能大量抽取 Interface、Service、Factory 與 Pattern；
- 被要求「加入功能」時，它可能選擇最短修改路徑，把新行為塞進現有大型流程；
- 被要求「移除重複」時，它可能合併語法相似但業務意義不同的程式；
- 被要求「不要過度設計」時，它又可能保留已經混合多個 Change Driver 的巨大單元。

這些結果不一定來自 AI 不理解 SOLID，而是任務沒有提供足夠的需求語意與判定邊界。

AI 需要的不只是「避免過度設計」或「保持 Function 簡短」兩句互相拉扯的指令，而是一套能回答以下問題的 RULE：

- 哪些需求共同構成同一目的？
- 哪些變動原因彼此獨立？
- 哪些一致性要求禁止拆分？
- 哪些擴充需求足以支持抽象？
- 目前證據不足時應保留什麼不確定性？

這正是從 Code-first 轉向 Requirement-first 的實際價值：不是讓設計固定朝「更多抽象」或「更少抽象」移動，而是讓抽象與邊界都有需求證據。

---

## 想處理的問題

當我們要求 AI Coding Agent「遵守 SOLID」時，看似已經提出一項明確要求，實際上仍缺少許多工程判定所需的資訊：

- 要分析哪些程式範圍？
- 哪些需求、驗收條件與業務規則是判定依據？
- 要查看哪些呼叫端、測試、依賴與外部副作用？
- 如何判斷兩組行為是否具有獨立的變動原因？
- 需要提出哪些可定位的證據？
- 資訊不足時，應該判定通過、失敗，還是不確定？
- 發現違反原則後，是否代表必須立即重構？
- 如何避免 AI 為了讓檢查全部通過而過度拆分、過度抽象？

單純把 SOLID 五項原則寫進 Prompt 或 `SKILL.md`，通常只能提醒 AI 使用某些設計概念，不能保證它依據一致的工程標準完成分析。

因此，真正需要建立的不是另一份 SOLID 教學，也不只是 Code Review Checklist，而是讓 AI 能夠執行、舉證、判定並完成驗收的規則系統。

---

## 核心觀念一：SOLID 不是結構分數

許多工具或檢查方式會從程式結構開始：

- Function 或 Method 有幾行？
- Class 有幾個 Method？
- 使用了幾個 Dependency？
- Interface 有幾個成員？
- Cyclomatic Complexity 是多少？
- 是否存在重複程式碼？
- 是否依賴 Concrete Class？

這些資料有價值，但只能指出「值得進一步檢查的位置」，不能單獨證明違反 SOLID。

例如：

- 一個很長的 Method 仍可能只完成一個具有一致性要求的業務目的。
- 一個只有幾行的 Method 也可能同時實作兩個獨立政策。
- 多個 Dependency 可能共同支援同一個完整的業務操作。
- 兩段相似程式碼可能代表不同業務概念，未來會因不同需求而改變。
- 依賴 Concrete Class 不一定需要 Interface；如果沒有替換、隔離或變動需求，新增抽象反而可能提高維護成本。

所以結構指標應該是 Signal，不是 Verdict。

SOLID 真正關心的是責任、變動、契約、使用者需求與依賴政策。這些問題不能只從數量得到答案。

---

## 核心觀念二：分析應從需求語意開始

一般靜態分析或 Code Smell 檢查通常採用以下方向：

```text
程式結構
    ↓
指標或 Pattern
    ↓
可能的設計問題
```

SOLID Rule Engineering 採用相反方向：

```text
需求／驗收條件／業務規則／變動原因
    ↓
對應到 Package／Class／Interface／Method
    ↓
選擇適用的 SOLID RULE
    ↓
根據證據完成判定
```

分析結果不應只是：

> 這個 Method 太長，因此違反 SRP。

而應該接近：

> 需求 A 與需求 B 具有彼此獨立的變動原因，兩項政策目前分別由同一個 Method 內的不同操作群組直接實作，因此形成責任耦合。

同樣地，分析也可能得到「目前不需要拆分」的結論：

> 這個 Method 雖然協調多個步驟，但所有步驟共同完成一個具有原子性要求的結果，目前沒有證據顯示其中存在獨立政策，因此不建議只因操作數量而拆分。

這種判定可以被檢查、質疑，也能在取得新需求後重新評估。

---

## 核心案例：完成訂單是否有多個責任？

假設一個 `completeOrder` Method 執行：

1. 記錄付款。
2. 更新庫存。
3. 寄送收據。
4. 通知倉庫。

如果只看程式結構，很容易直接認為它有四個責任。

但工程判定需要先確認：

- 對使用者而言，主要的可觀察結果是什麼？
- 哪些操作必須在同一個 Transaction 中成功或失敗？
- Email 失敗是否應該讓付款 Rollback？
- 通知倉庫是完成訂單的必要條件，還是可延後處理的外部效果？
- 付款、庫存、收據與倉庫通知分別由哪些需求或業務角色驅動？
- 這些政策是否會彼此獨立地改變？
- 不同呼叫端是否依賴不同的結果或副作用？

它可能是一個完整且凝聚的 Application Orchestration，也可能把數個獨立的業務政策混合在一起。

結論不能由「有四個步驟」直接推導，而需要需求與行為證據。

---

## 核心觀念三：給 LLM 的 RULE 必須包含判定邊界

「一個 Function 應該只有一個責任」是原則描述，但不是完整的 LLM 工程規則。

一條可供 AI 執行的 RULE 至少要包含：

- 規則目的；
- 適用對象與適用條件；
- 必要輸入與上下文；
- 分析程序；
- 必要證據；
- 判定狀態與條件；
- 例外情況；
- 禁止使用的判定捷徑；
- 完成條件；
- 建議與重新驗收方式。

例如，Method 層級的 SRP 規則可以要求 AI：

1. 使用「動詞＋業務對象＋可觀察結果」陳述 Method 的主要目的。
2. 列出主要操作、輸出、錯誤與副作用。
3. 依業務意圖將操作分組。
4. 把各組操作對應到需求、驗收條件、呼叫端或測試。
5. 找出每組政策的變動來源。
6. 判斷它們屬於同一個凝聚政策，還是具有獨立變動原因。
7. 為每項判定提供程式位置與語意依據。

同一條 RULE 也必須限制 AI 不可以：

- 只因行數過多就判定違反 SRP；
- 只因 Dependency 數量多就要求拆分；
- 只因程式碼相似就要求共用；
- 沒有真實變動軸就新增 Interface 或 Design Pattern；
- 把協調多個步驟直接視為多個責任；
- 為了讓報告全部通過而改變既有外部行為；
- 在缺少關鍵上下文時宣稱符合規則。

RULE 不會消除 LLM 的語意判斷，而是為判斷建立明確的輸入、程序、證據與決策邊界。

---

## 核心觀念四：判定不應只有 Pass 與 Fail

實際工程分析至少需要以下狀態：

- `pass`：有足夠證據支持符合規則。
- `warning`：存在風險訊號，但不足以證明違反。
- `fail`：有明確反例與可定位證據。
- `uncertain`：缺少的上下文可能改變結論。
- `not-applicable`：規則不適用於目前對象。
- `accepted-exception`：不符合一般規則，但有已確認且可追蹤的例外理由。

其中，`uncertain` 特別重要。

當需求不完整、外部呼叫端不可見，或業務意圖只能從程式與測試推測時，AI 應把推論與事實分開。資訊不足不是自動通過，也不應被包裝成高信心失敗。

不確定性本身就是一項工程結果。它指出修改前還需要確認什麼。

---

## 核心觀念五：符合性、實際影響與修正必要性必須分開

一般 Review 經常把三個問題壓縮成一句話：

> 這段程式違反 SRP，所以必須拆分。

實際上需要分別回答：

1. **Rule Compliance**：是否符合該項規則？
2. **Actual Impact**：目前造成什麼實際影響或風險？
3. **Remediation Necessity**：現在是否需要修正？

某項規則可能判定為 `fail`，但目前影響有限：

- 程式已經穩定且很少變動；
- 影響範圍受到隔離；
- 缺少足以安全重構的測試；
- 元件即將被替換；
- 修正風險大於目前問題。

相反地，一項 `warning` 也可能因即將到來的需求而需要優先處理。

因此修正建議可以分為：

- `none`：不需要處理；
- `optional`：可改善，但不是必要工作；
- `planned`：應納入後續規劃；
- `before-change`：在下一次相關需求修改前處理；
- `immediate`：目前已有明確且高影響的問題。

SOLID Finding 是工程決策的輸入，不是自動重構命令。

---

## AI 維護程式碼：推論偏差會在反覆修改中累積

AI 擅長產生局部看起來一致、整潔且符合常見模式的程式碼。它也很容易：

- 抽取 Helper；
- 建立 Interface；
- 套用 Design Pattern；
- 移除重複程式碼；
- 縮短 Method；
- 重整 Class 邊界。

但局部整潔不等於保存業務意圖。

AI 可能因為語法相似而合併兩個具有不同變動原因的 Function，也可能把一個有意義的 Transaction 邊界拆開，或建立沒有實際替換需求的抽象。

當後續維護也由 AI 進行時，問題會比第一次產生程式碼更明顯。

### AI 維護通常從結果反推原因

第一次設計系統時，團隊可能同時掌握：

- 原始 Requirement；
- Use Case 與 Acceptance Criteria；
- Architecture Decision；
- 曾經評估但放棄的替代方案；
- Transaction、Security 與 Reliability Constraint；
- 不同 Stakeholder 的 Change Driver。

但後續 AI Agent 接到維護任務時，往往只取得：

- 目前的 Code；
- 局部測試；
- 一段新的需求 Prompt；
- 目前要修改的檔案；
- 不完整或已經過時的文件。

這時 AI 不是從完整需求推導設計，而是從設計結果重建可能的需求語意。

```text
原始需求與設計理由
    ↓
目前程式結構
    ↓
AI 從程式反推語意
    ↓
AI 根據推測重新拆分、合併或抽象
```

只要中間遺失了設計理由，AI 重建出的語意就可能與原始需求不同。

### 語意分解與程式分解是兩件事

語意分解要回答：

- 系統要完成哪些業務目的？
- 哪些政策由不同 Actor 或 Requirement 驅動？
- 哪些行為必須共同維持同一項 Invariant？
- 哪些失敗可以獨立處理？
- 哪些變動應該彼此隔離？

程式分解則把這些理解映射成：

- Package；
- Module；
- Class；
- Interface；
- Method；
- Function；
- Dependency 與呼叫關係。

理想情況下，程式邊界應該反映語意邊界。但兩者不是天然等價。

一個 Class 可能包含多個業務目的；一個 Use Case 也可能需要多個 Object 協作完成。相同的語意可以有數種合理實作結構，而相似的程式結構也可能承載完全不同的業務意義。

如果 AI 只從 Syntax、命名、Dependency 與 Call Graph 分解程式，它很容易把「目前寫在一起」當成「語意上應該在一起」，或把「可以在結構上拆開」當成「業務上應該拆開」。

### 不當設計會在反覆維護中累積

一次推論錯誤可能只造成一個不理想的抽象；經過多次 AI 維護後，錯誤會成為下一次判斷的新依據。

```text
缺少原始語意
    ↓
Agent A 依 Code 推測責任
    ↓
產生一次不適當的拆分或合併
    ↓
Agent B 把新結構視為既有設計意圖
    ↓
再建立更多依賴、測試與抽象
    ↓
偏差逐步固化
```

例如：

- Agent A 把兩個語法相似但政策不同的 Function 合併。
- 新的共用 Function 使兩組測試都依賴同一個實作。
- Agent B 因為看到共同呼叫與共同測試，進一步判斷它們屬於同一責任。
- 後續新需求只能在共用 Function 中增加更多 Flag 與 Branch。
- 最後形成一個表面上高度共用、實際上混合多個 Change Driver 的大型單元。

反方向也可能發生：

- Agent A 將一個凝聚的 Transaction 拆成多個 Service。
- Agent B 對每個 Service 建立 Interface 與 Factory。
- Agent C 再為跨 Service 的一致性補上 Coordinator、Event 與補償流程。
- 原本簡單且必須共同成功的行為，逐步變成難以理解的過度設計。

每一次修改在局部都可能合理，整體設計卻逐步偏離原始語意。

### 測試通過不代表語意邊界仍然正確

既有測試通常可以證明選定輸入仍得到選定結果，但不一定記錄：

- 為什麼兩項行為應該分離；
- 為什麼兩個步驟必須位於同一個 Transaction；
- 哪個 Stakeholder 擁有某項 Policy；
- 哪些未來變動不應影響目前核心；
- 為什麼當初刻意沒有建立共用抽象。

因此，AI 可以在所有測試仍然通過的情況下，破壞 Responsibility Boundary、Substitution Contract 或 Dependency Policy。

功能行為沒有立即失效，但下一次需求變動會變得更難、更廣、更危險。這就是可維護性的退化。

### 語意侵蝕

當需求語意沒有與程式邊界一起保存，後續 AI 只能不斷從最新 Code 重新解釋設計。

每一次重新解釋都可能：

- 遺失一部分原始限制；
- 把 Inference 當成 Fact；
- 把偶然結構當成設計理由；
- 把局部整潔當成整體正確；
- 把通過測試當成維持語意。

程式可能持續運作，業務邊界卻逐步消失。這可以稱為「語意侵蝕」。

AI MaintainCode 的主要風險不只是產生 Bug，而是讓 Code 與 Requirement 之間的對應逐次漂移，最後沒有人或 Agent 能清楚說明某個邊界為什麼存在。

因此，AI 維護需要的不只是更多 Code Context，而是能把 Requirement、Change Driver、Rule Decision 與 Maintenance Constraint 一起帶入下一次修改的語意 Context。

---

## 分析 Artifact 的長期價值

需求驅動的 SOLID 分析不只產生一份給 Reviewer 閱讀的報告，也能產生：

- Requirement–Code Map；
- Rule Decision 與證據；
- 已知的 Change Drivers；
- Transaction 與 Consistency Boundary；
- Accepted Exception；
- Uncertainty 與待確認假設；
- Maintenance Constraint。

例如：

```text
- 不可只因 formatReceipt 與其他 Formatter 相似就合併；兩者由不同需求擁有。
- 不可把 warehouse.notify 移入資料庫 Transaction；通知失敗不應回滾付款。
- 修改 completePayment 前必須重新確認 AC-002 與 SRS §5.1 的關係。
- 此處的呼叫端分析不包含外部 Plugin，因此目前結論為 uncertain。
```

如果這些 Artifact 與 Repository 一起保存，未來的 AI 維護 Agent 可以在修改前讀取。

它們便不只是分析輸出，而是 LLM 可讀的維護契約，用來保存「為什麼這個邊界存在」。

---

## Skill 的定位

`solid-rule-engineering` 是一套以需求語意為起點、唯讀執行的 SOLID 分析 Skill。

它不是：

- 自動重構工具；
- SOLID 分數計算器；
- 固定閾值的 Linter；
- Design Pattern 產生器；
- 保證程式設計正確的形式驗證工具。

它負責：

- 確認分析範圍與可用證據；
- 建立需求、驗收條件、變動原因與程式單元的映射；
- 只選擇目前對象真正適用的 SOLID RULE；
- 區分 Repository Fact 與 Semantic Inference；
- 逐條產生有證據的判定；
- 分別評估符合性、實際影響與修正必要性；
- 提出與證據及風險相稱的建議；
- 保留不確定性、例外與缺少的上下文。

Skill 採用唯讀設計，不修改 Code、Test、Requirement 或 Configuration。它的責任是分析與建議，不是自行完成重構。

---

## 三種使用模式

### Design Mode

在實作前，根據 PRD、SRS、User Story、Acceptance Criteria 或一段需求 Prompt，分析可能的責任與依賴邊界。

輸出是設計建議、假設與未解問題，不直接把推測當成唯一正確的 Code Structure。

### Review Mode

在實作過程中，分析 Partial Code 或 Current Diff，檢查程式結構是否仍符合已知需求語意，並區分事實與推論。

### Acceptance Mode

在實作完成後，結合完整 Code、Caller、Test 與 Diff，為每個適用 RULE 提供支持判定或明確的 Evidence Gap。

其中一個實際使用情境是 PR 前自我審查。即使沒有正式 SRS，也可以使用 Issue、User Story、PR Description 或開發 Prompt 作為輕量需求依據。

---

## Skill 與 Rule 的分工

### Skill

Skill 定義 AI 應該何時啟用這項能力、如何收集上下文、依什麼順序分析，以及輸出什麼報告。

### Rule

Rule 定義各項 SOLID 原則在特定層級的：

- 適用條件；
- 必要證據；
- 評估程序；
- 判定狀態；
- 工程限制；
- 例外；
- 完成標準。

### Tool

搜尋、Call Graph、Dependency Analysis、Complexity、Duplicate Detection、Compile 與 Test 等工具負責提供客觀資料，但不應單獨替代語意判定。

### Acceptance Report

報告保存 Scope、Rule Version、Evidence、Decision、Impact、Remediation Necessity、Exception 與 Uncertainty，讓結果可以被重查及重新驗收。

---

## 目前 Rule Pack 的涵蓋範圍

目前版本為 Rule Pack `0.2.0`，包含：

- `SEM`：在套用 SOLID 前建立需求語意與程式映射；
- `SRP`：責任與獨立變動原因；
- `OCP`：面對已證實變動軸時的擴充邊界；
- `LSP`：替換時的前置條件、後置條件、不變量與副作用；
- `ISP`：Interface 是否符合實際 Client 的需要；
- `DIP`：高階政策與技術細節之間的依賴方向；
- `REC`：建議是否與實際影響、成本及風險相稱。

分析層級包含 Package、Class、Interface、Method 與 Function。

---

## 專案目前提供的內容

公開 Repository 包含：

- `SKILL.md`：主要 Skill Contract；
- `references/rule-schema.md`：Rule Schema；
- `references/oo-solid-rules.md`：物件導向 SOLID Rule Pack；
- `references/srp-function-rules.md`：Function／Method SRP Rules；
- `references/acceptance-report.md`：分析報告要求；
- `templates/`：分析報告、需求與程式映射、Rule Authoring Template；
- `examples/`：端到端 SRP Review 範例；
- `evals/`：Skill Regression Cases；
- `platforms/`：Codex、Claude Code、Copilot 與 OpenCode 使用說明；
- `agents/openai.yaml`：OpenAI Agent 設定。

Repository 採用 MIT License：

https://github.com/NextEvoEco/solid-rule-engineering

---

## 誠實限制

推廣內容不能把這套方法描述成 SOLID 的自動真理判定器。

需要明確說明：

1. **判定品質仍受需求品質限制。** 需求錯誤、過時或缺漏時，分析無法自行恢復不存在的業務知識。
2. **部分結論仍需要 LLM 進行語意判斷。** RULE 可以約束判斷，但不能把所有設計問題轉換成確定性計算。
3. **Repository 內的行為不等於完整業務意圖。** Test 與 Caller 可以提供證據，但也可能只反映目前實作。
4. **`uncertain` 不應被當成缺陷。** 它代表需要補充資訊或人工確認。
5. **符合 SOLID 不等於軟體整體品質合格。** Security、Performance、Reliability、Usability 與實際業務適用性仍需其他驗證。
6. **分析不會自動完成重構。** 唯讀邊界刻意保留了實作與驗收的獨立性。
7. **Rule Pack 仍在演進。** 現階段內容適合實驗、Review 與共同改進，不應宣稱已涵蓋所有語言、框架與架構情境。

---

## 推廣目標

### 觀念推廣

希望讀者理解：

- SOLID 是針對設計變動與契約的推理工具，不是程式結構分數。
- 程式推論能發現結構訊號，需求語意推論才能確認真正的變動來源。
- 每個 Responsibility、Variation Point 與 Abstraction 都應該追溯到 Requirement Source；否則只是無根的變動性。
- 過度設計與功能過大可能源自同一個問題：只分析 Code，沒有分析 Requirement 與 Change Driver。
- 好的設計不是一味拆分或抽象，而是讓邊界對應真實的變動原因與一致性需求。
- AI 維護不只是修改 Code，也在重新解釋 Code 的語意；若缺少 Requirement–Code Mapping，偏差會在多次維護中累積。
- AI 可以解釋 SOLID，不代表能在缺少證據時正確套用。
- Semantic Analysis 與 Structural Analysis 應互相配合。
- 不重構也可能是合理且有證據的工程決策。
- 缺少資訊時，誠實標示不確定性比輸出自信結論更有價值。

### Skill 推廣

希望合適的讀者願意：

- 閱讀 Repository 與完整範例；
- 在自己的 PR、Class 或 Method 上試用；
- 比較一般 SOLID Prompt 與 Evidence-based Review 的結果；
- 回報 False Positive、False Negative 與規則缺口；
- 提供不同語言、框架與真實需求的 Evaluation Case；
- 共同討論哪些 Rule 可以工具化，哪些必須保留語意判斷。

---

## 主要受眾

### 優先受眾

- 使用 Codex、Claude Code、Copilot 或其他 Coding Agent 的開發者；
- 需要在 PR 前進行設計自我審查的開發者；
- 關心 AI Generated Code 可維護性的 Tech Lead 與 Architect；
- 正在建立 Agent Skill、Rule Pack 或 AI Engineering Workflow 的實作者；
- 需要保存 Requirement–Code Traceability 的團隊。

### 次要受眾

- Code Reviewer；
- QA 與 Engineering Governance 實務工作者；
- 對 SOLID 教學、Clean Architecture 與 Software Design 有興趣的讀者；
- 研究 AI MaintainCode、Agent Evaluation 與語意保存的人。

### 不應優先訴求的受眾

- 只想取得自動重構結果的人；
- 希望以單一分數決定 Merge 與否的人；
- 不願提供任何需求或行為上下文，卻期待確定答案的人。

---

## 建議的完整論述順序

1. 從「需求會持續改變」開始，先建立可維護性的問題背景。
2. 說明 OO 如何使用 Object、Responsibility、Encapsulation 與 Interface 組織變動邊界。
3. 使用 RUP 的 Use-case-driven、Architecture-centric、Iterative 與 Risk-driven 視角，把需求、設計和變動連接起來。
4. 說明 SOLID 五項原則如何共同限制需求變動造成的修改擴散。
5. 區分程式推論與需求語意推論，說明只有後者能確認 Change Driver 的來源。
6. 說明語意分解與程式分解失去對應時，會產生無根的變動性。
7. 說明 Code-first 如何同時造成 False Split 與 False Cohesion，形成過度設計或功能過大。
8. 提出「要求 AI 遵守 SOLID，究竟代表什麼？」
9. 說明 SOLID 原則描述與可執行工程規則之間的差距。
10. 以行數、依賴數與相似程式碼說明 Metric 只能作為 Signal。
11. 使用 `completeOrder` 案例展示 Requirement 與 Change Driver 如何改變判定。
12. 說明 RULE 所需的輸入、程序、證據、判定與禁止條件。
13. 介紹 `uncertain`，強調缺少上下文也是分析結果。
14. 分開 Compliance、Impact 與 Remediation Necessity。
15. 延伸到 AI MaintainCode 與 Semantic Erosion。
16. 說明分析 Artifact 如何成為 LLM-readable Maintenance Contract。
17. 介紹 `solid-rule-engineering` 的模式、內容與唯讀邊界。
18. 誠實揭露限制，避免過度承諾。
19. 邀請讀者試用、提供案例與共同完善 Rule Pack。

---

## 可使用的標題方向

### 觀念型

- SOLID 不是分數：AI 時代如何保存設計意圖
- 要求 AI 遵守 SOLID，為什麼仍然不夠？
- 從 Code Smell 到工程證據：重新理解 SOLID
- AI 會寫出乾淨程式碼，但它知道邊界為什麼存在嗎？

### Skill 型

- 把 SOLID 變成 AI 可執行的工程判定契約
- SOLID Rule Engineering：從需求、證據到驗收
- 一套不自動重構的 SOLID Skill，能解決什麼問題？
- 用 Requirement–Code Mapping 審查 AI Generated Code

### 問題型

- Method 太長，就代表違反 SRP 嗎？
- AI 說程式符合 SOLID，它提出證據了嗎？
- 當 AI 同時產生程式與設計判定，誰來定義通過？
- 下一個 AI Agent 會不會把你的業務邊界優化掉？

---

## 後續平台評估時需要決定的問題

在改寫平台版本前，應先逐項決定：

1. 平台主要目標是觀念教育、引發討論、取得 Repository 訪問，還是邀請試用？
2. Article 與 Post 是否分工：Article 完整說明，Post 聚焦單一爭議點並導流？
3. 是否使用同一個 `completeOrder` 案例，讓跨平台內容具有一致識別？
4. 哪些英文工程名詞保留原文，哪些使用繁體中文？
5. 是否需要圖解「需求 → 程式映射 → RULE → 報告」？
6. 是否公開 Rule ID 與實際報告片段，增加可信度？
7. 是否把 AI MaintainCode 與 Semantic Erosion 作為第二篇內容，而不是塞入同一篇？
8. Call to Action 是閱讀、試用、Star、提供案例，還是參與討論？
9. 是否需要針對熟悉 SOLID 與不熟悉 SOLID 的讀者製作不同入口？
10. 各平台能接受多少 Repository 細節與安裝說明？

---

## 最終希望留下的印象

這個專案不是要發明另一套 SOLID 定義，也不是讓 AI 對程式碼打分數。

它延續的是一條工程思考脈絡：需求會改變；OO 提供組織責任與協作的方式；RUP 讓需求、架構、風險與迭代保持連接；SOLID 幫助設計限制變動影響；而 AI 時代還需要把這些判斷轉換成可以執行、舉證與重新驗收的規則。

它試圖處理的是更實際的問題：

> 當 AI 參與程式設計、產生與維護時，我們如何讓它知道一項設計判定需要哪些上下文、依據什麼證據、在什麼條件下算完成，以及哪些具有業務理由的邊界不應被輕易「優化」掉？

SOLID Rule Engineering 的價值不只是找出問題，而是保存判定理由。
