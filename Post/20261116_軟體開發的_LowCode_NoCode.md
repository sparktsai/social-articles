# 軟體開發的 LowCode, NoCode

## 起源

現在講到 LowCode，第一個想到的都是 Agent, Flow 使用極少量的 程式編碼開發 代理流程
NoCode，第一個想到的則是軟體開發時，使用 Vibe Coding，進行開發，完全只看 E2E 的結果，不接觸程式碼

如果更進一步，軟體開發時，使用 SDD Specification-Driven Development
只撰寫文件，看文件，看測試報告

---

## 假設

我對程式語言不熟，沒有工程師進行 Review Code，PR 可以做，等於從 意圖 到 產出
如何不 Review Code 情形下，能夠擺脫 Vibe Coding 的 測試風險
如果使用 SDD 規格驅動開發，如果是使用 prompt 由 AI 產生 規格文件，可以 Review 規格文件，Review 驗證結果

---

## 需求

過程可能會面臨什麼問題 ？
這些問題即可轉成 軟體工程 AI NoCode 情形下，如何 確認 開發品質的 治理工程

## 目前可能會碰到的問題

- 怎樣 AI 測試完的 測試報告，可以確認軟體品質
- 怎樣的測試報告內容，可以符合 HITL 所需判斷 達成 Acceptance Criteria 
- 怎樣判斷 過程中 單向 LLM 提問可以保證了解 使用者意圖，不是開發規格
- Vibe Coding 以使用者意圖為導向 和 SDD 以規格為導向，兩者間的 Gap
- 是否真的不 Review Code (不了解程式語言，系統架構)，真的可以確認可以 PR
- 使用者動作權責，AI 需要負擔的權責，這個權責不是 RDBA 中的授權 AI 存取什麼，是如何保證 軟體品質，整個軟工如何處理
- 預設流程需要 Human 扮演什麼角色
- 

## Post

### 觀點

這篇 Post 的重點不是介紹 Low-Code、No-Code、Vibe Coding 或 SDD 的差異，而是提出一個更根本的問題：

> 當 Human 看不懂 Code，還能依據什麼判斷軟體品質，並決定是否 PR？

No-Code 的真正門檻，不是 AI 能不能產生 Code，而是 Human 不看 Code，能不能判斷產出是否符合原本意圖，並透過 Acceptance Criteria 確認功能需求是否達成。但 Acceptance Criteria 的通過，不等於軟體品質已獲得保證；Human 仍必須知道哪些品質屬性與風險已被驗證，哪些尚未被驗證。

Human 仍然擁有 PR 的決定權，因此重點不是「誰有權批准 PR」，而是：

> AI 是否提供了足以支撐 Human 判斷的 Evidence？

真正的 No-Code，不只是隱藏 Code，還必須把技術執行結果還原成 Human 能理解、能驗證、能據以做出決定的 Evidence。

### 兩個 Gap

#### Intent–Specification Gap

Vibe Coding 以 Human Intent 與最終體驗為導向；SDD 則以 Specification 為開發與驗證基準。

兩者之間存在一個容易被隱藏的 Gap：

> Intent 是否被正確、完整地轉成 Specification？

```text
Human Intent
    ↓  誰確認語意沒有偏移？
Specification
    ↓
Implementation
```

即使 Specification、Code 與 Test 完全一致，仍然可能只是正確實作了錯誤的理解。

因此，Specification 符合測試結果，不等於 Specification 符合 Human Intent。

#### Technical Result–to–Human Evidence Gap

AI 可以產生 Code、執行測試並輸出 Test Report，但 Test Report 不一定足以讓不懂 Code 的 Human 判斷 Acceptance Criteria 是否達成，更不能只因 Acceptance Criteria 通過，就推論整體軟體品質已經獲得保證。

```text
Human Intent
→ Specification
→ Code
→ Test Execution
→ Technical Results
→ Human-readable Evidence
→ Human Judgment
→ Human PR
```

前半段是將 Human Intent 轉成機器能執行的形式；後半段則必須把技術結果還原成 Human 能判斷的 Evidence。

這個過程不是將 Log 排版得更漂亮，也不是把工程術語翻譯成自然語言，而是重新建立以下三者之間的關係：

- Human 原本想要什麼。
- 系統實際做了什麼。
- 哪些結果與風險已經或尚未被驗證。

### Human-readable Evidence

以下內容即使改寫成中文，仍然只是工程結果，不一定是 Human-readable Evidence：

- Unit Test coverage 87%。
- 42 個 Test Cases Passed，但沒有說明總共有幾個、幾個失敗、幾個未執行。
- HTTP Status 200。
- P95 Latency 320 ms。
- Regression Suite Passed。
- No Critical Exception。

不了解這些工程術語的人，仍然無法據此回答：

- 使用者要求的功能真的完成了嗎？
- 哪些操作與情境已經驗證？
- 實際結果是否符合原本期待？
- 哪些情況尚未測試？
- 還有哪些不能由現有測試排除的風險？
- 是否已經有足夠依據可以 PR？

例如，不只是顯示：

> Checkout E2E Test Passed.

而是還原成一份可追溯的驗證摘要：

> 本次共有 42 個 Test Cases：36 個通過、1 個失敗、5 個未執行。
>
> **已通過：**使用者將兩件商品加入購物車，套用有效折扣碼後，以模擬信用卡完成付款。訂單金額由 NT$1,200 降為 NT$1,080，付款成功，訂單已建立，庫存各扣除一件，使用者收到訂單確認。
>
> **未通過：**輸入不存在的折扣碼時，流程卡住，沒有顯示預期的錯誤訊息，使用者也無法繼續結帳。
>
> **未驗證：**信用卡付款只使用模擬刷卡環境，尚未進行實際刷卡；訂單金額 `99999999999999999999` 的極端值尚未測試；付款中斷、重複付款與庫存不足的情況也尚未驗證。
>
> 因此，現有 Evidence 只能支持「有效折扣碼加上模擬信用卡」這條功能路徑已達成 Acceptance Criteria，不能據此宣告實際付款整合或整體軟體品質已獲得保證。

Human-readable Evidence 至少應讓 Human 看見：

- Test Cases 的總數，以及通過、失敗、未執行與無法判定的數量。
- 每一項 Acceptance Criterion 對應哪些實際操作與驗證。
- 測試使用的輸入、前置條件及環境。
- 預期結果與實際結果的比較。
- 哪些案例已通過，哪些失敗，失敗時實際發生了什麼。
- 哪些情境未執行或尚無法驗證，以及未驗證的原因。
- Edge Cases 與異常路徑是否被涵蓋。
- AI 在開發與驗證過程中做了哪些假設。
- 本次變更是否影響既有功能。
- 哪些風險仍然需要 Human 親自操作或判斷。

### 核心主張

> No-Code 不只需要讓 Human 不必閱讀 Code，也必須讓 Human 不必先成為軟體工程師，才能判斷結果是否正確。

如果最後交給使用者的仍然只是 Coverage、Status Code、Latency 與一排綠色 Passed，那不是真正完成了 No-Code。

Human 只是從看不懂 Code，變成看不懂 Test Report。

### 敘事流程

1. 從 AI 已經可以依照自然語言產生 Code、執行測試並建立 PR 開始。
2. 設定前提：最後仍由 Human 決定是否 PR，但這個 Human 不懂程式語言，也無法進行 Code Review。
3. 提出第一個 Hidden Gap：Vibe Coding 的 Human Intent，是否被正確轉成 SDD 使用的 Specification？
4. 進一步指出：即使 Specification、Code 與 Test 一致，也可能只是正確實作了錯誤的理解。
5. 將焦點放在主要問題：Test Evidence 是否足以支持 Human 判斷 Acceptance Criteria 已經達成？
6. 區分 Technical Results 與 Human-readable Evidence；工程數據或自然語言摘要不等於可判斷的 Evidence。
7. 用實際操作情境說明 Evidence 如何還原 Human Intent、系統行為、驗證結果與未涵蓋風險。
8. 收斂到核心主張：真正的 No-Code 必須同時建立一個 Human-readable Quality Interface。
9. 以開放問題邀請不同角色提出自己批准 PR 所需的最低 Evidence。

### Hook

> AI 已經可以把 Human Intent 轉成 Specification、Code 和 Test。
>
> 但測試完成後，誰把技術結果還原成 Human 看得懂的 Evidence？
>
> 如果最後交給使用者的仍然是 Coverage、Status Code、Latency 和一排綠色 Passed，那不是真正的 No-Code。
>
> Human 只是從看不懂 Code，變成看不懂 Test Report。

### 開放的問題

主要問題：

> 如果你完全看不懂 Code，只能閱讀 Specification、Acceptance Criteria 和 Test Evidence，AI 至少必須提供哪些內容，你才願意 PR？

可延伸討論：

- Human 如何確認自己的 Intent 已充分、正確地傳達給 AI，而 AI 對 Intent 的理解沒有語意偏移？
- AI 應如何回述 Intent、揭露假設並提出澄清問題，讓 Human 在開發前識別「正確實作了錯誤理解」的風險？
- 除了驗證功能需求的 Acceptance Criteria，如何確認效能、安全、可用性、容錯、資料一致性與可復原性等品質屬性也有對應的驗證條件？
- AI 是否應主動建議額外的 Acceptance Criteria 或品質驗證條件，補足 Human 沒有想到、但關係軟體穩健性的邊界情境與隱性需求？
- AI 新增的驗證條件應由誰確認，如何避免 AI 自行擴大需求範圍，或把建議誤當成已經同意的需求？
- Test Evidence 應提供哪些內容，才能讓不懂 Code 的 Human 判斷 Acceptance Criteria？
- 測試步驟、畫面截圖、操作錄影、預期與實際結果、Regression 結果及未驗證風險，哪些是不可缺少的？
- Human-readable Evidence 是否應依產品、功能與風險等級而不同？
- 當 Acceptance Criteria 失敗、遺漏或尚未驗證時，Human 需要哪些資訊，才能判斷應該先修正到完善再 PR，還是可以接受風險、先 PR，並明確標註為下一次 Sprint 的待辦項目？
- 哪些失敗屬於不可 PR 的 Blocking Issue，哪些可以在有責任人、風險說明、追蹤項目與完成時限的前提下延後處理？
- 如何避免 AI 同時產生 Specification、Code、Test 與 Evidence，最後只是用自己的結果證明自己正確？

### Medium 系列拆分

若每篇上限為 900 字，可拆成 6 個主題。每篇只回答一個核心問題，其餘議題留給後續文章。

#### 一、AI 真的理解了我的 Intent 嗎？

**問題：**Human 如何確認自己的 Intent 已正確傳達給 AI？

**問題描述：**Human 使用自然語言描述需求時，往往帶有未明說的背景、假設與期待。AI 即使產出了完整的 Specification，也可能只是合理地誤解 Intent。本篇聚焦 AI 應如何回述理解、列出假設、指出模糊處並要求 Human 確認，在開發前縮小 Intent–Specification Gap。

#### 二、Acceptance Criteria 通過，為什麼不等於軟體品質沒問題？

**問題：**Acceptance Criteria 能證明什麼，又不能證明什麼？

**問題描述：**Acceptance Criteria 主要驗證功能需求，不會自動覆蓋效能、安全、可用性、容錯、資料一致性與可復原性。本篇說明「功能符合」與「品質可接受」的差別，以及為什麼 AC 全綠仍不足以宣告整體軟體品質已獲得保證。

#### 三、AI 應該主動補上 Human 沒想到的驗證條件嗎？

**問題：**AI 如何補充邊界情境與隱性需求，又不擅自擴大需求？

**問題描述：**Human 可能只提到正常流程，漏掉無效折扣碼、極端金額、重複付款、網路中斷或庫存衝突。AI 可以主動建議額外 AC 或品質驗證條件，但必須將「Human 已確認的需求」與「AI 建議的風險項目」分開，並由 Human 決定是否納入範圍。

#### 四、不看 Code，Human 需要什麼 Evidence 才能做決定？

**問題：**Test Report 要包含哪些資訊，才算 Human-readable Evidence？

**問題描述：**Coverage、HTTP 200 或「42 Tests Passed」只是 Technical Results，無法告訴 Human 總共有幾項、哪些失敗、哪些未測試，也無法說明實際用戶會遇到什麼。本篇聚焦 Evidence 如何連結 AC、操作步驟、預期與實際結果、失敗案例、未驗證範圍與剩餘風險。

#### 五、有失敗或未驗證項目，還可以 PR 嗎？

**問題：**Human 應如何決定先修完再 PR，或接受風險並延後處理？

**問題描述：**測試失敗不一定都必須阻擋 PR，但也不能只用「下個 Sprint 再修」一語帶過。本篇探討 Blocking Issue 的判定原則，以及延後處理時所需的風險說明、影響範圍、責任人、追蹤項目、完成時限與明確的 Human 風險接受。

#### 六、AI 可以用自己的測試證明自己做對了嗎？

**問題：**當 Specification、Code、Test 與 Evidence 都由同一個 AI 產生時，誰來驗證驗證者？

**問題描述：**AI 可能根據自己誤解的 Intent 寫出 Specification，再產生與該 Specification 完全一致的 Code 與 Test，最後以全數通過的 Evidence 證明自己正確。本篇聚焦如何引入 Human checkpoint、獨立驗證來源、反例與風險導向測試，避免形成封閉的自我證明循環。

### 標題方向

- 不看 Code，Human 要看到什麼，才能 PR？
- No-Code 的下一個問題，不是生成，而是品質判斷
- Human 只是從看不懂 Code，變成看不懂 Test Report？
- 真正的 No-Code，如何把技術結果還原成 Human-readable Evidence？
