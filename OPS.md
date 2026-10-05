# 每日進度更新（進度妹／wedding bots）

純資料更新：**改 `data.json` → commit 上 `main` → 完**。  
Live site 約 1 分鐘後自動更新。唔使去 GitHub Settings relaunch Pages，亦唔使為改資料再開一個 coding agent。

網址：https://ctang613.github.io/wedding-progress/  
欄位同私隱細節：`data.schema.md`

## Checklist

1. 對 Drive「婚禮總覽」Doc，同 Wedding Planning 表。數字以 Wedding Planning 為準。
2. 只改 repo 頂層 `data.json`：
   - `asOf` 改做今日（`YYYY-MM-DD`）
   - 只改今次有變嘅欄位
3. 私隱再睇一眼（公開站，有網址就睇到）：
   - 唔好寫護照／check-in 姓名、酒店 booking ID、付款金額、收據
   - 唔好寫賓客姓名或聯絡
   - 金額 → `見 Drive`
   - 酒店細節 → `待 SA 確認／見 Drive`
4. 狀態只用 `ok`／`half`／`no`（純提醒先用 `tbd`）。
5. Commit 並 push，或者 merge PR，去 **`main`**。
6. 等 Actions「Deploy GitHub Pages」成功（大約 1 分鐘）。
7. 開 live site 重新整理，對 `asOf` 同改過嘅句子。

## 唔使做

- Settings → Pages 手動 relaunch
- 為咗改 `data.json` 再開 coding agent

## 要開正常 code PR

- 改版面、CSS、JS（`index.html`）
- 加或換 Look 相片（`looks/`）
