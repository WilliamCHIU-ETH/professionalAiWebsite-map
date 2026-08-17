# 接手責任與探索範圍

這份附錄回答：哪些事情可以探索、哪些沿用現況優化、哪些需要新建。

## Decision Boundary

```text
IN SCOPE
├─ 理解並整理既有 repo
├─ 改善網站內容與模板系統
├─ 建立醫師可自行維護網站的後台
└─ 探索 Chat mode / Google Sites-like 的修改體驗

OUT OF SCOPE
├─ 商業模式與定價
├─ 醫師付費意願
├─ 網站是否增加曝光或病患
└─ 擴展到其他專業人士
```

## Explore

```text
EXPLORE
├─ Chat-first / Visual-first / Hybrid
├─ 醫師最常修改的內容
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

## Optimize

```text
OPTIMIZE
├─ Facebook 資料清洗與欄位分類
├─ 醫師 profile schema
├─ 來源與人工查核標記
├─ 貼文文字與圖片配對
├─ 專科對應的內容與視覺規則
├─ B2 / C2 模板元件化
├─ 手機與無障礙體驗
├─ 生成流程錯誤處理
├─ 測試與 QA gate
└─ 部署與效能
```

浮動 IP、VPN 或代理池只是 Facebook 抓取的候選方案之一，不預設為答案。需要與 Meta API、使用者授權及手動匯入比較穩定性、維護成本與平台規範。

## Create

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
│  ├─ 區塊開關與排序
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

## 目標架構候選

```text
                         Doctor Dashboard
                                |
                +---------------+---------------+
                v                               v
          Chat Editing                  Visual Editing
       "主圖換成這張"                 點選 / 拖曳 / 排序
                |                               |
                +---------------+---------------+
                                v
                     Structured Change Request
                                |
                                v
                     Validation / Permission
                                |
                                v
                   Site Project + Profile Schema
                                |
                 +--------------+--------------+
                 v              v              v
              Content        Layout          Assets
                 +--------------+--------------+
                                v
                         Draft Renderer
                                |
                                v
                         Preview / Confirm
                                |
                                v
                        Versioned Publish
```

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

## 尚待決定

```text
OPEN
├─ 第一版後台採 Chat-first、Visual-first 或 Hybrid
├─ 哪些欄位與版面允許醫師修改
├─ 修改是否一定要 preview / publish
├─ 每位醫師網址與網域策略
├─ 是否保留靜態 HTML 生成模式
├─ profile 與 site project 的儲存方式
├─ Facebook 持續同步或只作首次匯入
└─ 哪些醫療內容必須人工確認才能發布
```
