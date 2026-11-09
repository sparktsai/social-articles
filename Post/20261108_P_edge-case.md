# 邊界測試

## Hook

你會指定 AI 產生 Egde Case 的 Unit Test 以解決 Latent Defect 的問題嗎 ?

## Description

有一種 Bug，常在系統運行了幾年後才發現
他發生的原因是
- 數值過大：隨時間累積而觸發
- 判斷值不存在：隨業務或資料演變而觸發
- 上線時測不出來
  - 測試資料量小
  - 開發時假設「值域是封閉的」
  - 負向測試通常被視為次要而被省略

在人工撰寫程式時代，我們常會
- 在原始碼加入一堆 Exception
  - 例外情形特殊處理
  - 非預期的值進行記錄，跳過處理
- 在單元測試的測試程式
  - Execption Path Testing / Error Path Testing
  - Negative Testing / Robustness Testing

後來 自動化單元測試
- 人工 Review
- 人工 加 Unit test

現在 AI
- 測試主要是 End-to-End，以期能完成 Acceptance Criteria
- 單元測試幾乎沒有，除非使用 Skill
- PR Review，原始碼都看來不及了，測試程式更不會有人 Review

## Question

我曾寫了一個 Robustness Testing Skill 來讓 AI 產生 Edge Case Unit Test，
且可以執行測試後產生 Test Report
然後我只需 5 秒看完 Test Report

你呢 ？
當 AI GenCode 後
會注意到 Edge Case 嗎
會產生 Robustness Testing 嗎
還是有其他解決方案
還是現在已經為日後的 AI GenCode 埋下了 Bug Cost