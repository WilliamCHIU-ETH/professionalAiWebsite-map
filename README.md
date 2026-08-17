# professionalAiWebsite-map

這個 repository 是 `professionalAiWebsite` 的產品與技術 mental map，用來快速對齊：

- 產品原始意圖
- 交接 repo 已做到哪裡
- 現況的技術邊界與已知問題
- 接手後可以探索、優化與新建的範圍

> 本文件描述的是截至 2026-08-17 的交接現況，不把 Demo、部署完成或網站生成數視為產品效果證明。

## 1. 本階段的決策邊界

```text
本階段要處理
├─ 理解並整理既有 repo
├─ 改善網站內容與模板系統
├─ 建立醫師可自行維護網站的後台
└─ 探索 Chat mode / Google Sites-like 的修改體驗

本階段不處理
├─ 商業模式與定價
├─ 醫師付費意願
├─ 網站是否增加曝光或病患
└─ 擴展到律師、會計師、政治人物
```

## 2. Product Intent

原始意圖不是再提供一套需要專業人士自己學習的建站工具，而是先替他完成網站，再讓他能以低負擔持續維護。

```text
專業人士想被看見
        |
        v
缺的不是建站工具，而是時間與執行能力
        |
        v
系統從公開資料建立第一版網站
        |
        v
專業人士不必從空白頁開始
        |
        v
後續能用低學習成本自行修改與發布
```

目前接手後的產品方向可簡化為：

```text
Initial Site Generation
第一次自動建站
        |
        v
Doctor Self-Service CMS
醫師自行維護
        |
        v
AI-assisted Editing
Chat 與視覺化修改
```

## 3. 交接 Repo 現況

來源 repo：[`william-agent/professionalAiWebsite`](https://github.com/william-agent/professionalAiWebsite)

線上 Demo：[`social2site-dev`](https://social2site-dev-557076811903.asia-east1.run.app/)

```text
使用者貼上 Facebook 粉專 URL
                |
                v
        Web UI + SSE 進度
                |
                v
       scrape.js 公開資料抓取
       ├─ OG metadata
       └─ Playwright 公開貼文
                |
                v
 scraped_profile.json + 圖片素材
                |
                v
       build_profile.js
       規則分類與資料正規化
                |
                v
       profile.json + assets
                |
                v
          generate.js
       ┌────────┴────────┐
       v                 v
 B2 Clinical Chart   C2 Quiet Luxe
       └────────┬────────┘
                v
          靜態 HTML 網站
                |
                v
     Docker container / Cloud Run
```

抓取失敗時的 Demo 保險絲：

```text
Facebook 封鎖 / 逾時 / 抓取失敗
                |
                v
    顯示預先生成的展示網站
                |
                v
        Demo 不會中斷
```

## 4. 已完成能力

```text
CONFIRMED
├─ 可輸入 Facebook 公開粉專 URL
├─ 可抓姓名、大頭照、簡介與部分公開貼文
├─ 可轉成共用的 profile.json
├─ 可產生 B2 / C2 兩種靜態網站
├─ 有 Web UI 與生成進度
├─ 有抓取失敗 fallback
├─ 已用 Docker 部署至 Google Cloud Run
├─ 有基本 RWD、動畫降級與醫療免責聲明
└─ 可連回 Facebook 或醫院掛號頁
```

目前網站不是由 runtime LLM 動態設計。主要流程是：

```text
結構化資料 + 固定模板 -> HTML
```

這仍然可以自動產生網站，但目前的 AI Agent 能力尚未出現在使用者執行階段。

## 5. 已知限制

```text
CURRENT LIMITS
├─ B2 / C2 是固定版型，主要只有資料被替換
├─ 專科不一定會改變視覺母題
│  └─ 泌尿科網站仍可能出現骨科手骨圖案
├─ Facebook 長簡介可能被錯放到職稱或學經歷
├─ 貼文可能混入播放器與介面文字
├─ Facebook 資料抓取受登入牆與 datacenter IP 影響
├─ 每次生成會覆寫共用 profile、assets 與固定網站網址
├─ 沒有每位醫師獨立的 site/project
├─ 沒有登入、權限與所有權移交
├─ 沒有後台編輯器
├─ 沒有 draft / preview / publish workflow
├─ 沒有版本紀錄與復原
├─ 沒有 runtime LLM / Chat editing
└─ 沒有正式自動化測試
```

目前兩個網址代表「最新一次生成結果」，不是兩個永久保存的醫師網站：

```text
/sites/b2/index.html
/sites/c2/index.html
```

## 6. 我可以探索的部分

探索代表還沒有拍板，先比較候選方案與使用方式。

```text
EXPLORE
├─ Chat-first 或 Google Sites-like
│  ├─ 純 Chat
│  ├─ 畫面直接編輯
│  └─ Chat + 視覺編輯混合
├─ 醫師最常修改哪些內容
│  ├─ 門診時間
│  ├─ 主圖與形象照
│  ├─ 專長與經歷
│  ├─ 衛教文章
│  └─ 區塊順序
├─ 版面自由度
│  ├─ 只換 theme
│  ├─ 可調 section 順序
│  └─ 可選 layout / component variant
├─ 專科如何影響版型與視覺語言
└─ Facebook 後續同步方式
   ├─ 公開頁抓取
   ├─ Meta 授權
   └─ 後台手動匯入
```

## 7. 我可以優化的部分

優化代表沿用現有能力，但讓結果更可靠、可維護。

```text
OPTIMIZE
├─ Facebook 資料清洗與欄位分類
├─ 醫師 profile schema
├─ 來源與人工查核標記
├─ 貼文文字與圖片配對
├─ 專科對應的內容與視覺規則
├─ B2 / C2 模板元件化
├─ 靜態網站的無障礙與手機體驗
├─ 生成流程錯誤處理
├─ 測試與 QA gate
└─ 部署與效能
```

Facebook 浮動 IP、VPN 或代理池是其中一種技術候選，但不預設為答案。它需要和 Meta API、使用者授權及手動匯入比較穩定性、維護成本與平台規範。

## 8. 我可以新建的部分

新建代表目前 repo 沒有、但醫師自行維護網站所必需的產品層。

```text
CREATE
├─ Authentication
│  ├─ 醫師登入
│  └─ 管理者 / 醫師權限
├─ Site Project Model
│  ├─ 每位醫師獨立 site_id
│  ├─ 獨立資料與素材
│  └─ 獨立網址
├─ Website CMS
│  ├─ 文字修改
│  ├─ 圖片上傳與替換
│  ├─ 區塊開關
│  ├─ 區塊排序
│  └─ theme / layout 設定
├─ Publishing Workflow
│  ├─ draft
│  ├─ preview
│  ├─ publish
│  └─ version rollback
└─ AI Editing Layer
   ├─ 理解自然語言需求
   ├─ 轉成結構化修改指令
   ├─ 驗證允許修改的欄位
   └─ 讓醫師確認後發布
```

## 9. 目標技術架構候選

```text
                         Doctor Dashboard
                                |
                ┌───────────────┴───────────────┐
                v                               v
          Chat Editing                  Visual Editing
       "主圖換成這張"                 點選 / 拖曳 / 排序
                |                               |
                └───────────────┬───────────────┘
                                v
                     Structured Change Request
                                |
                                v
                     Validation / Permission
                                |
                                v
                   Site Project + Profile Schema
                                |
                 ┌──────────────┼──────────────┐
                 v              v              v
              Content        Layout          Assets
                 └──────────────┼──────────────┘
                                v
                         Draft Renderer
                                |
                                v
                         Preview / Confirm
                                |
                                v
                        Versioned Publish
```

AI 與確定性系統的責任邊界：

```text
AI
└─ 理解醫師想改什麼

Deterministic System
├─ 驗證修改是否合法
├─ 修改結構化資料
├─ 產生可預期的網站
└─ 保存版本

Human
└─ 預覽並確認發布
```

不讓 AI 直接任意重寫整份 HTML，才能保留穩定性、版本控制與可復原性。

## 10. 建議推進順序

```text
Phase 1  Site Isolation
         每位醫師有獨立 project、資料、素材與網址
             |
             v
Phase 2  Editable Data
         建立 schema、表單修改、圖片上傳、預覽發布
             |
             v
Phase 3  Component System
         section、theme、layout 與專科視覺規則
             |
             v
Phase 4  AI-assisted Editing
         Chat -> structured changes -> preview -> publish
             |
             v
Phase 5  Reliability
         權限、版本復原、測試、監控與資料同步
```

## 11. 尚待決定

```text
OPEN
├─ 第一版後台採 Chat-first、Visual-first 或 Hybrid
├─ 哪些欄位與版面允許醫師修改
├─ 修改是即時生效，還是一定要 preview / publish
├─ 每位醫師網址與網域策略
├─ 是否保留靜態 HTML 生成模式
├─ profile 與 site project 使用何種儲存方式
├─ Facebook 採持續同步或只作首次匯入
└─ 哪些醫療內容必須人工確認才能發布
```

## 12. 來源

- 交接 repo：<https://github.com/william-agent/professionalAiWebsite>
- 線上 Demo：<https://social2site-dev-557076811903.asia-east1.run.app/>
- 交接簡報：`專業人士網站.pdf`
- 現況試跑案例：高銘鴻醫師 B2 / C2，2026-08-17 檢視
