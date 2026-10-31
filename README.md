# 台股上市櫃 融資維持率排行

每個平日台灣時間 21:43，GitHub Actions 會從證交所、櫃買中心抓取全部個股的融資進出與股價，
推估每檔股票的融資平均成本與融資維持率，產生排行頁面並發布到 GitHub Pages (`docs/index.html`)。

報告網址：https://a12021994-netizen.github.io/margin-report/
（GitHub Pages 的發布來源要設成 `main` 分支的 `/docs` 資料夾）

- `margin_report.py`：抓資料、推估成本、輸出 HTML
- `margin_template.html`：頁面範本
- `.github/workflows/margin.yml`：每日排程（也可在 Actions 頁手動執行）

## 推估方法
- 維持率 = 收盤價 ÷ (融資平均成本 × 融資成數)，融資成數：上市 6 成、上櫃 5 成
- 觀察期（約一年）第一天的融資餘額，成本假設為當天成交均價；之後每天新增留倉的部位（融資買進扣掉資券互抵的當沖部分）以當天成交均價計入，賣出、現償依平均成本從舊部位移出
- 官方沒有公布個股維持率，這是用公開資料推估的整體平均值，僅供參考
