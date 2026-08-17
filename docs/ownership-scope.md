# 接手責任與探索範圍

這份附錄回答：哪些事情可以探索、哪些沿用現況優化、哪些需要新建。

## Decision Boundary

```mermaid
flowchart LR
    I["IN SCOPE"] --> I1["理解並整理既有 repo"]
    I --> I2["改善內容與模板系統"]
    I --> I3["建立醫師自助後台"]
    I --> I4["探索 Chat / Google Sites-like 體驗"]

    O["OUT OF SCOPE"] --> O1["商業模式與定價"]
    O --> O2["醫師付費意願"]
    O --> O3["曝光或病患成效"]
    O --> O4["擴展到其他專業人士"]
```

## Explore

```mermaid
flowchart LR
    E["EXPLORE"] --> E1["Chat-first / Visual-first / Hybrid"]
    E --> E2["常見修改內容"]
    E2 --> E21["門診時間"]
    E2 --> E22["主圖與形象照"]
    E2 --> E23["專長、經歷、衛教文章"]
    E2 --> E24["區塊順序"]

    E --> E3["版面自由度"]
    E3 --> E31["Theme"]
    E3 --> E32["Section 順序"]
    E3 --> E33["Layout / component variant"]

    E --> E4["專科視覺語言"]
    E --> E5["Facebook 同步方式"]
    E5 --> E51["公開頁抓取"]
    E5 --> E52["Meta 授權"]
    E5 --> E53["後台手動匯入"]
```

## Optimize

```mermaid
flowchart LR
    O["OPTIMIZE"] --> O1["資料清洗與欄位分類"]
    O --> O2["Profile schema"]
    O --> O3["來源與人工查核標記"]
    O --> O4["貼文與圖片配對"]
    O --> O5["專科內容與視覺規則"]
    O --> O6["B2 / C2 模板元件化"]
    O --> O7["手機與無障礙體驗"]
    O --> O8["錯誤處理、測試、QA"]
    O --> O9["部署與效能"]
```

浮動 IP、VPN 或代理池只是 Facebook 抓取的候選方案之一，不預設為答案。需要與 Meta API、使用者授權及手動匯入比較穩定性、維護成本與平台規範。

## Create

```mermaid
flowchart LR
    C["CREATE"] --> A["Authentication"]
    A --> A1["醫師登入"]
    A --> A2["管理者 / 醫師權限"]

    C --> S["Site Project Model"]
    S --> S1["獨立 site_id"]
    S --> S2["獨立資料、素材、網址"]

    C --> W["Website CMS"]
    W --> W1["文字與圖片修改"]
    W --> W2["區塊開關與排序"]
    W --> W3["Theme / layout"]

    C --> P["Publishing Workflow"]
    P --> P1["Draft / preview / publish"]
    P --> P2["Version rollback"]

    C --> AI["AI Editing Layer"]
    AI --> AI1["理解自然語言"]
    AI --> AI2["轉成結構化修改"]
    AI --> AI3["驗證欄位並確認發布"]
```

## 目標架構候選

```mermaid
flowchart TD
    A["Doctor Dashboard"] --> B["Chat Editing<br/>主圖換成這張"]
    A --> C["Visual Editing<br/>點選 / 拖曳 / 排序"]
    B --> D["Structured Change Request"]
    C --> D
    D --> E["Validation / Permission"]
    E --> F["Site Project + Profile Schema"]
    F --> G["Content"]
    F --> H["Layout"]
    F --> I["Assets"]
    G --> J["Draft Renderer"]
    H --> J
    I --> J
    J --> K["Preview / Confirm"]
    K --> L["Versioned Publish"]
```

```mermaid
flowchart LR
    A["AI"] --> A1["理解醫師想改什麼"]
    S["Deterministic System"] --> S1["驗證修改是否合法"]
    S --> S2["修改結構化資料"]
    S --> S3["產生可預期的網站"]
    S --> S4["保存版本"]
    H["Human"] --> H1["預覽並確認發布"]
```

不讓 AI 直接任意重寫整份 HTML，才能保留穩定性、版本控制與可復原性。

## 尚待決定

```mermaid
flowchart LR
    O["OPEN"] --> O1["Chat-first / Visual-first / Hybrid"]
    O --> O2["允許修改的欄位與版面"]
    O --> O3["Preview / publish 規則"]
    O --> O4["網址與網域策略"]
    O --> O5["是否保留靜態 HTML"]
    O --> O6["Profile / site project 儲存方式"]
    O --> O7["Facebook 同步或首次匯入"]
    O --> O8["醫療內容人工確認範圍"]
```
