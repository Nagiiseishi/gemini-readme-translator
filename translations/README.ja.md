> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Gemini APIを使用して、`README.md`を自動的に複数の言語に翻訳するGitHub Actionです。相互リンクされた言語ナビゲーションメニューをすべてのファイルにインテリジェントに挿入し、変更を直接コミットするか、レビュー用のPull Requestを作成することができます。

## 🚀 機能
* **多言語サポート:** 1回の実行で複数言語のREADMEを生成します。
* **自動ナビゲーション:** ファイルの先頭に標準の言語切り替えメニューを自動的に挿入および保守します（無効化も可能）。AIが自動的にスタイルを設定します！
* **カスタムスタイル:** カスタムメニュースタイルパラメータを提供することで、AIが希望どおりのフォーマットで言語切り替えメニューを生成するようにできます。
* **トークントラッキング:** Geminiのトークン使用状況の統計を出力します。

## 🛠 使用方法

ワークフローファイル（例: `.github/workflows/translate.yml`）を作成します:

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

## 📥 入力

| 入力 | 必須 | デフォルト | 説明 |
| --- | --- | --- | --- |
| `api_key` | はい |  | Google GeminiのAPIキー。 |
| `github_token` | はい |  | 標準のGitHubトークン（`${{ secrets.GITHUB_TOKEN }}`）。 |
| `languages` | はい |  | カンマ区切りのターゲット言語（例: `ru, es`）。 |
| `output_dir` | いいえ | | 翻訳されたファイルを保存するディレクトリ。デフォルトはソースファイルのディレクトリです。 |
| `add_language_menu` | いいえ | `true` | `false`に設定すると、言語メニューの自動生成が無効になります。 |
| `menu_style` | いいえ | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | 新しい言語メニューを生成する際にAIが使用するリファレンススタイル。 |
| `commit_message` | いいえ | `docs: auto-translate README via Gemini` | gitコミットメッセージに使用されるテキスト。 |
| `model` | いいえ | `gemini-3.1-pro-preview` | 使用するGeminiモデル。 |
| `source_file` | いいえ | `README.md` | 翻訳元のベースファイル。 |

## 🔑 Google Gemini APIキーの取得方法

このアクションを使用するには、Google AI Studioからの無料APIキーが必要です:

1. [Google AI Studio](https://aistudio.google.com/)にアクセスします。
2. Googleアカウントでログインします。
3. 左側のナビゲーションメニューで**Get API key**をクリックします。
4. **Create API key**ボタンをクリックします。
5. 生成されたキーをコピーします。
6. GitHubリポジトリの **Settings** -> **Secrets and variables** -> **Actions** に移動します。
7. **New repository secret**をクリックし、名前を`GEMINI_API_KEY`にして、Secretフィールドにキーを貼り付け、保存します。

## 🔑 標準GitHubトークンの設定方法

このアクションは、組み込みの`GITHUB_TOKEN`を使用してコミットをプッシュしたり、Pull Requestを作成したりします。手動でPersonal Access Token (PAT) を作成する**必要はありません**が、デフォルトトークンに正しい権限があることを確認する**必要があります**:

1. リポジトリの **Settings** -> **Actions** -> **General** に移動します。
2. **Workflow permissions**セクションまで下にスクロールします。
3. **Read and write permissions**を選択します。
4. **Save**をクリックします。
5. ワークフローYAMLで、（使用例に示されているように）`${{ secrets.GITHUB_TOKEN }}`を`github_token`入力に渡すだけです。

## 📄 ライセンス

このプロジェクトはMITライセンスの下でライセンスされています。詳細については、[LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE)ファイルを参照してください。