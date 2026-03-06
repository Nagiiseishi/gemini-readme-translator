> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README 翻译器

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

一个使用 Gemini API 自动将你的 `README.md` 翻译成多种语言的 GitHub Action。它会智能地在所有文件中注入相互链接的语言导航菜单，并且可以直接提交更改或创建 Pull Request 以供审查。

## 🚀 功能特性
* **多语言支持：** 一次运行即可生成多种语言的 README。
* **自动导航：** 自动在文件顶部插入并维护标准的语言切换菜单（可禁用）。AI 会自动为其设置样式！
* **自定义样式：** 你可以提供自定义的菜单样式参数，让 AI 完全按照你的期望来格式化语言切换器。
* **Token 跟踪：** 输出 Gemini Token 使用情况的统计信息。

## 🛠 使用方法

创建一个工作流文件（例如：`.github/workflows/translate.yml`）：

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

## 📥 输入参数

| 参数 | 是否必填 | 默认值 | 描述 |
| --- | --- | --- | --- |
| `api_key` | 是 |  | 你的 Google Gemini API 密钥。 |
| `github_token` | 是 |  | 标准的 GitHub 令牌 (`${{ secrets.GITHUB_TOKEN }}`)。 |
| `languages` | 是 |  | 以逗号分隔的目标语言（例如：`ru, es`）。 |
| `output_dir` | 否 | | 保存翻译文件的目录。默认与源文件所在的目录相同。 |
| `add_language_menu` | 否 | `true` | 设置为 `false` 以禁用自动生成语言菜单。 |
| `menu_style` | 否 | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | AI 生成新语言菜单时使用的参考样式。 |
| `commit_message` | 否 | `docs: auto-translate README via Gemini` | 用于 git 提交信息的文本。 |
| `model` | 否 | `gemini-3.1-pro-preview` | 要使用的 Gemini 模型。 |
| `source_file` | 否 | `README.md` | 要翻译的基础文件。 |

## 🔑 如何获取 Google Gemini API 密钥

要使用此 Action，你需要一个来自 Google AI Studio 的免费 API 密钥：

1. 访问 [Google AI Studio](https://aistudio.google.com/)。
2. 使用你的 Google 账号登录。
3. 在左侧导航菜单中，点击 **Get API key**。
4. 点击 **Create API key** 按钮。
5. 复制生成的密钥。
6. 前往你的 GitHub 仓库 -> **Settings** -> **Secrets and variables** -> **Actions**。
7. 点击 **New repository secret**，将其命名为 `GEMINI_API_KEY`，将你的密钥粘贴到 Secret 字段中，然后保存。

## 🔑 如何配置标准 GitHub 令牌 (Token)

此 Action 使用内置的 `GITHUB_TOKEN` 来推送提交或创建 Pull Request。你**不需要**手动创建个人访问令牌（PAT），但你**必须**确保默认令牌具有正确的权限：

1. 前往你的仓库 **Settings** -> **Actions** -> **General**。
2. 向下滚动到 **Workflow permissions** 部分。
3. 选择 **Read and write permissions**。
4. 点击 **Save**。
5. 在你的工作流 YAML 文件中，只需将 `${{ secrets.GITHUB_TOKEN }}` 传递给 `github_token` 输入参数（如使用示例所示）。

## 📄 许可证

本项目采用 MIT 许可证进行授权 - 有关详细信息，请参阅 [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) 文件。