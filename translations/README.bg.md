> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, който автоматично превежда вашия `README.md` на множество езици, използвайки Gemini API. Той интелигентно вмъква взаимно свързано езиково навигационно меню във всички файлове и може или да комитне промените директно, или да създаде Pull Request за преглед.

## 🚀 Характеристики
* **Многоезична поддръжка:** Генерирайте README файлове за множество езици с едно изпълнение.
* **Автоматична навигация:** Автоматично вмъква и поддържа стандартно меню за превключване на езика в горната част на вашите файлове (може да бъде деактивирано). Изкуственият интелект го стилизира автоматично!
* **Персонализирано стилизиране:** Можете да предоставите параметър за персонализиран стил на менюто, така че изкуственият интелект да форматира превключвателя на езици точно както искате.
* **Проследяване на токени:** Извежда статистика за използването на токени в Gemini.

## 🛠 Употреба

Създайте workflow файл (напр. `.github/workflows/translate.yml`):

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

## 📥 Входни параметри

| Входен параметър | Задължителен | По подразбиране | Описание |
| --- | --- | --- | --- |
| `api_key` | Да |  | Вашият Google Gemini API ключ. |
| `github_token` | Да |  | Стандартен GitHub токен (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Да |  | Целеви езици, разделени със запетая (напр. `ru, es`). |
| `output_dir` | Не | | Директория за запазване на преведените файлове. По подразбиране е директорията на изходния файл. |
| `add_language_menu` | Не | `true` | Задайте `false`, за да деактивирате автоматичното генериране на езиковото меню. |
| `menu_style` | Не | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Референтният стил, който изкуственият интелект използва при генериране на ново езиково меню. |
| `commit_message` | Не | `docs: auto-translate README via Gemini` | Текст, използван за git commit съобщението. |
| `model` | Не | `gemini-3.1-pro-preview` | Моделът на Gemini, който да се използва. |
| `source_file` | Не | `README.md` | Основният файл за превод. |

## 🔑 Как да получите Google Gemini API ключ

За да използвате този Action, ви е необходим безплатен API ключ от Google AI Studio:

1. Отидете в [Google AI Studio](https://aistudio.google.com/).
2. Влезте с вашия Google акаунт.
3. В лявото навигационно меню кликнете върху **Get API key**.
4. Кликнете върху бутона **Create API key**.
5. Копирайте генерирания ключ.
6. Отидете във вашето GitHub хранилище -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Кликнете върху **New repository secret**, наименувайте го `GEMINI_API_KEY`, поставете вашия ключ в полето Secret и запазете.

## 🔑 Как да конфигурирате стандартния GitHub токен

Този Action използва вградения `GITHUB_TOKEN` за push на къмити или създаване на Pull Requests. **Не е необходимо** да създавате Personal Access Token (PAT) ръчно, но **трябва** да се уверите, че токенът по подразбиране има правилните права (permissions):

1. Отидете в настройките на вашето хранилище: **Settings** -> **Actions** -> **General**.
2. Превъртете надолу до раздела **Workflow permissions**.
3. Изберете **Read and write permissions**.
4. Кликнете върху **Save**.
5. Във вашия workflow YAML файл просто подайте `${{ secrets.GITHUB_TOKEN }}` към входния параметър `github_token` (както е показано в примера за употреба).

## 📄 Лиценз

Този проект е лицензиран съгласно MIT License - вижте файла [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) за подробности.