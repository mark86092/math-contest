# math-contest 專案規範

## 技術架構

- Hugo 靜態網站，主題為 `hugo-book`
- 內容放在 `content/`，靜態檔案（PDF）放在 `static/files/`
- PDF 連結需加 `/math-contest/` 前綴，例如 `/math-contest/files/...`

## 目錄結構

```
content/學科能力競賽/<年度>/複賽/<區域>/<考試>.md
content/學科能力競賽/<年度>/決賽/<考試>.md
static/files/學科能力競賽/<年度>/複賽/<區域>/<檔案>.pdf
static/files/學科能力競賽/<年度>/決賽/<檔案>.pdf
```

## Weight 規則

- 複賽比決賽先發生，weight 較小（複賽: 20，決賽: 30）
- 年度 `_index.md` 的 weight 用年度數字（例如 `weight: 109`）

## 內容格式

- 各考試 markdown 檔的題目用 `## 第一題`、`## 第二題` 等標題
- 參考資料統一放在頁面**最下方**，標題為 `## Reference`，內容用列點
- PDF 連結格式：`- [說明文字](/math-contest/files/...)`
- 來源網站直接展開 URL，例如：`- https://cantor.math.ntnu.edu.tw/...`

## 各年度區域命名

複賽區域統一使用：北一區、北二區、嘉義區、臺南區、高屏區、臺北市、新北市、臺中市、高雄市
