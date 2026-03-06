> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, що автоматично перекладає ваш `README.md` кількома мовами за допомогою Gemini API. Він інтелектуально додає перехресне навігаційне меню перемикання мов в усі файли та може або фіксувати (commit) зміни безпосередньо, або створювати Pull Request для перевірки.

## 🚀 Можливості
* **Багатомовна підтримка:** Генеруйте файли README кількома мовами за один запуск.
* **Автоматична навігація:** Автоматично вставляє та підтримує стандартне меню перемикання мов у верхній частині ваших файлів (можна вимкнути). ШІ автоматично стилізує його!
* **Користувацький стиль:** Ви можете надати параметр користувацького стилю меню, щоб ШІ відформатував перемикач мов саме так, як ви цього хочете.
* **Відстеження токенів:** Виводить статистику використання токенів Gemini.

## 🛠 Використання

Створіть файл робочого процесу (наприклад, `.github/workflows/translate.yml`):

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

## 📥 Вхідні параметри

| Параметр | Обов'язковий | За замовчуванням | Опис |
| --- | --- | --- | --- |
| `api_key` | Так |  | Ваш API-ключ Google Gemini. |
| `github_token` | Так |  | Стандартний токен GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Так |  | Цільові мови, розділені комами (наприклад, `ru, es`). |
| `output_dir` | Ні | | Каталог для збереження перекладених файлів. За замовчуванням це каталог вихідного файлу. |
| `add_language_menu` | Ні | `true` | Встановіть `false`, щоб вимкнути автогенерацію мовного меню. |
| `menu_style` | Ні | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Еталонний стиль, який ШІ використовує при генерації нового мовного меню. |
| `commit_message` | Ні | `docs: auto-translate README via Gemini` | Текст, що використовується для повідомлення коміту git. |
| `model` | Ні | `gemini-3.1-pro-preview` | Модель Gemini для використання. |
| `source_file` | Ні | `README.md` | Базовий файл для перекладу. |

## 🔑 Як отримати API-ключ Google Gemini

Щоб використовувати цю дію, вам потрібен безкоштовний API-ключ від Google AI Studio:

1. Перейдіть до [Google AI Studio](https://aistudio.google.com/).
2. Увійдіть за допомогою свого облікового запису Google.
3. У лівому навігаційному меню натисніть **Get API key**.
4. Натисніть кнопку **Create API key**.
5. Скопіюйте згенерований ключ.
6. Перейдіть до свого репозиторію GitHub -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Натисніть **New repository secret**, назвіть його `GEMINI_API_KEY`, вставте свій ключ у поле Secret та збережіть.

## 🔑 Як налаштувати стандартний токен GitHub

Ця дія використовує вбудований `GITHUB_TOKEN` для надсилання комітів або створення Pull Requests. Вам **не потрібно** створювати Personal Access Token (PAT) вручну, але ви **повинні** переконатися, що токен за замовчуванням має правильні дозволи:

1. Перейдіть у вашому репозиторії до **Settings** -> **Actions** -> **General**.
2. Прокрутіть вниз до розділу **Workflow permissions**.
3. Виберіть **Read and write permissions**.
4. Натисніть **Save**.
5. У вашому YAML-файлі робочого процесу просто передайте `${{ secrets.GITHUB_TOKEN }}` у параметр `github_token` (як показано в прикладі використання).

## 📄 Ліцензія

Цей проєкт ліцензовано на умовах ліцензії MIT — детальну інформацію дивіться у файлі [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).