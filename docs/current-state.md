# 現況技術盤點

這份附錄回答：交接 repo 現在怎麼運作、已完成什麼、主要限制在哪裡。

## 執行流程

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

抓取失敗時，系統改為顯示預先生成的網站，確保 Demo 不會中斷。

## 已完成能力

```text
CONFIRMED
├─ 可輸入 Facebook 公開粉專 URL
├─ 可抓姓名、大頭照、簡介與部分公開貼文
├─ 可轉成共用 profile.json
├─ 可產生 B2 / C2 兩種靜態網站
├─ 有 Web UI 與生成進度
├─ 有抓取失敗 fallback
├─ 已用 Docker 部署至 Google Cloud Run
├─ 有基本 RWD 與動畫降級
└─ 有醫療免責聲明及 Facebook / 掛號連結
```

目前主要是確定性自動化：

```text
結構化資料 + 固定模板 -> HTML
```

runtime 沒有 LLM 動態理解醫師特色、設計網站或執行自然語言修改。

## 已知限制

```text
CONTENT
├─ Facebook 長簡介可能被錯放到職稱或學經歷
├─ 貼文可能混入播放器與介面文字
├─ 圖片與貼文配對可能錯誤
└─ 缺少完整來源與人工查核狀態

DESIGN
├─ B2 / C2 是固定版型
├─ 專科不一定會改變視覺母題
└─ 泌尿科網站仍可能出現骨科手骨圖案

PLATFORM
├─ 每次生成會覆寫共用 profile、assets 與固定網址
├─ 沒有每位醫師獨立 site / project
├─ 沒有登入、權限與所有權移交
├─ 沒有後台編輯器
├─ 沒有 draft / preview / publish / rollback
└─ 沒有正式自動化測試

DATA SOURCE
├─ Facebook 登入牆可能阻擋貼文
├─ Cloud Run datacenter IP 可能被封鎖
└─ 代理池、Meta API、使用者授權與手動匯入仍待比較
```

目前 `/sites/b2/index.html` 與 `/sites/c2/index.html` 代表最新一次生成結果，不是永久保存的個別醫師網站。

## 部署

```text
GitHub repo
    |
    v
Docker image
Node.js 20 + Chromium + Noto CJK
    |
    v
Google Artifact Registry
    |
    v
Google Cloud Run / asia-east1
```

## 現況來源

- <https://github.com/william-agent/professionalAiWebsite>
- <https://social2site-dev-557076811903.asia-east1.run.app/>
- 2026-08-17 高銘鴻醫師 B2 / C2 試跑結果
