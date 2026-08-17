# 現況技術盤點

這份附錄回答：交接 repo 現在怎麼運作、已完成什麼、主要限制在哪裡。

## 執行流程

```mermaid
flowchart TD
    A["Facebook 粉專 URL"] --> B["Web UI + SSE 進度"]
    B --> C["scrape.js"]
    C --> C1["OG metadata"]
    C --> C2["Playwright 公開貼文"]
    C1 --> D["scraped_profile.json + 圖片素材"]
    C2 --> D
    D --> E["build_profile.js<br/>規則分類與資料正規化"]
    E --> F["profile.json + assets"]
    F --> G["generate.js"]
    G --> H["B2 Clinical Chart"]
    G --> I["C2 Quiet Luxe"]
    H --> J["靜態 HTML 網站"]
    I --> J
    J --> K["Docker container / Cloud Run"]
```

抓取失敗時，系統改為顯示預先生成的網站，確保 Demo 不會中斷。

## 已完成能力

```mermaid
flowchart LR
    C["CONFIRMED"] --> C1["Facebook URL 輸入"]
    C --> C2["姓名、照片、簡介、部分貼文"]
    C --> C3["共用 profile.json"]
    C --> C4["B2 / C2 靜態網站"]
    C --> C5["Web UI、進度、失敗 fallback"]
    C --> C6["Docker / Google Cloud Run"]
    C --> C7["RWD、動畫降級、醫療免責、外部連結"]
```

目前主要是確定性自動化：

```mermaid
flowchart LR
    A["結構化資料"] --> C["固定模板"]
    C --> D["HTML"]
```

runtime 沒有 LLM 動態理解醫師特色、設計網站或執行自然語言修改。

## 已知限制

```mermaid
flowchart LR
    R["CURRENT LIMITS"] --> C["CONTENT"]
    C --> C1["長簡介可能錯放欄位"]
    C --> C2["貼文混入播放器與介面文字"]
    C --> C3["圖片與貼文可能錯配"]
    C --> C4["缺少來源與查核狀態"]

    R --> D["DESIGN"]
    D --> D1["B2 / C2 固定版型"]
    D --> D2["專科與視覺母題可能錯配"]

    R --> P["PLATFORM"]
    P --> P1["覆寫共用 profile、assets、網址"]
    P --> P2["沒有獨立 site / project"]
    P --> P3["沒有登入、後台與發布流程"]
    P --> P4["沒有版本復原與自動化測試"]

    R --> S["DATA SOURCE"]
    S --> S1["Facebook 登入牆"]
    S --> S2["datacenter IP 封鎖"]
    S --> S3["替代匯入方式待比較"]
```

目前 `/sites/b2/index.html` 與 `/sites/c2/index.html` 代表最新一次生成結果，不是永久保存的個別醫師網站。

## 部署

```mermaid
flowchart TD
    A["GitHub repo"] --> B["Docker image<br/>Node.js 20 + Chromium + Noto CJK"]
    B --> C["Google Artifact Registry"]
    C --> D["Google Cloud Run<br/>asia-east1"]
```

## 現況來源

- <https://github.com/william-agent/professionalAiWebsite>
- <https://social2site-dev-557076811903.asia-east1.run.app/>
- 2026-08-17 高銘鴻醫師 B2 / C2 試跑結果
