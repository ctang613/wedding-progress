# Scott × Shin Tung 婚禮進度網站

手機優先、純靜態（單一 `index.html`，CSS／JS 內嵌），無 build step、無 framework。

## 頁面
1. **總覽** — 兩大日子（倒數）＋ 緊急待辦 3 條 ＋ 整體進度 ＋ 預算
2. **Pre-wedding** — 濟州拍攝（2026-10-15）
3. **結婚當日** — 2027-10-30，Green House
4. **進度看板** — 紅／黃／綠／事後
5. **注意事項** — 待決事項、提醒、相關文件連結

## 本機開啟
- 直接雙擊 `index.html`（file:// 可用），或
- `cd wedding-progress && python3 -m http.server 8000`，然後開 http://localhost:8000
  （手機同一 Wi-Fi 可開 `http://<電腦IP>:8000`）

## 更新資料
所有內容喺 `index.html` 入面 `const DATA = {...}`。改 status 即自動重算進度：
- `ok` = 已完成／已確認（100%）
- `half` = 進行中／半鎖定／待確認（50%）
- `no` = 未開始／未決（0%）

⚠️ 唔好加入任何賓客姓名或聯絡資料——網站可能經連結分享。

## 發佈到 GitHub Pages
**方法 A：`/docs` 資料夾**
1. 將本資料夾內容複製到 repo 嘅 `docs/`（包括 `.nojekyll`）
2. push 去 `main`
3. Repo → Settings → Pages → Source：Deploy from a branch → `main` / `/docs`

**方法 B：`gh-pages` branch**
```bash
cd wedding-progress
git init && git checkout -b gh-pages
git add . && git commit -m "Wedding progress site"
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin gh-pages
```
然後 Settings → Pages → Source：`gh-pages` / root。

網址會係 `https://<user>.github.io/<repo>/`。

> 注意：公開 repo 嘅 GitHub Pages 係任何人有網址都睇到（`noindex` 只係叫搜尋器唔好收錄）。
> 頁內嘅 Google Drive 連結（婚禮總覽 Doc、Wedding Planning 表、Pre-wedding 夾）需要對方本身有 Drive 權限先開到。

資料來源：「婚禮總覽」Doc ＋ Wedding Planning 表（數字以 Wedding Planning 為準），更新至 2026-10-05。
