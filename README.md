# professionalAiWebsite-map

`professionalAiWebsite` 的產品與技術 mental map。目標是快速回答三件事：產品想做什麼、交接 repo 做到哪裡、接手後由我負責什麼。

> 現況快照：2026-08-17。Demo、部署或生成成功不等於產品效果證明。

## Product Intent

```mermaid
flowchart TD
    A["專業人士想被看見<br/>但沒有時間學建站工具"] --> B["系統先從公開資料<br/>建立第一版網站"]
    B --> C["不需要從空白頁開始製作"]
    C --> D["醫師以低學習成本<br/>自行修改與發布"]
    D --> E["Chat editing + Visual editing"]
```

一句話：把「一次性自動建站 Demo」推進成「醫師可自行維護的 AI-assisted Website CMS」。

## 現有 Repo 做到哪裡

```mermaid
flowchart TD
    A["Facebook URL"] --> B["scrape.js<br/>公開資料與圖片抓取"]
    B --> C["build_profile.js<br/>規則分類與資料正規化"]
    C --> D["profile.json + assets"]
    D --> E["generate.js"]
    E --> F["B2 固定模板"]
    E --> G["C2 固定模板"]
    F --> H["靜態 HTML / Cloud Run"]
    G --> H
```

```mermaid
flowchart LR
    C["CONFIRMED"] --> C1["Facebook URL 可生成網站"]
    C --> C2["B2 / C2 兩種模板"]
    C --> C3["Web UI、進度與失敗 fallback"]
    C --> C4["Docker / Google Cloud Run"]
    C --> C5["RWD、掛號連結、醫療免責"]

    L["CURRENT LIMITS"] --> L1["風格與資訊架構固定"]
    L --> L2["資料分類與專科視覺可能錯配"]
    L --> L3["生成會覆寫共用資料與網址"]
    L --> L4["沒有獨立 site、登入與後台"]
    L --> L5["沒有 draft / preview / publish / rollback"]
    L --> L6["runtime 沒有 LLM / Chat editing"]
```

詳細技術盤點：[docs/current-state.md](docs/current-state.md)

## 我的責任範圍

```mermaid
flowchart LR
    E["EXPLORE"] --> E1["Chat / Visual / Hybrid"]
    E --> E2["可修改的內容與版面"]
    E --> E3["模板自由度"]
    E --> E4["Facebook 匯入方式"]

    O["OPTIMIZE"] --> O1["資料清洗與 profile"]
    O --> O2["專科視覺規則"]
    O --> O3["模板元件化"]
    O --> O4["測試、QA、部署穩定性"]

    N["CREATE"] --> N1["醫師登入與權限"]
    N --> N2["每人獨立 site project"]
    N --> N3["Website CMS"]
    N --> N4["Preview / Publish / Rollback"]
    N --> N5["AI editing layer"]
```

本階段不處理商業模式、定價、付費意願或曝光成效。

詳細責任與候選架構：[docs/ownership-scope.md](docs/ownership-scope.md)

## 目標方向

```mermaid
flowchart TD
    A["Doctor Dashboard"] --> B["Chat Editing"]
    A --> C["Visual Editing"]
    B --> D["Structured Change Request"]
    C --> D
    D --> E["Validation / Permission"]
    E --> F["Site Project + Profile Schema"]
    F --> G["Draft"]
    G --> H["Preview"]
    H --> I["Publish"]
    I --> J["Versioned Website"]
```

```mermaid
flowchart LR
    A["AI"] --> A1["理解需求<br/>產生結構化修改"]
    S["System"] --> S1["驗證權限、修改資料<br/>生成網站、保存版本"]
    H["Human"] --> H1["預覽並確認發布"]
```

## 建議順序

```mermaid
flowchart TD
    P1["1. Site isolation<br/>獨立資料、素材與網址"] --> P2["2. Editable data<br/>Schema、表單、圖片、預覽發布"]
    P2 --> P3["3. Component system<br/>Section、theme、layout、專科規則"]
    P3 --> P4["4. AI-assisted editing<br/>Chat → structured changes → preview → publish"]
    P4 --> P5["5. Reliability<br/>權限、版本復原、測試與監控"]
```

## 來源

- 交接 repo：<https://github.com/william-agent/professionalAiWebsite>
- 線上 Demo：<https://social2site-dev-557076811903.asia-east1.run.app/>
- 交接簡報：`專業人士網站.pdf`
