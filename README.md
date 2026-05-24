# Personal Accounting System

這是一套個人記帳軟體，目標是降低人工記帳成本，透過自動化方式蒐集日常消費紀錄，並完成交易分類與資料保存。

系統主要包含三個記帳來源：

1. Apple Pay 即時刷卡紀錄
2. 電子發票載具同步
3. 人工手動記帳

目前第一階段會先實作 Apple Pay Transaction 模組，後續再擴充載具同步與手動記帳功能。

---

## Project Goal

本專案希望建立一個可以自動化紀錄日常消費的記帳系統。

當使用者完成 Apple Pay 或刷卡交易後，系統可以即時接收交易資訊，判斷使用者與商家是否存在，並依照商家類型進行分類，最後儲存為一筆交易紀錄。

若商家尚未建立分類資料，系統會透過 AI 或分類服務協助辨識商家類型，並建立商家與分類的對應關係。

---

## Core Modules

### 1. Apple Pay Transaction Module

負責處理 Apple Pay 或刷卡通知所產生的交易紀錄。

主要流程：

1. 接收 Apple Pay transaction request
2. 檢查使用者是否存在
3. 檢查商家分類是否已存在
4. 若商家分類不存在，進行商家類型辨識
5. 建立或更新商家分類對應
6. 新增交易紀錄
7. 推送記帳成功訊息給使用者

---

### 2. Invoice Carrier Sync Module

尚未規劃完成。

未來預計用於同步電子發票載具資料，將發票消費紀錄匯入系統，補足未透過 Apple Pay 或刷卡通知取得的交易資料。

---

### 3. Manual Transaction Module

尚未規劃完成。

未來預計提供使用者手動新增、修改、刪除交易紀錄，適用於現金消費、轉帳、分帳或其他無法自動取得的支出。

---

## Current Architecture

目前 Apple Pay Transaction 模組規劃如下：

```text
Apple Pay / Transaction Trigger
        |
        v
RESTful API
        |
        v
Check User Availability
        |
        v
Check Merchant Type Availability
        |
        v
Identify Merchant Type
        |
        v
Insert Transaction Data
        |
        v
Push Message
