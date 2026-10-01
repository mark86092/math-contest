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

亞太相關的三個分類為**不同活動**，勿混淆。各自的 content 目錄名、顯示名稱（由 `_index.md` 的 `title` front matter 控制）與 PDF 靜態路徑不必一致，對應如下：

| content 目錄 | 顯示名稱 | 網址 | PDF 靜態路徑（`static/files/…`） |
|---|---|---|---|
| `亞太數學奧林匹亞競賽初選考試` | 亞太數學奧林匹亞競賽初選考試 | `/亞太數學奧林匹亞競賽初選考試/` | `亞太數學奧林匹亞競賽初選考試/` |
| `APMO` | 亞太數學奧林匹亞競賽 | `/apmo/` | `亞太數學奧林匹亞競賽/` |
| `APMOC` | 亞太數學研習營 | `/apmoc/` | `亞太數學研習營/` |
| `TMO` | 臺灣數學奧林匹亞競賽 | `/tmo/` | `臺灣數學奧林匹亞競賽/` |
| `IMO` | 國際數學奧林匹亞競賽 | `/imo/` | `國際數學奧林匹亞競賽/` |

目錄名採英文簡稱者（`APMO`、`APMOC`、`TMO`、`IMO`）是為了網址方便輸入；顯示名稱仍為中文（網址會小寫化，例如 `TMO` → `/tmo/`）。

`亞太數學奧林匹亞競賽初選考試` 依各年度是否分階段而有兩種結構：

- 單一考試的年度（例如 2019、2020）：題目直接寫在 `content/亞太數學奧林匹亞競賽初選考試/<年度>/_index.md`
- 分階段的年度（例如 2022 年起分第一階段、第二階段）：每個階段是自己的子目錄，題目寫在該子目錄的 `_index.md`（`bookCollapseSection: true`）：

```
content/亞太數學奧林匹亞競賽初選考試/<年度>/第一階段/_index.md
content/亞太數學奧林匹亞競賽初選考試/<年度>/第二階段/_index.md
```

這是為了讓每一題的解答檔（見下方「題目解答檔」）能明確歸屬到正確的階段，避免「第一階段第一題」和「第二階段第一題」的解答檔案名稱混淆。

## Weight 規則

- 複賽比決賽先發生，weight 較小（複賽: 20，決賽: 30）
- 年度 `_index.md` 的 weight 用年度數字（例如 `weight: 109`）

## 內容格式

- 各考試 markdown 檔的題目用 `## 第一題`、`## 第二題` 等標題
- 參考資料放在 front matter 的 `references` 陣列，渲染時會統一顯示在頁面**最下方**（標題為 Reference），不要手動在內文寫 `## Reference`
  - PDF 連結：`{ text: "說明文字", url: "/math-contest/files/..." }`
  - 純網址（無額外說明文字）：只寫 `{ url: "https://..." }`，畫面上會直接顯示展開的 URL
  - 渲染邏輯見 `layouts/partials/docs/references.html`，由 `layouts/single.html`、`layouts/list.html` 呼叫

```yaml
references:
  - text: "111高中學科能力競賽數學科決賽總報告.pdf"
    url: "/math-contest/files/學科能力競賽/111學年度/決賽/111高中學科能力競賽數學科決賽總報告.pdf"
  - url: "https://cantor.math.ntnu.edu.tw/..."
```
- 日期用 `date` front matter（顯示在標題下方，格式 `2006/01/02`，同時決定 timeline 排序）。跨多日的活動（例如研習營）另加 `enddate`，會渲染成「開始 – 結束」區間；`date` 仍為開始日。此區間顯示由 `layouts/partials/docs/post-meta.html` 處理。

## 特輯（彙整頁）

「特輯」是跨年度、跨分類的彙整頁，放在 `content/特輯/` 底下，例如「學科能力競賽 複賽北一區」列出各年度的複賽北一區。

- 每個特輯是一個 markdown 檔，front matter 設 `layout: "list-filter"` 與 `filterpath: "<路徑片段>"`（例如 `複賽/北一區`）。
- `layouts/list-filter.html` 會掃描全站，列出檔案路徑含 `filterpath` 的 section 頁面，一列一個，文字為其上上層（年度）標題，連結指向該 section；該頁自身若有 `date` 才顯示日期。
- 新增其他特輯（例如其他區、其他考試類別）只要再建一個 markdown 檔改 `filterpath` 即可，不需另寫 layout。

## 各年度區域命名

區域命名依各年度實際資料而定，不固定。常見的有：北一區、北二區、嘉義區、臺南區、高屏區、臺北市、新北市、臺中市、高雄市、臺中區等。新增時以來源資料的實際區域名稱為準，不要自行推斷。

## 題目解答檔

- 每一題的解答獨立成一個檔案，與該題目所屬的 `_index.md` 放在同一層目錄（分階段的年度就放在對應的 `第一階段/`、`第二階段/` 子目錄下，不可放在年度資料夾下，以免無法區分是哪個階段的題目）
- 檔名格式：`第X題解答-<來源>.md`，例如 `第二題解答-AI.md`
  - `<來源>` 標示解答提供者，目前有 `AI`（AI 生成）與官方/人工來源（例如 `官方`、`人工`）
- Front matter `title` 格式：`"第X題<來源>解答"`，例如 `"第二題AI解答"`
- Front matter `weight` 公式：`100 + 10 * 題號 + <來源代碼>`
  - `<來源代碼>`：AI 為 `2`，人工／官方為 `1`
  - 例如第二題的 AI 解答 weight 為 `100 + 10*2 + 2 = 122`
- AI 生成的解答檔內容最上方需加註：`*以下為 AI 生成之解答，僅供參考，未經正式審核。*`
