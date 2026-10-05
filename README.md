# Scott × Shin Tung 婚禮進度網站

手機優先、純靜態。版面喺 `index.html`（CSS／JS 內嵌），**進度資料喺頂層 `data.json`**。頁面用 `fetch('data.json')` 載入，無 build step、無 framework。

Live：https://ctang613.github.io/wedding-progress/

## 頁面
1. **總覽** — 兩大日子（倒數）＋ 緊急待辦 ＋ 整體進度 ＋ 預算
2. **Pre-wedding** — 濟州拍攝（2026-10-15）
3. **結婚當日** — 2027-10-30，Green House
4. **進度看板** — 紅／黃／綠／事後
5. **注意事項** — 待決事項、提醒、相關文件連結
6. **Look・揀衫** — `#look`，參考相喺 `looks/`

## 本機開啟
`data.json` 要經 HTTP 先載入到，**唔好直接雙擊 `index.html`（`file://` 會載入失敗）**。

```bash
python3 -m http.server 8000
```

然後開 http://localhost:8000 （手機同一 Wi-Fi：`http://<電腦IP>:8000`）。

## 更新資料
每日進度只改 `data.json`（`asOf` ＋ 有變動嘅欄位）。欄位、狀態碼、私隱規則見 [`data.schema.md`](data.schema.md)。進度妹／bot 步驟見 [`OPS.md`](OPS.md)。

改 status 之後，頁面會自動重算進度：
- `ok` = 已完成／已確認（100%）
- `half` = 進行中／半鎖定／待確認（50%）
- `no` = 未開始／未決（0%）

⚠️ 唔好加入護照／入住姓名、酒店訂單號、付款金額、收據、賓客姓名或聯絡資料——網站係公開連結。

## 發佈（commit 到 `main` = 自動上線）

**Live site 嘅 source of truth 就係 `main`。**

1. Push，或者 merge PR，去 `main`
2. GitHub Actions workflow **Deploy GitHub Pages**（`.github/workflows/pages.yml`）會自動發佈，大約 1 分鐘
3. 開 https://ctang613.github.io/wedding-progress/ 重新整理，對一下頁頂日期

**唔使**去 Repo Settings → Pages 手動 relaunch。  
**唔使**為純資料更新再開一個 coding agent。

### 每日 Drive sync
1. 對 Drive「婚禮總覽」同 Wedding Planning（數字以 Wedding Planning 為準）
2. 只改 `data.json`：更新 `asOf`，同埋今次有變嘅欄位
3. Commit 上 `main`（直接 push，或者 PR merge 上去）
4. 等 Actions 綠燈——完成

改 UI、CSS／JS，或者換 Look 相片（`looks/`），先要開正常 code PR。

> 公開 repo 嘅 GitHub Pages 係任何人有網址都睇到（`noindex` 只係叫搜尋器唔好收錄）。  
> 頁內嘅 Google Drive 連結需要對方本身有 Drive 權限先開到。

資料來源：「婚禮總覽」Doc ＋ Wedding Planning 表（數字以 Wedding Planning 為準）。
