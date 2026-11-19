# CRR — Chat Record Reuse

## 系列定位

AI 對話不只產生答案，也會產生問題、解釋、想法、假設、選項、推論、修正、決策與未完成工作。

這些內容通常被留在依 session 排列的 Chat History 中。對話雖然結束，其中的 Topic 卻可能仍在發展。

本系列以 **Human–AI 的角色與互動關係** 為起點，說明不同對話為何產生不同意義的內容，再進一步展示如何透過 Topic Chat Recorder 將內容保存成可攜的 Markdown，交給 Obsidian、NotebookLM、Zotero、文件、試算表、Issue Tracker 或 Git 繼續整理與利用。

核心主張：

> A conversation may end, but its topics may not.

> Capture the conversation. Reuse the knowledge anywhere.

## 產品與內容邊界

Topic Chat Recorder 負責：

- 從目前 Codex 或 Claude Code task 擷取 user／assistant 文字訊息。
- 依使用者指定的 Topic 匯出 Markdown。
- 支援完整 task 匯出，或 `start → stop` 的局部記錄。
- 保存 platform、model、session、時間、working directory 與 message trace ID。
- 排除 system、developer、reasoning、tool call、tool output 與 runtime environment 內容。

Topic Chat Recorder 不負責：

- 自動判斷或拆分 Topic。
- 自動建立 Obsidian 知識庫。
- 自動上傳 NotebookLM。
- 驗證 AI 回答或外部來源是否正確。
- 建立不可竄改或法律意義上的稽核證據。
- 證明 Human authorship、originality 或最終成果正確。

系列文章必須清楚區分產品現有能力與下游工具完成的再利用工作。

## 發佈結構

| 平台     | 數量 | 形式                              | 主要任務                                             |
| -------- | ---: | --------------------------------- | ---------------------------------------------------- |
| Medium   |   10 | 完整 Story                         | 建立完整觀點、模型、案例與工作流                         |
| LinkedIn |    8 | 2 篇 Articles＋6 篇 Posts          | Articles 建立分類與對話前方法；Posts 建立獨立專業觀點    |
| X        |   38 | 2 篇 Articles＋36 篇 short Posts  | Articles 建立完整觀點；Posts 拆解為容易回應的小單位      |

Medium 是完整論述來源，但 LinkedIn 與 X 不直接摘要 Medium。每個平台都需依自己的閱讀情境重寫。

---

# Medium — 10 Stories

## M_CRR_A_01 — Your AI Conversation Ended. Its Topics Did Not.

### 核心問題

為什麼保留 Chat History，仍然無法找回或延續真正重要的內容？

### 重點

- Chat 是一次互動的容器；Topic 才是持續發展的內容。
- 同一個 Topic 可能跨越不同 session、日期與 AI 工具。
- 長對話會混合已完成、未完成與剛出現的主題。
- 記錄的問題不是「聊天是否還在」，而是「內容是否仍可利用」。
- 從 Chat History 重新定義為 Topic Lifecycle。

### 案例

使用者先詢問 AI 對話類型，後來逐步發展成產品定位、再利用工具、系列文章與 Capafy 詳情頁。

### 讀者帶走的判斷

對話結束不代表主題完成；值得延續的 Topic 需要獨立於 chat interface 的可攜記錄。

## M_CRR_A_02 — Four Ways Humans Receive Help from AI

### 涵蓋形態

Inquiry、Learning、Advisory、Assistance。

### 核心問題

Human 都是在「向 AI 取得內容」，但取得答案、建立理解、接受建議與取得局部支援，為什麼不是同一件事？

### 重點

- Inquiry：保存具體問題、答案、釐清與衍生問題；再利用為 FAQ 與答案索引。
- Learning：保存解釋、例子、誤解與理解歷程；再利用為學習筆記與知識缺口。
- Advisory：保存選項、條件、利弊與建議理由；再利用為決策比較及採納結果回顧。
- Assistance：保存查詢、查證、來源線索與未確認項目；再利用為研究追蹤及主要工作的支援材料。
- 比較 Inquiry 與 Learning：找到答案不等於形成理解。
- 比較 Advisory 與 Assistance：前者協助選擇，後者服務另一項主要任務。
- AI 提供的答案、建議與來源線索都不能自動視為已驗證事實。

### 工具與產出

Obsidian／NotebookLM 用於 FAQ 與學習；Spreadsheet／ADR 用於建議比較；Zotero 用於外部來源管理。

### 讀者帶走的判斷

即使內容都來自 AI，它在對話中可能分別是答案、解釋、選項或待查證線索；記錄後也應進入不同工作流。

## M_CRR_A_03 — Four Ways Humans and AI Develop Content Together

### 涵蓋形態

Discussion、Exploration、Analysis、Creation。

### 核心問題

Human 與 AI 共同發展內容時，如何區分交換觀點、發現方向、建立推論與產生作品？

### 重點

- Discussion：保存觀點、分支、共識與分歧；再利用為後續討論與思想演變。
- Exploration：保存新問題、早期假設與意外方向；再利用為 research questions 與 Idea backlog。
- Analysis：保存條件、假設、關係、推論與結論；再利用為分析報告、模型與 decision record。
- Creation：保存概念、結構、草稿、替代版本與取捨；再利用為文章、簡報與未來素材。
- 比較 Discussion 與 Exploration：前者已有討論對象，後者可能仍在尋找問題。
- 比較 Analysis 與 Creation：前者建立判斷，後者形成作品。
- 保存創作過程不等於證明 Human authorship 或 originality。

### 案例

以本系列從「有哪些 AI 對話類型」逐步發展成產品定位、內容模型與系列規劃為例。

### 讀者帶走的判斷

共同發展的價值往往存在於分支、假設與被放棄的方向，而不只存在於最後答案。

## M_CRR_A_04 — Three Ways AI Evaluates or Challenges Human Work

### 涵蓋形態

Critique、Review、Dialectic。

### 核心問題

AI 對 Human 內容提出意見時，評論、審查與辯證有何差異？

### 重點

- Critique：保存評價標準、優缺點與閱讀反應；再利用為定位與表達改善。
- Review：保存問題、缺漏、標準、修正要求與處理狀態；再利用為 Issue、checklist 與再次審查。
- Dialectic：保存反例、反駁、成立條件與主張修正；再利用為論證地圖與更強的主張。
- Critique 提供評價；Review 對照標準判斷；Dialectic 透過多輪挑戰改變主張。
- Revision 與 Verification 是可能出現在三者中的活動，不必另立為互斥類型。

### 案例

同一篇產品詳情可以先接受讀者觀點評論，再接受能力邊界審查，最後用反方觀點檢驗核心主張。

### 讀者帶走的判斷

「AI 給了意見」不足以描述內容的地位；必須知道那是評價、問題判定，還是對主張的挑戰。

## M_CRR_A_05 — Reflection: When AI Helps Human Look Back

### 涵蓋形態

Reflection，以及十二種形態之間的轉換關係。

### 核心問題

當 AI 不再主要提供外部答案，而是協助 Human 回顧自己的理解、選擇與改變時，對話記錄有什麼不同價值？

### 重點

- Reflection 保存認知變化、錯誤理解、決策原因與經驗教訓。
- 它記錄的不是 AI 知道什麼，而是 Human 如何改變。
- 可再利用為 journal、retrospective、個人原則與改善計畫。
- 同一段 Chat 可以從 Inquiry 轉為 Discussion、Exploration、Analysis、Critique、Creation、Review，最後進入 Reflection。
- Verification、Revision、Organization 與 Simulation 是可以跨越多種形態的第二層活動。
- 提供十二種形態的摘要矩陣，連接主要保存內容、再利用方向與代表工具。
- 說明十二種形態不是 Topic Chat Recorder 的自動分類功能，而是協助使用者判斷什麼值得保存。

### 完整案例

回顧 CRR 對話如何從初始分類問題發展成修正版模型、再利用工具、Capafy 詳情與跨平台內容規劃。

### 讀者帶走的判斷

對話記錄不只保存 AI 的輸出，也能保存 Human 的思想如何形成、被挑戰並發生改變。

## M_CRR_A_06 — What Is Worth Recording?

### 核心問題

如果不是所有 Chat 都值得保存，應該如何選擇？

### 重點

- 值得記錄的七個條件：會延續、背景成本高、產生分支、含假設或決策、經過多輪修改、需要查證、可轉成未來成果。
- 不需要保存的情況：一次性翻譯、容易重查的單點答案、沒有後續用途的即時資訊。
- Topic 命名應描述長期問題，不使用 session ID。
- 比較完整 task 匯出與 `start → stop` 局部記錄。
- 說明「記得更多」不是目的，「保留可再利用內容」才是目的。

### 實作

展示 Topic Chat Recorder 的開始、停止、輸出目錄及 Markdown 結果。

### 讀者帶走的判斷

好的記錄策略不是保存最多，而是保存未來仍可能改變行動或理解的內容。

## M_CRR_A_07 — Reuse AI Conversations for Learning and Research

### 核心問題

如何把過去的 AI 對話轉成可持續使用的學習與研究材料？

### 重點

- Topic Chat Recorder：保存原始對話脈絡。
- Obsidian：建立連結、標籤、Topic index 與長期筆記。
- NotebookLM：針對一組來源重新提問、比較與綜合。
- Zotero：管理真正的論文、網頁、作者與出版資料。
- 對話中的 AI 回答是研究材料，不等於已驗證事實。
- 將「知道答案」轉成「知道哪些已理解、哪些仍有疑問、哪些需要來源」。

### 工作流

```text
Conversation → Topic Markdown → Obsidian / NotebookLM
                              → Zotero source verification
```

### 讀者帶走的判斷

Recorder 保存學習如何發生；知識工具負責讓學習繼續發展。

## M_CRR_A_08 — Reuse AI Conversations for Decisions, Creation, and Work

### 核心問題

對話如何轉成決策、文章、Issue 或可重複工作成果？

### 重點

- 分析與建議 → Spreadsheet decision matrix／ADR。
- 探索與創作 → 文章、簡報、產品概念與內容素材。
- 評論與審查 → Issue、checklist、修正與驗收紀錄。
- 對話與 Git commit／文件版本建立參照關係。
- 原始記錄保存完整脈絡；工作工具只承接需要執行的部分。
- 不要把長對話直接貼成文件，必須經過 Select、Verify、Organize、Transform。

### 工作流

```text
Record → Select → Verify → Organize → Transform → Trace
```

### 讀者帶走的判斷

對話記錄不是最終成果，而是可以反覆轉換的工作材料。

## M_CRR_A_09 — From One AI Discussion to a Reusable Knowledge Asset

### 核心問題

一段真實 AI 對話，如何從初始問題發展成可以持續利用的 Topic？

### 重點

- 使用本系列實際對話作為 end-to-end case。
- 從八種對話類型修正為十二種 Human–AI 互動關係。
- 說明「輔助型」如何被重新定義為查詢、查證與局部支援。
- 將類型接到工具、產出、價值與系列文章。
- 展示原始 Chat、Topic Markdown、整理後模型與 Capafy 詳情頁之間的關係。
- 比較沒有記錄時需重新解釋的成本，以及有記錄時可以直接延續的內容。
- 收斂產品定位與誠實邊界。

### 讀者帶走的判斷

Topic Chat Recorder 的價值不是多保存一份 Chat，而是讓已經投入的思考可以繼續產生結果。

## M_CRR_A_10 — Before You Talk to AI, Decide What Kind of Conversation You Need

### 核心問題

為什麼許多 AI 對話在幾輪後看似內容豐富，卻已經偏離原本的 Topic、目的與預期產出？

### 核心主張

對話漂移不一定是 AI 回答錯誤。很多時候，Human 沒有先決定要進行哪一種對話，也沒有在 AI 提出新方向時確認是否要切換模式。

AI 很擅長延伸問題、補充可能性與提出下一步。這些能力可以帶來探索，也可能讓原本只是查詢、審查或決策的對話，不知不覺變成另一個任務。

### 對話前的六項定義

```text
Topic：這次要處理哪個主題？
Mode：需要哪一種對話形態？
Purpose：為什麼要進行這段對話？
Output：結束時需要得到什麼？
Boundary：哪些延伸暫時不處理？
Stop condition：何時應該收斂、停止或另開 Topic？
```

### 十二種形態如何改變提示方式

- Inquiry：要求直接回答特定問題，不主動擴張範圍。
- Learning：要求循序解釋並檢查理解。
- Advisory：要求提出選項、條件、風險與取捨。
- Assistance：明確說明主要任務，限制 AI 只提供局部支援。
- Discussion：允許交換觀點，但維持既定 Topic。
- Exploration：明確允許發散，並在最後整理新方向。
- Analysis：先固定資料、假設、條件與判斷問題。
- Creation：定義作品、讀者、目的及 Human 保留的控制權。
- Critique：要求依指定觀點或標準提出評價。
- Review：提供檢查標準、範圍與通過條件。
- Dialectic：要求 AI 主動提出反例及挑戰主張。
- Reflection：聚焦 Human 的理解、選擇與變化，不急著產生外部答案。

### 對話中的模式切換

模式可以改變，但應該被明確看見：

```text
原始模式：Analysis
AI 提出三個新研究方向
Human 決定：
- 留在 Analysis，將新方向記入 backlog；或
- 明確切換為 Exploration；或
- 建立另一個 Topic 繼續。
```

### 每隔幾輪的檢查點

- 我們仍在處理原本的 Topic 嗎？
- 現在仍是原本選擇的對話形態嗎？
- AI 新增的內容服務原目的，還是形成另一個目的？
- 預期產出是否已經改變？
- 應該繼續、收斂，還是另開 Topic？

### 與 Topic Chat Recorder 的關係

- 開始前以 Topic 命名，協助建立對話邊界。
- 使用局部記錄保存真正屬於該 Topic 的內容。
- 若對話產生獨立方向，應建立另一個 Topic，而不是把所有內容混在同一筆記。
- 記錄能呈現何時發生漂移，但不會自動替使用者維持目的或阻止模式切換。

### 讀者帶走的判斷

不要只問「我要問 AI 什麼？」也要先問：「我希望 Human 與 AI 進行哪一種對話，最後要得到什麼？」

---

# LinkedIn — 2 Articles + 6 Posts

Article 用來完整建立十二種 Human–AI 對話形態；6 篇 Posts 則各自合併兩個相鄰觀點，形成一篇可獨立成立的完整論述。每篇先以真實工作問題作為 Hook，結尾邀請讀者分享如何處理。Posts 控制在 3,000 characters 內，正文不依賴 Article 或 Medium 連結補足主張。

## L_CRR_A_01 — Twelve Ways Humans and AI Develop a Conversation

### 核心問題

Human 與 AI 扮演的角色如何改變對話內容的意義，以及內容未來可以如何再利用？

### 文章目的

- 建立十二種對話形態的完整分類，而不是只列出名稱。
- 說明分類基礎是 Human–AI 的角色與互動關係，不是單純依工作任務分類。
- 讓讀者理解同一段 Chat 可以在不同形態之間轉換。
- 連接每種形態所產生的內容、記錄理由與再利用方向。
- 作為後續 LinkedIn Posts、Medium Stories 與 X Posts 的共同概念入口。

### 開場張力

AI conversations are often treated as question-and-answer exchanges.

But asking, learning, discussing, exploring, analyzing, creating, reviewing, and reflecting do not produce the same kind of content—even when they happen inside the same chat.

### A. Human 從 AI 取得內容

1. **Inquiry — 發問型**
   - Human 是提問者；AI 是回答者。
   - 產生具體問題、答案、釐清與衍生問題。
   - 可再利用為 FAQ、答案索引與後續提問。

2. **Learning — 學習型**
   - Human 是學習者；AI 是教師或解說者。
   - 產生解釋、例子、誤解、追問與理解過程。
   - 可再利用為學習筆記、複習材料與知識缺口。

3. **Advisory — 建議型**
   - Human 是決策者；AI 是顧問。
   - 產生候選方案、條件、風險、利弊與建議理由。
   - 可再利用為方案比較、決策回顧與採納結果評估。

4. **Assistance — 輔助型**
   - Human 是主要任務執行者；AI 是查詢、查證或局部支援助手。
   - 產生資料線索、比較結果、驗證結果與未確認項目。
   - 可再利用為研究追蹤、重新查證及寫作或工作支援。

### B. Human 與 AI 共同發展內容

5. **Discussion — 討論型**
   - Human 是對話者；AI 是討論夥伴。
   - 產生不同觀點、分支議題、共識與分歧。
   - 可用來延續討論、比較觀點與整理思想演變。

6. **Exploration — 探索型**
   - Human 是問題探索者；AI 是探索夥伴。
   - 產生新問題、早期假設、可能方向與意外發現。
   - 可再利用為新 Topic、研究問題與 Idea backlog。

7. **Analysis — 分析型**
   - Human 定義問題與條件；AI 協助分析。
   - 產生條件、假設、關係、推論與結論。
   - 可用來重新分析、調整條件及追溯結論依據。

8. **Creation — 創作型**
   - Human 是創作發起者與方向控制者；AI 是共同創作者或產出者。
   - 產生概念、結構、草稿、替代版本與內容選擇。
   - 可用來延續創作、重用素材及追溯作品形成過程。

### C. AI 評估或挑戰 Human

9. **Critique — 評論型**
   - Human 提出觀點或作品；AI 擔任評論者。
   - 產生評價標準、優缺點、立場與閱讀反應。
   - 可用來比較評論、調整定位與改善表達。

10. **Review — 審查型**
    - Human 提交內容並決定如何修正；AI 依標準審查。
    - 產生問題、缺漏、違反標準之處與修正要求。
    - 可用來追蹤問題、再次審查及保存品質紀錄。

11. **Dialectic — 辯證型**
    - Human 是主張者或質疑者；AI 是反方或挑戰者。
    - 產生反例、反駁、主張弱點、成立條件與修正。
    - 可用來強化論證、保存觀點改變與找回修改理由。

### D. AI 協助 Human 回看自己

12. **Reflection — 反思型**
    - Human 回顧經驗與思想；AI 擔任反思夥伴。
    - 產生認知變化、錯誤理解、決策原因與經驗教訓。
    - 可用於個人回顧、比較前後觀點與改善未來判斷。

### 必須說明的交疊關係

- 十二種類型不是互斥標籤。
- 發問可能存在於所有類型，但發問型以取得特定答案為主要關係。
- 驗證、編修、整理與模擬可以跨越多種對話形態，較適合作為第二層活動標記。
- 一段創作對話可能依序經過探索、討論、分析、創作、評論、辯證、審查與反思。
- 同一個 Topic 可以跨越多個 session，並在不同互動形態中持續發展。

### 與 Topic Chat Recorder 的連接

- 對話形態協助使用者判斷哪些內容值得保存。
- Topic Chat Recorder 保存選定的 user／assistant 對話與基本 metadata。
- 使用者再依內容性質交給 Obsidian、NotebookLM、Zotero、文件、試算表、Issue Tracker 或 Git 處理。
- 十二種形態不是產品內建的自動分類功能。
- 記錄不會自動驗證答案、證明 authorship 或形成不可竄改證據。

### 收尾主張

> The value of an AI conversation depends not only on what was said, but on what Human and AI were doing together.

> Record the interaction so its questions, reasoning, decisions, and unfinished work can be reused after the chat ends.

## L_CRR_A_02 — Decide the Conversation Before AI Decides the Direction

### 核心問題

為什麼原本明確的 AI 任務，經過幾輪後會變成另一場對話，甚至產出與原目的無關的內容？

### 專業情境

- 原本只想查證一個事實，最後變成產品策略討論。
- 原本要求審查文件，AI 卻開始重寫整份內容。
- 原本需要分析選項，幾輪後開始無限制探索新方向。
- AI 的延伸可能有價值，但 Human 沒有明確決定是否改變任務。

### 核心框架

對話開始前先定義：

1. **Topic**：這次處理什麼？
2. **Mode**：十二種形態中的哪一種？
3. **Purpose**：為什麼需要這段對話？
4. **Output**：最後要得到什麼 artifact 或 decision？
5. **Boundary**：哪些延伸不在本次範圍？
6. **Stop condition**：何時應該收斂、停止或另開 Topic？

### 關鍵 distinction

- 漂移不是所有延伸都不好，而是目的已改變卻沒有被明確決定。
- Exploration 可以有意發散；Review 則應受到標準與範圍限制。
- 模式可以切換，但切換應由 Human 確認。
- AI 可以提出新方向；Human 應決定繼續、放入 backlog 或另開 Topic。

### 可直接採用的 checkpoint

```text
Are we still discussing the same topic?
Are we still using the same conversation mode?
Does this direction support the original purpose?
Should this become a separate topic?
```

### 與產品的連接

Topic Chat Recorder 可以保存對話如何發展，讓使用者事後看見目的與形態何時改變；但 Recorder 不會自動控制對話方向。保持 Topic 和目的仍是 Human 的責任。

### 收尾主張

> Before asking AI what to do, decide what kind of conversation you want to have—and what must still be true when it ends.

## L_CRR_P_01_01 — A Conversation Can End Before Its Topic Does

- 現實 Hook：記得曾與 AI 討論重要決定，卻找不到在哪一個 chat。
- 工作情境：使用者關閉 chat，幾天後仍需要繼續其中一個問題；同一 Topic 也可能分散在多個 session。
- 核心 distinction：Chat completion ≠ Topic completion。
- 同時說明：Session 是平台容器；Topic 是使用者的工作單位。
- 目的：建立系列問題意識，並說明 topic-based recording 與一般 history 的差異。
- 不宣稱：產品具備搜尋 UI 或自動分類。
- 結尾提問：讀者如何在原始 chat 結束後找回並延續有價值的工作？

## L_CRR_P_02_01 — The Same AI Sentence Can Have Five Different Meanings

- 以「這個方案有三項風險」為例。
- 分別作為學習、分析、建議、審查及查證線索。
- 目的：引出 Human–AI 角色決定內容意義。
- 延伸：AI conversations 不只是 Q&A；不同互動會產生 FAQ、學習筆記、決策紀錄、Issue 或 retrospective。
- 導向：記錄需要保留關係與脈絡，不只是文字。
- 結尾提問：團隊如何避免 AI 建議在再利用時失去原始脈絡？

## L_CRR_P_03_01 — Not Every AI Chat Is Worth Saving

- 列出值得記錄的判斷條件。
- 使用一次性翻譯與跨 session 決策作對比。
- 目的：避免產品被理解成無差別備份工具。
- 核心句：Record for future use, not for accumulation.
- 同時說明：長 transcript 可能增加查找和理解成本；完整匯出與局部 capture 各有適用情況。
- 方法：先定義 Topic、Purpose、Expected output、Boundary 與 Stop condition。
- 結尾提問：讀者如何判斷哪些 AI conversations 應保存，以及有效範圍在哪裡？

## L_CRR_P_04_01 — A Chat Export Is Not Yet a Knowledge Base

- 對比 Record、Organize、Verify、Reuse。
- Topic Chat Recorder 是上游記錄層，不取代 Obsidian 或 NotebookLM。
- 目的：說明產品邊界並建立可信度。
- 核心句：Portable input is valuable because it can leave the original chat tool.
- 同時說明：AI answers 是 research material，不是 verified sources；Zotero 保存外部來源，Topic record 保存查詢原因與使用過程。
- 目的：建立 knowledge-base 與 research provenance 的正確邊界。
- 避免：把 AI citation 當作事實查證完成。
- 結尾提問：團隊如何防止合理但未驗證的 AI 回答變成「已驗證知識」？

## L_CRR_P_05_01 — Do Not Lose the Reasoning Behind a Decision

- 只保存結論會失去條件、替代方案與取捨。
- 對話記錄可轉成 decision matrix 或 ADR。
- 目的：連接分析型、建議型對話與專業決策。
- 延伸：最終文章同樣看不出哪些構想被提出、拒絕或修正；對話記錄可作為改版與跨平台改寫素材。
- 目的：同時連接專業決策，以及創作、評論、辯證和編修。
- 邊界：記錄形成過程不等於證明法律上的 authorship。
- 結尾提問：團隊如何保存決策與草稿背後的 reasoning，而不只保存結果？

## L_CRR_P_06_01 — Record → Select → Verify → Organize → Transform → Trace

- 提出六步驟再利用流程。
- 每一步只解決一個問題，不把所有能力宣稱為 Recorder 內建。
- 使用 CRR 實際案例呈現 Topic 如何從分類討論轉換成產品說明與跨平台文章系列。
- 目的：給讀者可直接採用的操作框架，並以真實產出呈現再利用價值。
- 可搭配單張流程圖。
- 結尾提問：讀者使用什麼流程，將 AI transcript 轉換成團隊可以信任並再利用的成果？

---

# X — 2 Articles + 36 Short Posts

X 以 2 篇長篇 Articles 建立完整觀點，再用 36 篇可獨立閱讀、可直接回應的短 Posts 拆解不同切角。短 Posts 每三篇為一個觀點群，但不要求讀者按順序閱讀，也不使用「Part 1／Part 2」作為理解前提。

## X_CRR_A_01 — Twelve Ways Humans and AI Develop a Conversation

### 文章目的

在一篇 X Article 中完整介紹十二種 Human–AI 對話形態，讓後續短 Posts 有可引用的分類入口。

### 結構

1. 為什麼 AI conversation 不只是 Q&A。
2. 分類基礎：Human 角色、AI 角色、互動關係與內容地位。
3. Human 從 AI 取得內容：Inquiry、Learning、Advisory、Assistance。
4. Human 與 AI 共同發展：Discussion、Exploration、Analysis、Creation。
5. AI 評估或挑戰 Human：Critique、Review、Dialectic。
6. AI 協助 Human 回看自己：Reflection。
7. Verification、Revision、Organization、Simulation 作為跨類型活動。
8. 同一段 Chat 如何在多種形態之間轉換。
9. 每種形態產生的內容及再利用方向。
10. Topic Chat Recorder 保存對話，但不會自動分類或驗證內容。

### 呈現方式

- 比 LinkedIn Article 更直接、更短段落。
- 使用一張十二種類型分組圖或表格。
- 每種類型用「角色 → 內容 → 再利用」三個元素說明。
- 文章本身完整成立，不要求先閱讀 Medium。

### 核心主張

> The same AI output can mean different things because Human and AI were doing different things together.

## X_CRR_A_02 — Choose the Conversation Before It Drifts

### 核心問題

在開始與 AI 對話前，如何先定義目的，避免幾輪之後被有趣但無關的延伸帶離原本 Topic？

### 結構

1. 以常見漂移案例開場：從查詢變策略、從 Review 變 Rewrite、從 Analysis 變無限制 Exploration。
2. 說明漂移的問題不是 AI 提出新方向，而是 Human 沒有明確決定是否切換目的。
3. 提出對話前定義卡：Topic、Mode、Purpose、Output、Boundary、Stop condition。
4. 說明十二種形態需要不同提示與邊界。
5. 提供每隔幾輪可使用的 alignment checkpoint。
6. 區分有意 Exploration 與無意 Drift。
7. 新方向的三種處理：繼續、放入 backlog、另開 Topic。
8. 說明 Topic Chat Recorder 可以保存漂移過程，但不能代替 Human 維持目的。

### 可引用檢查表

```text
What topic am I working on?
What kind of conversation do I need?
What output should exist at the end?
What is outside this conversation?
When should I stop or open a new topic?
```

### 核心主張

> Do not enter an AI conversation with only a prompt. Enter it with a purpose, a mode, and a boundary.

## Group 01 — Conversation vs Topic

### X_CRR_P_01_01 — Chat Ended, Topic Did Not

- 對話結束與 Topic 完成不是同一件事。
- 以未完成問題作為回應入口。

### X_CRR_P_01_02 — Session Is a Container

- Session belongs to the platform; Topic belongs to the work。
- 強調以日期找 chat 的限制。

### X_CRR_P_01_03 — Three States in One Chat

- 同一段 chat 可同時包含已完成、未完成與剛出現的 Topic。
- 問讀者目前如何處理三種狀態。

## Group 02 — Meaning Comes from Interaction

### X_CRR_P_02_01 — Same Sentence, Different Meaning

- 同一句風險描述可分別是答案、建議、分析或審查問題。

### X_CRR_P_02_02 — An Answer Is Not Always an Answer

- AI 內容也可能只是 hypothesis、option 或 verification lead。

### X_CRR_P_02_03 — Record the Role, Not Only the Words

- 文字必須連同 Human／AI 當時的角色才能正確再利用。

## Group 03 — Questions, Learning, Advice, Assistance

### X_CRR_P_03_01 — Inquiry vs Learning

- 找到一個答案，不等於建立理解。

### X_CRR_P_03_02 — Advice Needs Conditions

- 沒有條件與取捨理由的建議，未來很難重新評估。

### X_CRR_P_03_03 — Research Assistance Is Supporting Work

- 查詢與驗證是支援主要任務，不應被誤認為最終成果。

## Group 04 — Discussion, Exploration, Analysis, Creation

### X_CRR_P_04_01 — Discussion Starts with a Topic

- 討論發展觀點；探索可能連問題都還沒定義。

### X_CRR_P_04_02 — Do Not Save Only the Conclusion

- 分析的價值包含條件、假設與推論路徑。

### X_CRR_P_04_03 — Creation Leaves Reusable Fragments

- 被拒絕的名稱、結構與例子仍可能成為未來素材。

## Group 05 — Critique, Review, Dialectic, Reflection

### X_CRR_P_05_01 — Critique Is Not Review

- Critique 提供評價；Review 對照標準找問題。

### X_CRR_P_05_02 — Debate Changes the Claim

- 辯證的價值不只是反方意見，而是主張被修正的過程。

### X_CRR_P_05_03 — Reflection Records Human Change

- 反思記錄的不是 AI 知道什麼，而是 Human 如何改變理解。

## Group 06 — What Is Worth Recording?

### X_CRR_P_06_01 — Record High-Reconstruction-Cost Context

- 如果背景重新解釋成本高，就值得記錄。

### X_CRR_P_06_02 — One Translation Does Not Need a Topic

- 以一次性工作反襯 selective recording。

### X_CRR_P_06_03 — Record Future Use, Not Past Volume

- 記錄判斷應由未來用途決定，不由 chat 長度決定。

## Group 07 — Topic Boundary

### X_CRR_P_07_01 — A Topic Is Not a Session ID

- Topic name 應描述持續問題，而不是技術識別碼。

### X_CRR_P_07_02 — Full Export or Focused Capture?

- 整段屬於同一 Topic 才完整匯出；否則記錄局部範圍。

### X_CRR_P_07_03 — Long Transcript Can Reduce Reuse

- 保存更多內容可能增加重新理解成本。

## Group 08 — Obsidian and NotebookLM

### X_CRR_P_08_01 — Markdown Is the Handoff Format

- 可攜 Markdown 讓內容離開原始 chat tool。

### X_CRR_P_08_02 — Obsidian Organizes; Recorder Captures

- 清楚區分 capture 與 long-term knowledge organization。

### X_CRR_P_08_03 — NotebookLM Reuses Sources

- 對多份 Topic records 重新提問，但仍需查證來源內容。

## Group 09 — Research and Verification

### X_CRR_P_09_01 — AI Citation Is Not Verification

- 引用可協助定位，不會自動使主張正確。

### X_CRR_P_09_02 — Zotero and Topic Records Solve Different Problems

- Zotero 管來源；Topic record 管查詢與判斷脈絡。

### X_CRR_P_09_03 — Preserve What Is Still Unverified

- 未確認項目本身是重要的研究狀態。

## Group 10 — Decisions and Work

### X_CRR_P_10_01 — Decision Without Reasoning Is Hard to Revisit

- 保存選擇但未保存取捨，未來只能猜測。

### X_CRR_P_10_02 — Conversation Is Not an Issue Tracker

- 原始脈絡留在 Topic record；行動項目進 Issue Tracker。

### X_CRR_P_10_03 — Link the Record to the Change

- 將對話記錄與 document、ADR、Issue 或 commit 建立參照。

## Group 11 — Creation and Authorship Boundaries

### X_CRR_P_11_01 — Final Draft Hides Rejected Paths

- 最終版本看不出哪些替代方向曾被考慮。

### X_CRR_P_11_02 — Process Record Is Not Authorship Proof

- 記錄可呈現過程，不等於證明 originality 或法律權利。

### X_CRR_P_11_03 — Reuse the Material, Not the Entire Transcript

- 從記錄選取素材並轉換，不是原文全部搬到新成果。

## Group 12 — End-to-End Reuse

### X_CRR_P_12_01 — Six Steps After Recording

- Record → Select → Verify → Organize → Transform → Trace。

### X_CRR_P_12_02 — Recorder Is the Upstream Layer

- Recorder 保存；其他工具整理、查證與產出。

### X_CRR_P_12_03 — This Series Came from One Recorded Topic

- 以 CRR 系列本身作為 conversation reuse 的實際證據。

---

# 平台寫作原則

## Medium

- 每篇建立一個完整 argument，不將多篇 LinkedIn Post 串接後當成 Medium。
- 使用 1 篇完整 Story 說明如何在對話前選擇形態、目的、產出與邊界。
- 必須包含具體案例、機制、限制與讀者可採用的方法。
- 需要完整說明時使用小標題；避免把文章寫成產品功能清單。
- Capafy CTA 只放在讀者已理解問題與方法之後。

## LinkedIn

- 使用 1 篇 Article 完整說明十二種對話形態，再用 1 篇 Article 說明對話前如何選擇形態並防止無意漂移；其餘內容使用獨立 Posts。
- Articles 建立完整分類與方法，但不承擔所有產品操作與工具教學。
- 一篇只建立一個主要觀點。
- 開頭直接進入專業工作情境，不用 generic AI hook。
- Post 本身先提供完整價值；外部連結只是補充。
- 以具體 trade-off、案例或診斷問題結尾，不使用空泛的 “Thoughts?”。

## X

- 使用 1 篇 Article 介紹十二種對話形態，再用 1 篇 Article 說明如何先定義目的、模式與邊界。
- 優先使用獨立短 Post，不要求讀者看過前文。
- 每篇只處理一個 distinction、反例、問題或邊界。
- 延續 BRA／EBG 的做法：同一個核心觀點拆成多個可獨立回應的切角。
- 不重複近似文案；每篇必須增加新資訊。
- 可以引用先前 Post 回應，但 Reply 本身也必須提供實質觀點。
- 一般 Post 以 280 characters 為目標上限；發佈前實際量測。

# 系列成功判斷

本系列不是以「完整列出十二種分類」作為成功，而是讓讀者依序理解：

1. 自己確實有找不到、接不上或用不了的 AI 對話。
2. 不同 Human–AI 互動產生不同價值的內容。
3. 不是所有 Chat 都要記錄，但某些 Topic 值得跨 session 保存。
4. Markdown 記錄可以交給既有工具再利用。
5. Topic Chat Recorder 減少的是擷取與保留脈絡的人工成本。
6. Recorder 保存過程，但不誇大為正確性、原創性或不可竄改證明。
7. 與 AI 對話前先選擇形態、目的、預期產出與邊界，並在需要切換模式時由 Human 明確決定。
