> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, который автоматически переводит ваш `README.md` на несколько языков с использованием Gemini API. Он интеллектуально вставляет меню языковой навигации с перекрестными ссылками во все файлы и может либо фиксировать изменения напрямую (коммит), либо создавать Pull Request для проверки.

## 🚀 Возможности
* **Многоязычная поддержка:** Генерация файлов README для нескольких языков за один запуск.
* **Автоматическая навигация:** Автоматически вставляет и поддерживает стандартное меню переключения языков в начале ваших файлов (можно отключить). ИИ автоматически форматирует его!
* **Настраиваемый стиль:** Вы можете предоставить параметр пользовательского стиля меню, чтобы ИИ форматировал переключатель языков именно так, как вы хотите.
* **Отслеживание токенов:** Выводит статистику использования токенов Gemini.

## 🛠 Использование

Создайте файл рабочего процесса (например, `.github/workflows/translate.yml`):

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

## 📥 Входные параметры

| Входной параметр | Обязательный | По умолчанию | Описание |
| --- | --- | --- | --- |
| `api_key` | Да |  | Ваш API-ключ Google Gemini. |
| `github_token` | Да |  | Стандартный токен GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Да |  | Целевые языки, разделенные запятыми (например, `ru, es`). |
| `output_dir` | Нет | | Каталог для сохранения переведенных файлов. По умолчанию используется каталог исходного файла. |
| `add_language_menu` | Нет | `true` | Установите в `false`, чтобы отключить автоматическую генерацию языкового меню. |
| `menu_style` | Нет | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Эталонный стиль, который ИИ использует при генерации нового языкового меню. |
| `commit_message` | Нет | `docs: auto-translate README via Gemini` | Текст, используемый для сообщения коммита в git. |
| `model` | Нет | `gemini-3.1-pro-preview` | Используемая модель Gemini. |
| `source_file` | Нет | `README.md` | Базовый файл для перевода. |

## 🔑 Как получить API-ключ Google Gemini

Для использования этого Action вам потребуется бесплатный API-ключ от Google AI Studio:

1. Перейдите в [Google AI Studio](https://aistudio.google.com/).
2. Войдите с помощью своего аккаунта Google.
3. В левом навигационном меню нажмите на **Get API key** (Получить API-ключ).
4. Нажмите кнопку **Create API key** (Создать API-ключ).
5. Скопируйте сгенерированный ключ.
6. Перейдите в ваш репозиторий GitHub -> **Settings** (Настройки) -> **Secrets and variables** (Секреты и переменные) -> **Actions**.
7. Нажмите **New repository secret** (Новый секрет репозитория), назовите его `GEMINI_API_KEY`, вставьте ваш ключ в поле Secret и сохраните.

## 🔑 Как настроить стандартный токен GitHub

Этот Action использует встроенный токен `GITHUB_TOKEN` для отправки коммитов или создания Pull Request'ов. Вам **не нужно** вручную создавать личный токен доступа (PAT), но вы **должны** убедиться, что токен по умолчанию имеет правильные разрешения:

1. Перейдите в вашем репозитории в **Settings** (Настройки) -> **Actions** -> **General** (Общие).
2. Прокрутите вниз до раздела **Workflow permissions** (Разрешения рабочего процесса).
3. Выберите **Read and write permissions** (Разрешения на чтение и запись).
4. Нажмите **Save** (Сохранить).
5. В вашем YAML-файле рабочего процесса просто передайте `${{ secrets.GITHUB_TOKEN }}` во входной параметр `github_token` (как показано в примере использования).

## 📄 Лицензия

Этот проект распространяется под лицензией MIT — подробности см. в файле [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).