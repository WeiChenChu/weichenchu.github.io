# 網站分支發布與維護指南

本文件說明如何審查、發布與持續維護
`sol-design-architecture-refine-2026-07` 分支上的 MkDocs Material 網站。

## 1. Repository 與分支角色

- `main`：正式網站的 Markdown、圖片、CSS 與 `mkdocs.yml` 來源。
- `sol-design-architecture-refine-2026-07`：本次網站架構與視覺調整的試作分支。
- `gh-pages`：由 MkDocs 產生的靜態網站檔案，供 GitHub Pages 發布。
- `site/`：本機 build 產物，已由 `.gitignore` 排除，不應提交。

正式網站 repository：
[WeiChenChu/weichenchu.github.io](https://github.com/WeiChenChu/weichenchu.github.io)

不要直接編輯 `gh-pages` 的 HTML。所有內容與樣式都應先修改 source，
完成驗證後再由 MkDocs 重新部署。

## 2. 主要檔案

| 檔案 | 用途 |
| --- | --- |
| `mkdocs.yml` | 網站名稱、主題、導覽、Markdown extensions 與 CSS 載入設定 |
| `docs/index.md` | 首頁、研究支援流程、主要入口與聯絡資訊 |
| `docs/about.md` | 現職、經歷、教育、榮譽、社群角色與邀請演講 |
| `docs/expertise.md` | Imaging support、bioimage analysis 與 reproducible workflow 能力 |
| `docs/training.md` | 課程、開放教材與持續專業發展紀錄 |
| `docs/workflows-tools.md` | 開源 workflow 與工具說明 |
| `docs/stylesheets/extra.css` | 首頁、表格、workflow cards、明暗主題與響應式配置 |
| `docs/images/` | 首頁照片、證書與其他公開素材 |
| `docs/CNAME` | 自訂網域設定；部署前後都必須保留 |

## 3. 本機環境

目前使用 conda environment `mkdocs_material`，主要版本記錄在
`mkdocs_material_working.yml`：

- Python 3.12
- MkDocs Material 9.6.20
- mkdocs-static-i18n 1.3.0

現有環境可直接使用：

```powershell
conda run -n mkdocs_material mkdocs --version
```

`mkdocs_material_working.yml` 末尾含有舊電腦的絕對 `prefix`，若要在新電腦
重建環境，應先移除該 `prefix`，或手動建立同名環境：

```powershell
conda create -n mkdocs_material -c conda-forge python=3.12 pip
conda run -n mkdocs_material pip install mkdocs-material==9.6.20 mkdocs-static-i18n==1.3.0
```

## 4. 發布前審查

先確認目前位於正確分支：

```powershell
git switch sol-design-architecture-refine-2026-07
git status --short --branch
```

本分支建立時包含尚未提交的修改。第一次發布前，應確認以下四個新頁面
已被 Git 追蹤：

```text
docs/about.md
docs/expertise.md
docs/training.md
docs/workflows-tools.md
```

執行完整 build：

```powershell
conda run -n mkdocs_material mkdocs build --strict
git diff --check
```

啟動本機預覽：

```powershell
conda run -n mkdocs_material mkdocs serve -a 127.0.0.1:8000
```

瀏覽以下頁面：

- `http://127.0.0.1:8000/`
- `http://127.0.0.1:8000/about/`
- `http://127.0.0.1:8000/expertise/`
- `http://127.0.0.1:8000/training/`
- `http://127.0.0.1:8000/workflows-tools/`

發布前至少檢查：

- 首頁照片沒有被裁切，姓名與中文文字顯示正確。
- 桌機 top navigation 與手機 drawer navigation 都可使用。
- 手機沒有水平捲動；首頁可在首屏看到下一段提示。
- Training table 在桌機為表格、手機為堆疊欄位。
- Workflow cards 在桌機與手機沒有文字溢出。
- Light mode 與 dark mode 都有足夠對比。
- 新增或修改的外部連結與描述相符。
- `docs/CNAME` 仍存在。

## 5. 提交與推送試作分支

確認 diff 後，將 source 與本文件一起提交：

```powershell
git add mkdocs.yml docs BRANCH_RELEASE_AND_MAINTENANCE.md
git status --short
git commit -m "Refine site architecture and responsive design"
git push -u origin sol-design-architecture-refine-2026-07
```

推送後，建議在 GitHub 建立 pull request，目標設為 `main`。Pull request
應記錄：

- 首頁資訊架構變更。
- 導覽與頁面分類變更。
- 照片比例與手機 hero 調整。
- Training table 與 Workflow card 響應式驗證結果。
- `mkdocs build --strict` 結果。

## 6. 合併到 main

在 GitHub 完成 pull request 合併後，更新本機 `main`：

```powershell
git switch main
git pull --ff-only origin main
conda run -n mkdocs_material mkdocs build --strict
```

若選擇完全在本機合併，先確定 `main` 沒有其他未同步修改：

```powershell
git switch main
git pull --ff-only origin main
git merge --ff-only sol-design-architecture-refine-2026-07
conda run -n mkdocs_material mkdocs build --strict
git push origin main
```

如果 `--ff-only` 失敗，表示分支歷史已分歧。此時先檢查 commit history，
不要用 `git reset --hard` 或強制 push 解決。

## 7. 發布到 GitHub Pages

目前 repository 沒有 GitHub Actions 部署設定，`gh-pages` 歷史顯示為
MkDocs 手動部署。應在已同步、已通過 strict build 的 `main` 上執行：

```powershell
git switch main
git status --short --branch
conda run -n mkdocs_material mkdocs build --strict
conda run -n mkdocs_material mkdocs gh-deploy --force
```

`mkdocs gh-deploy --force` 會重新生成網站並推送到 `gh-pages`。執行前應確認：

- 工作目錄乾淨。
- 目前分支是 `main`。
- `main` 已推送到 `origin/main`。
- strict build 已通過。
- `docs/CNAME` 正確。

部署後，在 GitHub repository 的 `Settings > Pages` 確認發布來源仍為
`gh-pages` branch 的 root，並檢查正式網域：
[https://weichenchu.com/](https://weichenchu.com/)

GitHub Pages 與 CDN 更新可能需要數分鐘。不要因短暫看見舊版就立即重複部署。

## 8. 日常內容維護

### 更新 About

- 現職或日期改變時，同步更新首頁 role statement 與 `docs/about.md`。
- 不新增未確認的職稱、榮譽、演講或社群角色。
- Community role 應清楚區分 member、founding member 與 maintainer。

### 更新 Training

- 新活動放在相應年份與分類中，通常以較新的項目在前。
- 教材表格應提供 Topic、Training context 與 Materials。
- Materials link text 應說明媒介與語言，例如 `Zenodo slides`、
  `YouTube recording, Mandarin`。
- 同名課程應在標題加入活動或主辦單位，避免無法辨識。

### 更新 Workflows

每個 workflow 應維持相同資訊結構：

- `Data`：影像 modality、sample 或 acquisition context。
- `Workflow`：主要處理步驟，例如 denoising、segmentation、tracking 或 quantification。
- `Stack`：FIJI/ImageJ、Python、napari、Imaris、CLIJ 或 clEsperanto。
- `Value`：該流程提供的測量、品質控制或重現性價值。

新增 workflow 時，先放入最接近的主題群組；只有在至少有兩個相關項目時，
才建立新的頂層分類。

### 更新圖片與樣式

- 首頁照片維持完整原圖比例，避免使用會裁切臉部或背景的固定直式比例。
- 新圖片應壓縮到適合網頁的尺寸，保留可描述內容的 `alt` text。
- 色彩優先修改 `extra.css` 的 CSS variables，不要在多個 selector 重複硬編碼。
- 主要 responsive breakpoints 為 900px 與 700px；修改後必須重測桌機與手機。
- 不直接修改 `site/` 內的生成 CSS 或 HTML。

## 9. 建議的維護分支流程

每次維護都從最新 `main` 建立短期分支：

```powershell
git switch main
git pull --ff-only origin main
git switch -c content-update-YYYY-MM
```

建議命名：

- `content-update-YYYY-MM`
- `training-update-YYYY`
- `workflow-update-<topic>`
- `visual-refine-<topic>`

完成後依序執行 build、preview、commit、push、pull request、merge 與
`mkdocs gh-deploy`。不要把日常 source 修改直接提交到 `gh-pages`。

## 10. 回滾

如果正式發布後發現問題，優先回滾 source，再重新部署：

```powershell
git switch main
git pull --ff-only origin main
git log --oneline -10
git revert <problem-commit-or-merge-commit>
conda run -n mkdocs_material mkdocs build --strict
git push origin main
conda run -n mkdocs_material mkdocs gh-deploy --force
```

`git revert` 會保留歷史並建立反向 commit，適合已推送的正式網站。避免使用
`git reset --hard`、改寫公開 branch history，或直接刪除 `gh-pages` 內容。

若只有自訂網域失效，先檢查：

1. `docs/CNAME` 是否存在且內容正確。
2. `gh-pages` root 是否包含 `CNAME`。
3. GitHub `Settings > Pages` 的 custom domain 與 HTTPS 狀態。

## 11. 發布檢查清單

- [ ] 位於正確的 feature branch，且所有新檔案已被追蹤。
- [ ] `mkdocs build --strict` 通過。
- [ ] `git diff --check` 通過。
- [ ] 桌機與手機首頁已檢查。
- [ ] About、Imaging Support、Training、Workflows 路由可開啟。
- [ ] Light mode 與 dark mode 已檢查。
- [ ] 外部連結、圖片與 PDF 可開啟。
- [ ] `docs/CNAME` 仍存在。
- [ ] Feature branch 已 push 並合併至 `main`。
- [ ] `main` 已 push 且工作目錄乾淨。
- [ ] 從 `main` 執行 `mkdocs gh-deploy --force`。
- [ ] 正式網域與 GitHub Pages 狀態已確認。
