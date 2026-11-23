# SOLID 原本不是為了讓 Class 變小

提到 SOLID，我們通常先背五項原則，再檢查 Class、Interface、Inheritance 與 Dependency。

這很容易讓 SOLID 看起來像一套程式結構規範：

- Function 不要太長；
- Class 不要太大；
- 多使用 Interface；
- 避免 Concrete Dependency；
- 看到分支就使用 Strategy。

但在五個字母之前，SOLID 想解決的是另一個問題：

> 為什麼一套原本容易修改的軟體，會在持續加入需求後變得僵硬、脆弱，而且難以維護？

## 軟體的問題從變動開始

第一次完成一項功能，通常不是最困難的部分。

真正的困難發生在：

- 新需求必須加入既有流程；
- 原本規則需要修改；
- 外部服務或資料格式改版；
- 新客戶需要不同變體；
- 法規、安全與可靠性要求更新；
- 團隊需要理解數年前形成的設計。

一套軟體是否容易維護，不只取決於它今天能否運作，而在於明天改變時會發生什麼。

## Software Rot

Robert C. Martin 在〈Design Principles and Design Patterns〉中，從 Software Rot 描述設計逐步惡化的現象。

其中幾個典型症狀是：

### Rigidity

修改一項需求，必須連帶修改大量其他部分。

### Fragility

修改一個位置，卻讓其他看似無關的功能損壞。

### Immobility

元件與大量其他內容糾纏，難以被分離或重用。

### Viscosity

快速但破壞設計的修改方式，比維持正確邊界的方式更容易。

這些都不是 Code Style 問題，而是 Change Cost 與 Change Risk 的問題。

參考：[Robert C. Martin, Design Principles and Design Patterns](https://objectmentor.com/resources/articles/Principles_and_Patterns.pdf)

## OO 提供邊界，但不保證邊界正確

物件導向使用 Object、Responsibility、Encapsulation、Abstraction 與 Polymorphism 組織系統。

Encapsulation 讓內部決策可以改變，而不必迫使所有 Client 一起修改；Polymorphism 讓不同實作可以在共同契約下替換；Responsibility 則決定哪個 Object 應該知道或執行什麼。

但 OO 只是提供設計語言。

它仍然可能形成：

- 混合多個 Policy 的 Class；
- 破壞 Caller 預期的 Subtype；
- 綁定不相關 Client 的 Interface；
- 被 Framework 或 Database 控制的 Business Policy。

SOLID 的作用不是要求更多 Object，而是幫助我們判斷這些邊界是否能承受變動。

## RUP 提醒我們：需求、架構與迭代不能分離

Rational Unified Process 與 SOLID 不是同一套方法，SOLID 也不是由 RUP 推導而來。

但 RUP 的幾個特性提供了重要脈絡：

- Use-case driven；
- Architecture-centric；
- Iterative and incremental；
- Risk-driven。

Use Case 連接 Actor Goal 與系統行為；Architecture 支撐重要需求與風險；Iteration 承認需求理解會持續調整。

它提醒我們，程式結構不能脫離需求來源單獨理解。

當我們判斷一個 Method 是否有多個責任時，不能只數它執行幾個操作。需要知道它支援哪個 Use Case、哪些操作共同維持同一項結果，以及哪些 Policy 由不同需求驅動。

## 五項原則其實在回答同一個問題

SOLID 可以被放回一個共同問題理解：

> 當需求改變時，如何避免修改影響不必要地擴散？

### SRP：哪些原因會讓這個單元改變？

SRP 不是要求一個 Class 只能做一個技術動作，而是不要讓不同 Actor、Policy 或 Requirement 的變動被迫修改同一個單元。

### OCP：哪些已知變動不應持續破壞穩定核心？

OCP 不是預測所有未來，而是為已被證實會反覆出現的變動軸建立合適邊界。

### LSP：替換是否維持原有契約？

如果 Subtype 改變前置條件、結果、副作用或錯誤行為，Caller 就必須知道具體實作，抽象也就失去意義。

### ISP：哪些 Client 的需求不應被綁在一起？

Interface 應該由 Client 需要的能力形成，而不是把 Provider 能做的所有事集中在同一份契約。

### DIP：哪些穩定政策不應被易變細節控制？

Database、Framework、Vendor API 或傳輸技術改變時，不應迫使核心 Business Policy 一起重寫。

## SOLID 的源頭是 Change Management

從這個角度看，可維護性不只是 Code 容易閱讀。

它還包括：

- 能找到應該修改的位置；
- 能理解修改的業務理由；
- 能限制影響範圍；
- 能保留既有契約；
- 能判斷哪些行為應該一起改變；
- 能判斷哪些需求不應互相牽連。

因此，Function 長度、Class 大小與 Dependency 數量都只能作為訊號。

它們不能單獨決定一個設計是否符合 SOLID。

## Change Driver 才是責任的來源

如果不知道系統會因什麼原因改變，就無法可靠判斷什麼設計比較容易維護。

Change Driver 可能來自：

- Actor 或 Stakeholder；
- Business Policy；
- Regulatory Constraint；
- 外部系統；
- Failure 與 Compensation Rule；
- Performance、Security 或 Reliability Requirement；
- Ownership 與 Release Cadence。

合理的方向是：

```text
Requirement Source
→ Change Driver
→ Responsibility / Variation Boundary
→ Code Structure
```

而不是：

```text
Code Structure
→ 猜測 Change Driver
→ 使用猜測證明需要重構
```

## 回到 AI Generate Code

AI 熟悉五項原則，也能快速產生 Interface、Strategy、Factory 與分層架構。

但如果它不知道真正的 Change Driver，這些結構究竟是在控制需求變動，還是在模仿 SOLID 的外觀？

所以，理解 SOLID 的源頭非常重要。

如果 SOLID 只是 Class 與 Interface 的規則，AI 很容易執行。

如果 SOLID 的本質是控制 Requirement Change，AI 就必須先取得變動來源，才能作出合理設計。

這也帶出最後一個問題：如果要建立 SOLID for AI，究竟需要改變什麼？

