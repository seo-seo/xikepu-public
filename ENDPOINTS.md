# 機器可讀入口（ENDPOINTS）

| 路徑 | 格式 | 內容 | 更新方式 |
|---|---|---|---|
| `/llms.txt` | text/plain | 站點索引：術語數、文章清單、接口位置 | 每次建置 |
| `/llms-full.txt` | text/plain | 全部文章全文（給 AI 工具整批讀） | 每次建置 |
| `/feed.xml` | Atom | 全站文章訂閱 | 每次建置 |
| `/feed-a.xml` `/feed-b.xml` `/feed-c.xml` `/feed-d.xml` | Atom | 按主題簇（帳戶與故障／素材與結構／合規與紅線／錢與組織）拆分的子訂閱 | 每次建置 |
| `/feed.json` | JSON Feed 1.1 | 全站文章 | 每次建置 |
| `/api/articles.json` | JSON | 結構化索引：slug、標題、主題簇、人設、核驗日期、描述 | 每次建置 |
| `/api/gaps.json` | JSON | 每篇文章自己標的「不知道什麼」，每條帶編號與類型 | 每次建置 |
| `/api/cards.json` | JSON | 證據邊界卡索引（1080×1080 PNG 位址） | 每次建置 |
| `/api/site_stats.json` | JSON | 站級計數單一來源 | 每次建置 |
| `/raw/<slug>.md` | text/markdown | 單篇原文 | 每次建置 |
| `/mcp` | MCP | 讓使用者自己的 AI 工具查站點內容與工具計算 | 隨部署 |

契約：所有 JSON 的 `_meta.count` 必須等於 `site_stats.articles`；`api/gaps.json` 的缺口編號格式固定為 `G-<篇號>-<序號>`，引用時保留編號與核驗日期。

引用規則：可引用、可轉載，請保留核驗日期與「這篇文章的缺口」段落原文；不要把「一方稱」改寫成「已確認」。
