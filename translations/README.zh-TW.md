> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

這是一個 GitHub Action，能使用 Gemini API 自動將您的 `README.md` 翻譯成多種語言。它會智慧地在所有檔案中插入互相連結的語言導覽選單，並可以直接提交 (commit) 變更或建立 Pull Request 以供審閱。

## 🚀 功能特色
* **多語言支援：** 一次執行即可產生多種語言的 README 檔案。
* **自動導覽：** 自動在您的檔案頂部插入並維護標準的語言切換選單（可停用）。AI 會自動為其設定樣式！
* **自訂樣式：** 您可以提供自訂的選單樣式參數，讓 AI 完全按照您的需求來格式化語言切換器。
* **Token 追蹤：** 輸出 Gemini token 的使用量統計資訊。

## 🛠 使用方式

建立一個工作流程檔案（例如：`.github/workflows/translate.yml`）：

```yaml
name: Auto Translate README

on:
  push:
    paths:
      - 'README.md'
  workflow_dispatch:

jobs:
  translate:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Gemini README Translator
        uses: artryazanov/gemini-readme-translator@v1
        with:
          api_key: ${{ secrets.GEMINI_API_KEY }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
          languages: 'ru, zh-CN, es'
          add_language_menu: 'true'
          menu_style: '> 🌐 **Languages:** [English](README.md) | [Русский](README.ru.md)'


```

## 📥 輸入參數

| 參數 | 必填 | 預設值 | 說明 |
| --- | --- | --- | --- |
| `api_key` | 是 |  | 您的 Google Gemini API 金鑰。 |
| `github_token` | 是 |  | 標準的 GitHub token (`${{ secrets.GITHUB_TOKEN }}`)。 |
| `languages` | 是 |  | 以逗號分隔的目標語言（例如：`ru, es`）。 |
| `output_dir` | 否 | | 儲存翻譯檔案的目錄。預設為來源檔案的所在目錄。 |
| `add_language_menu` | 否 | `true` | 設為 `false` 可停用自動產生語言選單。 |
| `menu_style` | 否 | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | AI 在產生新語言選單時使用的參考樣式。 |
| `commit_message` | 否 | `docs: auto-translate README via Gemini` | 用於 Git 提交 (commit) 訊息的文字。 |
| `model` | 否 | `gemini-3.1-pro-preview` | 要使用的 Gemini 模型。 |
| `source_file` | 否 | `README.md` | 要翻譯的基礎來源檔案。 |

## 🔑 如何取得 Google Gemini API 金鑰

要使用此 Action，您需要從 Google AI Studio 取得免費的 API 金鑰：

1. 前往 [Google AI Studio](https://aistudio.google.com/)。
2. 使用您的 Google 帳號登入。
3. 在左側導覽選單中，點擊 **Get API key**。
4. 點擊 **Create API key** 按鈕。
5. 複製產生的金鑰。
6. 前往您的 GitHub 儲存庫 -> **Settings** -> **Secrets and variables** -> **Actions**。
7. 點擊 **New repository secret**，命名為 `GEMINI_API_KEY`，將您的金鑰貼到 Secret 欄位中，然後儲存。

## 🔑 如何設定標準 GitHub Token

此 Action 使用內建的 `GITHUB_TOKEN` 來推送提交 (commit) 或建立 Pull Request。您**不需要**手動建立個人存取權杖 (PAT)，但您**必須**確保預設 Token 具有正確的權限：

1. 前往您儲存庫的 **Settings** -> **Actions** -> **General**。
2. 向下捲動到 **Workflow permissions** 區塊。
3. 選擇 **Read and write permissions**。
4. 點擊 **Save**。
5. 在您的工作流程 YAML 檔案中，只需將 `${{ secrets.GITHUB_TOKEN }}` 傳遞給 `github_token` 參數即可（如使用方式範例所示）。

## 📄 授權條款

本專案採用 MIT 授權條款 - 詳情請參閱 [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) 檔案。