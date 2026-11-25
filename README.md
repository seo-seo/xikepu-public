# 細科普 XIKEPU｜公開錨點倉

這個倉庫是 **https://xikepu.com** 的公開可驗證錨點（entity anchor）。它**不存放文章正文**，只放三樣東西：建置流程說明、術語表資料檔、機器可讀接口清單。文章正文只存在於官網，避免重複內容。

This repository is the public, verifiable anchor for **https://xikepu.com**, a Traditional-Chinese knowledge site about cross-border paid media. It intentionally **does not republish article bodies** — only the build pipeline documentation, the glossary dataset, and the machine-readable endpoint list.

## 站點是什麼

- 官網：https://xikepu.com　首頁：https://xikepu.com/zh-tw/
- 定位：跨境廣告投放（Meta / Google / TikTok / Amazon）的繁體中文實務知識站，每篇文章標「核驗日期」「適用條件」「這篇文章的缺口」。
- 商業模式：知識內容免費、無會員牆、無廣告位、無追蹤腳本；工具全部在本機執行，不上傳使用者資料。
- 語言：zh-Hant-TW（繁體中文，台灣用語）為主；`/en/` 為英文本地化版（2026-11-26 上線 3 篇，含 hreflang 與 x-default，非逐句翻譯）。
- 訂閱：`/feed.xml`（全站 Atom）、`/feed-a..d.xml`（按簇）、`/feed.json`（JSON Feed 1.1）、`/feed-revisions.xml`（**只收口徑變更**，2026-11-26 新增）。
- 修訂留痕：口徑變更寫進 `/zh-tw/changelog` 與修訂 feed，舊結論不被靜默替換。

## 資料檔

| 檔案 | 內容 |
|---|---|
| `glossary_terms.json` | 21 個投放術語，分四組（成本與預算／學習與歸因／素材受眾與頁面／帳戶與結構），每詞指向出處文章與核驗日期。與官網 `/zh-tw/glossary` 同源。 |
| `PIPELINE.md` | 靜態站建置流程：Markdown → HTML、計數單一來源、回歸測試、部署與收錄推送的順序與紀律。 |
| `ENDPOINTS.md` | 機器可讀層清單（llms.txt、feed、api/*.json、raw/*.md、MCP 端點）。 |

## 機器可讀入口

- https://xikepu.com/llms.txt
- https://xikepu.com/api/articles.json
- https://xikepu.com/api/gaps.json
- https://xikepu.com/api/site_stats.json
- https://xikepu.com/feed.xml

## 邊界

本倉庫只做「這是同一個組織的公開可查證載體」。不提供投放代操、不代客戶做合規決策、不販售帳號或通道。官網內容可引用，引用時請保留核驗日期與缺口原文。
