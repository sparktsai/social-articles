# SOLID 不是五條程式規則：從 OO、RUP 到可維護性

談到 SOLID，我們通常從五個字母開始：SRP、OCP、LSP、ISP、DIP。

接著列出五項定義，搭配 Class、Interface、Inheritance 與 Dependency Injection 的例子。

這種教法方便記憶，卻很容易讓人誤解 SOLID 的目的。開發者可能開始計算 Class 有幾個 Method、Function 有幾行、Dependency 有幾個，或檢查每個 Concrete Class 前面是否都有 Interface。

最後，SOLID 從處理軟體變動的設計原則，變成一套程式結構外觀。

要理解 SOLID，我們不應先問五個字母分別代表什麼，而應先問：

> 為什麼一套原本容易修改的軟體，會在持續加入需求後變得僵硬、脆弱，而且難以理解？

## 問題從軟體變動開始

軟體不會在第一次交付後停止改變。

產品增加新功能、法規改變、外部服務升級、資料格式調整、效能要求提高、錯誤處理政策改變，甚至團隊的 Ownership 也會重新分配。

真正困難的通常不是第一次完成某項功能，而是第十次修改時，團隊仍能回答：

- 應該修改哪裡？
- 為什麼應該修改這裡？
- 哪些其他部分可能受到影響？
- 哪些既有契約不能改變？
- 如何確認修改沒有破壞其他需求？

Robert C. Martin 在 2000 年的〈Design Principles and Design Patterns〉中，從 Software Rot 談起。他描述的 Rigidity、Fragility、Immobility 與 Viscosity，都不是程式碼是否美觀的問題，而是軟體在修改中逐漸失去可維護性的現象。

- **Rigidity**：修改一項需求會迫使許多其他部分跟著改變。
- **Fragility**：修改一處，其他看似無關的位置卻發生問題。
- **Immobility**：元件包含太多相依內容，難以被分離或重用。
- **Viscosity**：錯誤但快速的修改方式，比維持設計的方式更容易。

SOLID 的背景不是「如何讓 Class 看起來更專業」，而是「如何避免軟體在需求變動中腐化」。

參考：[Robert C. Martin, Design Principles and Design Patterns](https://objectmentor.com/resources/articles/Principles_and_Patterns.pdf)

## OO 提供建立邊界的語言

物件導向不只是把 Function 放進 Class，也不只是使用 Inheritance。

OO 的重要價值之一，是讓我們使用 Object、Responsibility、Collaboration 與 Interface 組織行為和狀態。

### Encapsulation

Encapsulation 不只是把 Field 設為 `private`。更重要的是，Object 隱藏內部決策，只透過穩定契約與其他 Object 協作。

當內部資料表示或演算法改變時，修改不必擴散到所有使用者。

### Abstraction

Abstraction 讓 Client 依賴它真正需要的能力，不必知道每個實作細節。

但抽象不是越多越好。只有當某項語意需要被多個使用者穩定依賴，或存在值得隔離的變動來源時，抽象才有工程價值。

### Polymorphism

Polymorphism 允許不同實作維持共同契約。當新變體出現時，核心流程可能不必反覆加入條件判斷。

但前提是這些實作真的能遵守相同契約，而不是只有相似的 Method Signature。

OO 提供了建立邊界的方式，卻不保證邊界一定正確。

一個 Class 仍可能包含數個由不同需求驅動的政策；一個 Interface 仍可能強迫 Client 依賴不需要的方法；一個 Subtype 仍可能破壞呼叫端預期。

這正是設計原則存在的原因。

## RUP 把需求、架構與迭代連接起來

Rational Unified Process（RUP）與 SOLID 不是同一層次的概念，SOLID 也不是由 RUP 推導而來。

但 RUP 提供了一個理解軟體變動的重要脈絡：

- Use-case driven；
- Architecture-centric；
- Iterative and incremental；
- Risk-driven。

Use Case 將 Actor 的目標與系統可觀察行為連接起來。Architecture 則支撐重要 Use Case、品質要求與主要風險。Iteration 承認需求與設計不是一次完成，而會在實作及驗證中逐步釐清。

IBM 對 RUP 的說明指出，Use Case 不只用來收集需求，也會在分析、測試、迭代規劃與維護過程中持續被引用。

參考：[IBM, RUP and Requirements Management](https://public.dhe.ibm.com/software/rational/web/whitepapers/2003/rupcmm.pdf)、[RUP Best Practices](https://public.dhe.ibm.com/software/rational/web/whitepapers/2003/rup_bestpractices.pdf)

這提供了一個重要提醒：

> 程式結構不能與需求來源分離理解。

當我們判斷一個 Method 是否具有單一責任時，不能只看它做了幾個步驟。需要知道它支援哪個 Use Case、完成什麼結果、哪些操作必須共同維持一致性，以及哪些政策由不同需求驅動。

## SOLID 如何回應需求變動

五項原則可以放回同一個問題理解：

> 當需求改變時，系統能否以合理成本完成修改，而不讓影響不必要地擴散？

### SRP：分離不同的變動原因

SRP 不是要求一個 Class 只能執行一個技術動作，而是不要讓不同 Actor、Policy 或 Requirement 的變動被迫修改同一個設計單元。

### OCP：隔離已知的變動軸

OCP 不是要求所有程式預先建立 Extension Point，而是當某種變動已經被證實會反覆發生時，新增變體不必持續破壞穩定核心。

### LSP：替換不能破壞需求契約

如果 Subtype 改變前置條件、結果、副作用或錯誤行為，呼叫端就必須知道具體實作。表面上的抽象便沒有真正隔離變動。

### ISP：不同 Client 的需求不應被綁在一起

Interface 應該由使用者需要的能力形成，而不是把提供者能做的所有事情集中成一份大型契約。

### DIP：穩定政策不應被易變細節控制

資料庫、Framework、Vendor API 或傳輸技術改變時，不應迫使核心 Business Policy 跟著重寫。

但這不代表每個 Concrete Class 前面都必須有 Interface。依賴反轉必須對應真實的政策、替換或隔離需求。

## 可維護性不是程式碼外觀

SOLID 所追求的可維護性至少包含：

- 能找到應該修改的位置；
- 能理解修改的業務理由；
- 能限制修改影響範圍；
- 能保留既有契約；
- 能獨立測試受到影響的部分；
- 能判斷哪些行為應該一起改變；
- 能判斷哪些需求不應互相牽連。

因此，一個大型 Method 不一定違反 SRP，一個小型 Class 也不一定符合 SRP。

真正的問題是：

> 當需求改變時，哪些程式單元會因為哪些原因被修改？

## 從需求變動重新理解 SOLID

如果不知道系統會因什麼原因改變，就無法可靠判斷什麼設計比較容易維護。

Change Driver 可能來自不同 Actor、Business Policy、法規、外部系統、失敗語意、品質要求、Ownership 或 Release Cadence。

因此，合理的推導方向應該是：

```text
Requirement Source
    ↓
Change Driver
    ↓
Responsibility / Variation Boundary
    ↓
Package / Class / Interface / Method
```

SOLID 不是從最後一層的程式結構開始打分數，而是幫助我們檢查：程式邊界是否合理反映需求變動。

這也是 AI Generate Code 出現後，SOLID 必須被重新討論的原因。

AI 可以快速產生看起來符合五項原則的結構。但如果它不知道真正的 Change Driver，這些 Interface、Strategy 與 Service 究竟是在隔離需求變動，還是在模仿 SOLID 的外觀？

下一篇將討論：當程式碼的生產速度與生產者都改變後，SOLID 是否仍然重要。

