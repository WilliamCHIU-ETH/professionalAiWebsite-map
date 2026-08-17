# professionalAiWebsite-map

`professionalAiWebsite` 的產品與技術 mental map。目標是快速回答三件事：產品想做什麼、交接 repo 做到哪裡、接手後由我負責什麼。

> 現況快照：2026-08-17。Demo、部署或生成成功不等於產品效果證明。

## Product Intent

```text
專業人士想被看見，但沒有時間學建站工具
                    |
                    v
       系統先從公開資料建立第一版網站
                    |
                    v
          不需要從空白頁開始製作
                    |
                    v
       醫師以低學習成本自行修改與發布
                    |
                    v
        Chat editing + Visual editing
```

一句話：把「一次性自動建站 Demo」推進成「醫師可自行維護的 AI-assisted Website CMS」。

## 現有 Repo 做到哪裡

```text
Facebook URL
     |
     v
scrape.js                   公開資料與圖片抓取
     |
     v
build_profile.js            規則分類與資料正規化
     |
     v
profile.json + assets
     |
     v
generate.js
     |
     +----------+----------+
     v                     v
B2 固定模板             C2 固定模板
     +----------+----------+
                |
                v
       靜態 HTML / Cloud Run
```

```text
CONFIRMED
├─ Facebook URL 可生成網站
├─ 有 B2 / C2 兩種模板
├─ 有 Web UI、進度與失敗 fallback
├─ 已用 Docker 部署至 Google Cloud Run
└─ 有基本 RWD、掛號連結與醫療免責聲明

CURRENT LIMITS
├─ 兩種風格與資訊架構固定
├─ 資料分類會出錯，專科與視覺母題可能不匹配
├─ 每次生成會覆寫共用資料與固定網址
├─ 沒有每位醫師獨立 site、登入與後台
├─ 沒有 draft / preview / publish / rollback
└─ runtime 沒有 LLM 或 Chat editing
```

詳細技術盤點：[docs/current-state.md](docs/current-state.md)

## 我的責任範圍

```text
EXPLORE                    OPTIMIZE                   CREATE
├─ Chat / Visual / Hybrid  ├─ 資料清洗與 profile      ├─ 醫師登入與權限
├─ 可修改的內容與版面      ├─ 專科對應的視覺規則      ├─ 每人獨立 site project
├─ 模板自由度              ├─ 模板元件化              ├─ Website CMS
└─ Facebook 匯入方式       └─ 測試、QA、部署穩定性    ├─ Preview / Publish
                                                      ├─ Version rollback
                                                      └─ AI editing layer
```

本階段不處理商業模式、定價、付費意願或曝光成效。

詳細責任與候選架構：[docs/ownership-scope.md](docs/ownership-scope.md)

## 目標方向

```text
                         Doctor Dashboard
                                |
                +---------------+---------------+
                v                               v
          Chat Editing                  Visual Editing
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
                                v
                    Draft -> Preview -> Publish
                                |
                                v
                       Versioned Website
```

```text
AI              理解醫師想改什麼，產生結構化修改
System          驗證權限、修改資料、生成網站、保存版本
Human           預覽並確認發布
```

## 建議順序

```text
1. Site isolation
   每位醫師有獨立資料、素材與網址
        |
2. Editable data
   Schema、表單修改、圖片上傳、預覽發布
        |
3. Component system
   Section、theme、layout、專科視覺規則
        |
4. AI-assisted editing
   Chat -> structured changes -> preview -> publish
        |
5. Reliability
   權限、版本復原、測試與監控
```

## 來源

- 交接 repo：<https://github.com/william-agent/professionalAiWebsite>
- 線上 Demo：<https://social2site-dev-557076811903.asia-east1.run.app/>
- 交接簡報：`專業人士網站.pdf`
