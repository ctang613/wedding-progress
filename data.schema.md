# `data.json` 欄位

UTF-8 JSON，放喺 repo 頂層。`index.html` 用相對路徑 `fetch('data.json')` 載入（GitHub Pages 同本機 `python3 -m http.server` 都得；`file://` 唔得）。

每日 Drive sync **只改呢個檔**：更新 `asOf`，同埋今次有變嘅欄位。唔好把整份資料抄返入 `index.html`。

進度百分比只計 `pre.checklist` 同 `day.checklist` 入面 `s` 係 `ok`／`half`／`no` 嘅項目。

## 私隱（公開站，有網址就睇到）

**永遠唔好**寫入 `data.json`，亦唔好出現喺公開網站任何位置：

- 護照姓名、機票／酒店 check-in 姓名
- 酒店 booking ID、確認號、房號
- 付款金額、訂金數字、收據、卡號
- 賓客姓名、電話、電郵、或其他聯絡

代替寫法：

- 金額、已付幾多、收據 → `見 Drive`（`budget`／`vendors` 嘅 `total`、`actual`、`paid` 保持 `0`）
- 酒店細節 → `待 SA 確認／見 Drive`（可以寫日期，唔好寫酒店名同訂單號）
- 賓客 → 只寫人數（`day.guests`），唔好寫名

已有嘅公開套餐字句（例如報名優惠「已選減 $2,500」）可以保留做選擇紀錄；唔好再加新嘅付款或收據金額。

## 狀態碼 `s`

| 碼 | 意思 | 計分 |
| --- | --- | --- |
| `ok` | 已完成／已確認 | 100 |
| `half` | 進行中／半鎖定／待確認 | 50 |
| `no` | 未開始／未決 | 0 |
| `tbd` | 純提醒，唔係待辦進度 | 唔計入百分比 |

每個有狀態嘅項目通常係：

| 欄 | 必須 | 意思 |
| --- | --- | --- |
| `t` | 是 | 標題 |
| `d` | 否 | 一行補充 |
| `s` | 是 | 上面嘅狀態碼 |
| `c` | 是 | 顆粒標籤上顯示嘅短字（例如「已確認」「未買」） |

## 頂層欄位

| 欄 | 形狀 | 點用 |
| --- | --- | --- |
| `asOf` | `"YYYY-MM-DD"` | 頁頂「資料更新至」。每次 sync 都要改。 |
| `dates` | `{label, date, place}[]` | 首頁兩張倒數卡。`date` 用 `YYYY-MM-DD`。 |
| `urgent` | `{t, d}[]` | 首頁緊急待辦，順序就係優先序。 |
| `budget` | `{total, actual, paid, note}` | 公開站唔顯示金額。三個數字保持 `0`，狀態寫喺 `note`。 |
| `vendors` | `{name, actual, paid, note}[]` | 供應商名＋一句狀態。`actual`／`paid` 保持 `0`。 |
| `pre` | object | Pre-wedding，見下。 |
| `day` | object | 結婚當日，見下。 |
| `lanes` | object[] | 進度看板。 |
| `notes` | 狀態項目[] | 注意事項。提醒可以用 `s: "tbd"`。 |
| `links` | `{t, u}[]` | 只放文件標題同 URL，唔好貼文件內容。 |
| `looks` | object[] | Look 目錄。換相檔要另開 code PR。 |

### `pre`

| 欄 | 形狀 |
| --- | --- |
| `info` | `[標籤, 內容]` 二維陣列，例如 `["拍攝日", "2026-10-15（已確認）"]` |
| `timeline` | `{when, t, s, c}[]` |
| `elements` | 字串陣列（拍攝元素） |
| `rejected` | 字串陣列（已拒絕） |
| `checklist` | 狀態項目[]（計入 Pre-wedding 進度） |

### `day`

| 欄 | 形狀 |
| --- | --- |
| `venue` | 同 `pre.info`，`[標籤, 內容][]` |
| `guests` | `{list, tbc, venue}` 三個整數（人數，唔好加名） |
| `flow` | 字串陣列（當日流程骨架） |
| `songs` | 狀態項目[] |
| `checklist` | 狀態項目[]（計入結婚當日進度） |

### `lanes[]`

| 欄 | 意思 |
| --- | --- |
| `k` | `red`／`yellow`／`green`／`after`（決定顏色） |
| `title` | 欄標題 |
| `desc` | 欄下嘅一行說明 |
| `items` | 字串陣列（呢度唔用狀態碼） |

### `looks[]`

| 欄 | 意思 |
| --- | --- |
| `id` | 穩定 id，例如 `look-01` |
| `file` | 放大圖，相對路徑 `looks/<id>.jpg` |
| `thumb` | 網格縮圖 `looks/<id>-thumb.jpg` |
| `title` | 短標題 |
| `tags` | `female`／`male`，再加女裝 `A` `B` `C` 或男裝 `1` `2` `3`。可多過一個。 |
| `note` | 可選。情侶相可寫「女＋男」。 |

篩選同燈箱邏輯喺 `index.html`，唔喺 JSON。改標題、tag、note 可以當資料更新；**加新相或者換檔**要連 `looks/` 圖片一齊用 code PR。
