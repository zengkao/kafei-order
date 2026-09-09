# 卡啡 2.0 測試站

網址：https://zengkao.github.io/kafei-order/v2/

**這個資料夾是測試用的，正式站在上一層。** 由 `build_v2_testsite.py` 產生，
不要手改裡面的 html——下次重跑就沒了。改內容請改 `build_order_page.py`
的 HTML_TEMPLATE（訂購頁）或 `deploy/` 根目錄的對應頁面，再重跑：

    python build_order_page.py --json
    python build_v2_testsite.py

## 測試站與正式站的差別

| 項目 | 正式站 | 測試站 |
|---|---|---|
| 商品資料 | 執行期向 Apps Script 抓 | 用頁面內嵌的 2.0 豆單，不抓後端 |
| 庫存輪詢 | 每 30 秒 | 停用 |
| 送出訂單 | 真的寫入訂單分頁 | 擋下並跳說明，不發請求 |
| 門市清單 | 向 Apps Script 抓 | 一樣抓（唯讀 GET，無副作用） |
| 搜尋引擎 | 收錄 | `noindex,nofollow`，且不在 sitemap 裡 |

商品與庫存之所以停用，是因為線上 Apps Script 目前仍是 1.0 版，
`?action=products` 回的是 1.0 的舊商品表，抓了會把 2.0 豆單蓋掉。

## 可以測什麼

畫面、文案、分類篩選、加購物車、優惠金額計算（滿 $800／滿 $1,400 的門檻與折扣
都在前端算，可以直接驗）、結帳表單驗證、訂單確認彈窗的計算明細。

## 測不到什麼

真的下單、真的扣庫存、VIP 擇優（VIP 只有後端算得出來）、發票開立、出貨通知信。
那些要等 2.0 Apps Script 貼上去、且正式站切換之後才能驗。
