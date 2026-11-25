# 建置流程（PIPELINE）

官網是純靜態站，由 Markdown 與 HTML 樣板編譯成 `_dist/`，部署在 Cloudflare Pages。這裡只寫流程與紀律，不含文章正文。

## 一、單一資料來源

所有「N 篇文章／N 個工具／N 個術語／N 個 URL／N 條缺口」都由建置時計算，寫進 `_dist/api/site_stats.json`。頁面文案與回歸測試都讀這個檔，避免同一數字在十幾個地方各寫一次、改一處漏九處。

## 二、順序不可顛倒

```
python3 _build/build_site.py     # 1. 編譯（輸出 site_stats、sitemap 計數、feed、llms、api）
python3 _build/make_cards.py     # 2. 產生證據邊界卡（chromium 無頭截圖）
python3 _build/build_site.py     # 3. 再編譯一次，把新卡片索引進產物
node _qa/静态站回归测试.js        # 4. 站點回歸（讀 _dist/api/site_stats.json）
node _qa/工具页回归测试.js        # 5. 工具頁回歸
```

第 3 步漏掉的話，線上不會報錯，但卡片牆會少卡——這是這一套流程最容易靜默失敗的地方。

## 三、驗收紀律

- **核驗抓取必須帶 `Accept-Encoding: identity`**。否則 gzip 被截斷，會出現假 200 或空結果。
- **內鏈一律從 front-matter 的 slug 取**，不憑記憶寫路徑。
- **新增靜態頁要同步「靜態頁共 N 個」的斷言**，否則回歸會用計數把你擋下來。
- **缺口條目的分類詞會影響統計**（例如「實測」二字會讓該條進入「缺實測」統計），改文案前先看斷言。

## 四、收錄推送紀律

- IndexNow 只在 URL 實際變更時推單條；全量只在首次首發時跑一次。
- sitemap 由 build 依實際文章與工具頁計數，`<loc>` 數量與 `site_stats.urls` 必須相等。
- 搜尋引擎端的 sitemap 提交走 Search Console 手動，不做自動 ping（ping 端點已停用）。

## 五、不做的事

不做偽造社交信號、不做蜘蛛／訪客分流（cloaking）、不做指紋偽裝、不做偽原創流水線。這四項在技術上可行，但會把整個站的「可引用性」變成負資產。
