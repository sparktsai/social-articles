# 沒有需求來源的抽象：AI 如何同時造成過度設計與 God Class

過度設計與 God Class 看起來是相反問題。

一個把簡單需求拆成大量 Interface、Factory、Strategy 與 Service；另一個則把所有功能塞進同一個 Class。

但兩者可能具有相同根因：

> 設計只從目前的 Code Shape 出發，沒有回到 Requirement 與 Change Driver。

缺少需求語意時，我們既可能把不需要分離的行為拆開，也可能把應該獨立改變的政策放在一起。

## 每一項變動性都應該有來源

設計討論經常使用以下說法：

- 這裡未來可能改變；
- 這裡應該可以擴充；
- 這裡需要替換實作；
- 這裡應該隔離變動；
- 這裡需要一個 Interface。

每次出現這些說法，都可以追問：

> 這個變動來自哪一項 Requirement、Actor、Policy、Constraint 或已知 Change Scenario？

### 有根的變動性

```text
Requirement / Actor / Policy / Change Scenario
    ↓
Change Driver
    ↓
Responsibility 或 Variation Boundary
    ↓
Class / Interface / Method / Dependency Design
```

例如，支付 Provider 的確會因市場、客戶合約與法規而改變，而且不同 Provider 有獨立發布節奏。這時建立穩定的支付契約與 Adapter Boundary 有明確依據。

### 無根的變動性

```text
Branch / Dependency / Similar Code / Large Method
    ↓
推測未來可能改變
    ↓
建立 Abstraction 或拆分
    ↓
找不到 Requirement Source
```

如果唯一理由是「以後可能會有第二種實作」，系統便為沒有證據的未來，先付出今天的複雜度。

這就是無根的變動性。

## False Split：把凝聚行為拆散

AI 被要求「改善 SOLID」時，可能看到：

- Method 很長；
- Dependency 很多；
- 存在條件分支；
- 有重複程式碼；
- 直接使用 Concrete Class。

接著產生：

- Interface；
- Factory；
- Strategy；
- Repository；
- Coordinator；
- Event；
- 多層 Service。

這些結構不是天然錯誤。問題是它們是否對應真實變動。

假設一個付款完成流程必須在同一個 Transaction 中驗證狀態、寫入付款、更新訂單與建立事件。將每一步拆成可獨立替換的 Service，可能帶來：

- Transaction 邊界變得不清楚；
- 呼叫順序分散在多層；
- 錯誤與補償流程變得複雜；
- 原本完整的 Business Invariant 被技術介面切碎。

這是 False Split：結構上可以拆，語意上卻不應獨立改變。

## 過度設計的實際成本

過度設計不只是檔案比較多。

它會造成：

- 更多需要命名與理解的概念；
- 更多間接呼叫與追蹤成本；
- 業務流程被 Pattern 隱藏；
- 修改簡單行為也需要跨越多層；
- Test 大量依賴 Mock 與 Setup；
- 預測錯誤時，抽象比原始程式更難修改。

抽象不是免費的。它把某種變動假設寫進 Architecture。

如果假設沒有需求證據，Architecture 只是在保存猜測。

## False Cohesion：把偶然共存視為共同責任

另一個方向是每次加入需求時，都選擇最短修改路徑。

```text
新需求進來
→ 找到目前最接近的 Function
→ 加入 Branch、Dependency 或 Side Effect
→ Test 通過
→ 下一個需求繼續加入同一處
```

長期可能形成：

- God Function；
- God Class；
- 依 Mode Flag 切換多種業務目的的 Method；
- 同時處理 Policy、Persistence、Formatting 與 Notification 的流程；
- 不同 Actor 的需求集中修改同一單元。

問題不只是程式很長，而是不同 Change Driver 被累積在同一個邊界。

如果只看現在的 Code，這些行為可能因為「已經寫在一起」而被誤認為同一責任：

> 它們屬於同一責任，因為它們位於同一個 Class；它們位於同一個 Class，因為我們認為它們屬於同一責任。

這是一個封閉循環。

## 相似程式碼可能同時導致兩種錯誤

假設兩個 Function 目前使用相同公式。

AI 可能抽取共同實作，造成 False Cohesion：兩個由不同政策驅動的行為被綁在一起。

但 AI 也可能將一個完整流程中的相似步驟，各自包裝成數層抽象，造成 False Split。

因此，「是否重複」不能直接決定「是否共用」。需要比較：

- 目的；
- 輸入與輸出；
- 錯誤語意；
- Side Effect；
- Ownership；
- Change Driver。

只有語意與變動來源一致，共用抽象才具有穩定基礎。

## Function 大小不能決定責任數量

面對大型 Method，錯誤問題是：

> 超過多少行就必須拆分？

正確問題是：

> 這些操作是否共同完成一個不可分割的 Use Case Result，還是分別實作由不同需求驅動的 Policy？

面對數個小型 Class，錯誤問題是：

> Class 越小是否越符合 SRP？

正確問題是：

> 每個邊界是否對應真實且相對獨立的變動原因，還是只把同一項凝聚行為拆散？

## AI 為什麼會在兩個極端之間擺動？

AI 的行為高度受任務描述影響：

- 「改善架構」可能觸發更多 Pattern 與 Abstraction；
- 「加入功能」可能選擇最小 Diff；
- 「移除重複」可能合併不同 Policy；
- 「不要過度設計」可能保留已混合多個 Change Driver 的大型單元；
- 「保持 Function 簡短」可能拆散 Transaction 或 Invariant。

這些指令都只描述期待的 Code Shape，沒有提供需求判定依據。

AI 需要知道的不是固定往哪個方向移動，而是：

- 哪些需求共同構成同一目的？
- 哪些變動原因彼此獨立？
- 哪些一致性要求禁止拆分？
- 哪些已知變體足以支持抽象？
- 哪些內容目前仍不確定？

## 好設計不是更多或更少抽象

Requirement-first 並不主張一律拆分，也不替大型 Function 辯護。

它要避免兩種錯誤：

1. 把應該共同改變、共同維持一致性的行為拆開。
2. 把只是目前放在一起、實際由不同需求驅動的行為視為同一責任。

所以設計的核心問題不是：

> 我們應該建立多少 Class 與 Interface？

而是：

> 每個邊界是否有真實需求來源？每個變動軸是否有根？

下一篇將進入整個系列最重要的轉折：傳統 SOLID 預設人類理解需求；當使用者變成 AI，這個隱含前提還成立嗎？

