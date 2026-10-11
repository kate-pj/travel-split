# travel-split
# ✈️ 旅行分賬 travel-split

兩個人旅行時嘅分賬 App。單一 HTML 檔案，用 Google Sheet 做後端，最後以港幣結算。

**線上版**：https://kate-pj.github.io/travel-split/

---

## 功能

- **記低支出** — 項目、類別（🍜 食 / 🚌 交通 / 🏨 住宿 / 📦 其他）、付款人、金額、消費日期
- **多幣種** — 57 種當地貨幣可揀，匯率自動上網抓取，亦可以手動覆蓋
- **即時結算** — 總支出、各人已付、應付份額、類別分佈，計到邊個要俾邊個幾多錢
- **FPS 收款碼** — 撳掣產生收款人嘅轉數快 QR，金額已經寫入（⚠️ 見下面嘅限制）
- **兩部手機同步** — 經 Google Apps Script 寫入同一個 Google Sheet，每 10 秒同步
- **離線都用得** — QR library 已經 inline，唔靠 CDN

---

## 技術

| | |
|---|---|
| 前端 | 單一 `index.html`，原生 JavaScript，冇 build step |
| 後端 | Google Apps Script Web App + Google Sheet |
| 匯率 | [open.er-api.com](https://open.er-api.com)，後備用 jsDelivr 嘅 currency-api |
| QR | [qrcodejs 1.0.0](https://github.com/davidshimjs/qrcodejs)（MIT），已 inline 入 HTML |
| 寄存 | GitHub Pages |

本機行嘅話，任何靜態伺服器都得：

```bash
python -m http.server 8000
```

> 唔可以直接 `file://` 開，因為瀏覽器會擋住對外嘅 `fetch`。

---

## 安裝

### 1. 準備 Google Sheet

`Sheet1` 第一行做標題，第二行開始放資料：

| 欄 | 內容 |
|---|---|
| A | `id`（timestamp）|
| B | `desc` 項目 |
| C | `category` 類別 |
