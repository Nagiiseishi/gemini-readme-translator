> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# ಜೆಮಿನಿ README ಅನುವಾದಕ (Gemini README Translator)

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Gemini API ಬಳಸಿಕೊಂಡು ನಿಮ್ಮ `README.md` ಅನ್ನು ಬಹು-ಭಾಷೆಗಳಿಗೆ ಸ್ವಯಂಚಾಲಿತವಾಗಿ ಅನುವಾದಿಸುವ ಒಂದು GitHub Action. ಇದು ಎಲ್ಲಾ ಫೈಲ್‌ಗಳಿಗೆ ಅಡ್ಡ-ಸಂಪರ್ಕಿತ (cross-linked) ಭಾಷಾ ನ್ಯಾವಿಗೇಷನ್ ಮೆನುವನ್ನು ಬುದ್ಧಿವಂತಿಕೆಯಿಂದ ಸೇರಿಸುತ್ತದೆ ಮತ್ತು ಬದಲಾವಣೆಗಳನ್ನು ನೇರವಾಗಿ ಕಮಿಟ್ ಮಾಡಬಹುದು ಅಥವಾ ವಿಮರ್ಶೆಗಾಗಿ ಪುಲ್ ರಿಕ್ವೆಸ್ಟ್ (Pull Request) ಅನ್ನು ರಚಿಸಬಹುದು.

## 🚀 ವೈಶಿಷ್ಟ್ಯಗಳು
* **ಬಹು-ಭಾಷಾ ಬೆಂಬಲ:** ಒಂದೇ ಬಾರಿಗೆ ಅನೇಕ ಭಾಷೆಗಳಿಗೆ README ಗಳನ್ನು ರಚಿಸಿ.
* **ಸ್ವಯಂ-ನ್ಯಾವಿಗೇಷನ್:** ನಿಮ್ಮ ಫೈಲ್‌ಗಳ ಮೇಲ್ಭಾಗದಲ್ಲಿ ಗುಣಮಟ್ಟದ ಭಾಷಾ ಸ್ವಿಚರ್ ಮೆನುವನ್ನು ಸ್ವಯಂಚಾಲಿತವಾಗಿ ಸೇರಿಸುತ್ತದೆ ಮತ್ತು ನಿರ್ವಹಿಸುತ್ತದೆ (ಇದನ್ನು ನಿಷ್ಕ್ರಿಯಗೊಳಿಸಬಹುದು). AI ಇದನ್ನು ಸ್ವಯಂಚಾಲಿತವಾಗಿ ವಿನ್ಯಾಸಗೊಳಿಸುತ್ತದೆ!
* **ಕಸ್ಟಮ್ ಸ್ಟೈಲಿಂಗ್:** ನೀವು ಕಸ್ಟಮ್ ಮೆನು ಶೈಲಿಯ ಪ್ಯಾರಾಮೀಟರ್ ಅನ್ನು ಒದಗಿಸಬಹುದು, ಇದರಿಂದ AI ಭಾಷಾ ಸ್ವಿಚರ್ ಅನ್ನು ನಿಮಗೆ ಬೇಕಾದ ರೀತಿಯಲ್ಲಿಯೇ ಫಾರ್ಮ್ಯಾಟ್ ಮಾಡುತ್ತದೆ.
* **ಟೋಕನ್ ಟ್ರ್ಯಾಕಿಂಗ್:** Gemini ಟೋಕನ್ ಬಳಕೆಯ ಅಂಕಿಅಂಶಗಳನ್ನು ಔಟ್‌ಪುಟ್ ಮಾಡುತ್ತದೆ.

## 🛠 ಬಳಕೆ

ಒಂದು ವರ್ಕ್‌ಫ್ಲೋ ಫೈಲ್ ಅನ್ನು ರಚಿಸಿ (ಉದಾಹರಣೆಗೆ, `.github/workflows/translate.yml`):

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

## 📥 ಇನ್‌ಪುಟ್‌ಗಳು

| ಇನ್‌ಪುಟ್ | ಅಗತ್ಯವಿದೆಯೇ | ಡೀಫಾಲ್ಟ್ | ವಿವರಣೆ |
| --- | --- | --- | --- |
| `api_key` | ಹೌದು |  | ನಿಮ್ಮ Google Gemini API ಕೀ. |
| `github_token` | ಹೌದು |  | ಸಾಮಾನ್ಯ GitHub ಟೋಕನ್ (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | ಹೌದು |  | ಅಲ್ಪವಿರಾಮದಿಂದ ಬೇರ್ಪಟ್ಟ ಗುರಿ ಭಾಷೆಗಳು (ಉದಾ. `ru, es`). |
| `output_dir` | ಇಲ್ಲ | | ಅನುವಾದಿತ ಫೈಲ್‌ಗಳನ್ನು ಉಳಿಸಲು ಡೈರೆಕ್ಟರಿ. ಡೀಫಾಲ್ಟ್ ಆಗಿ ಮೂಲ ಫೈಲ್‌ನ ಡೈರೆಕ್ಟರಿಯನ್ನು ಬಳಸುತ್ತದೆ. |
| `add_language_menu` | ಇಲ್ಲ | `true` | ಭಾಷಾ ಮೆನುವಿನ ಸ್ವಯಂ-ರಚನೆಯನ್ನು ನಿಷ್ಕ್ರಿಯಗೊಳಿಸಲು `false` ಎಂದು ಹೊಂದಿಸಿ. |
| `menu_style` | ಇಲ್ಲ | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | ಹೊಸ ಭಾಷಾ ಮೆನುವನ್ನು ರಚಿಸುವಾಗ AI ಬಳಸುವ ಉಲ್ಲೇಖ (ರೆಫರೆನ್ಸ್) ಶೈಲಿ. |
| `commit_message` | ಇಲ್ಲ | `docs: auto-translate README via Gemini` | git ಕಮಿಟ್ ಸಂದೇಶಕ್ಕಾಗಿ ಬಳಸುವ ಪಠ್ಯ. |
| `model` | ಇಲ್ಲ | `gemini-3.1-pro-preview` | ಬಳಸಬೇಕಾದ Gemini ಮಾಡೆಲ್. |
| `source_file` | ಇಲ್ಲ | `README.md` | ಅನುವಾದಿಸಬೇಕಾದ ಮೂಲ ಫೈಲ್. |

## 🔑 Google Gemini API ಕೀಯನ್ನು ಪಡೆಯುವುದು ಹೇಗೆ

ಈ ಆಕ್ಷನ್ ಅನ್ನು ಬಳಸಲು, ನಿಮಗೆ Google AI Studio ದಿಂದ ಉಚಿತ API ಕೀಯ ಅಗತ್ಯವಿದೆ:

1. [Google AI Studio](https://aistudio.google.com/) ಗೆ ಹೋಗಿ.
2. ನಿಮ್ಮ Google ಖಾತೆಯೊಂದಿಗೆ ಸೈನ್ ಇನ್ ಮಾಡಿ.
3. ಎಡಗಡೆಯ ನ್ಯಾವಿಗೇಷನ್ ಮೆನುವಿನಲ್ಲಿ, **Get API key** ಮೇಲೆ ಕ್ಲಿಕ್ ಮಾಡಿ.
4. **Create API key** ಬಟನ್ ಅನ್ನು ಕ್ಲಿಕ್ ಮಾಡಿ.
5. ರಚಿಸಲಾದ ಕೀಯನ್ನು ಕಾಪಿ ಮಾಡಿ.
6. ನಿಮ್ಮ GitHub ರೆಪೊಸಿಟರಿಗೆ ಹೋಗಿ -> **Settings** -> **Secrets and variables** -> **Actions**.
7. **New repository secret** ಅನ್ನು ಕ್ಲಿಕ್ ಮಾಡಿ, ಅದಕ್ಕೆ `GEMINI_API_KEY` ಎಂದು ಹೆಸರಿಸಿ, ನಿಮ್ಮ ಕೀಯನ್ನು ಸೀಕ್ರೆಟ್ ಫೀಲ್ಡ್‌ನಲ್ಲಿ ಪೇಸ್ಟ್ ಮಾಡಿ ಮತ್ತು ಉಳಿಸಿ.

## 🔑 ಸಾಮಾನ್ಯ GitHub ಟೋಕನ್ ಅನ್ನು ಕಾನ್ಫಿಗರ್ ಮಾಡುವುದು ಹೇಗೆ

ಕಮಿಟ್‌ಗಳನ್ನು ಪುಶ್ ಮಾಡಲು ಅಥವಾ ಪುಲ್ ರಿಕ್ವೆಸ್ಟ್‌ಗಳನ್ನು ರಚಿಸಲು ಈ ಆಕ್ಷನ್ ಅಂತರ್ಗತ `GITHUB_TOKEN` ಅನ್ನು ಬಳಸುತ್ತದೆ. ನೀವು ಮ್ಯಾನುಯಲ್ ಆಗಿ ಪರ್ಸನಲ್ ಆಕ್ಸೆಸ್ ಟೋಕನ್ (PAT) ಅನ್ನು ರಚಿಸುವ ಅಗತ್ಯವಿಲ್ಲ, ಆದರೆ ಡೀಫಾಲ್ಟ್ ಟೋಕನ್‌ಗೆ ಸರಿಯಾದ ಅನುಮತಿಗಳಿವೆ ಎಂಬುದನ್ನು ನೀವು ಖಚಿತಪಡಿಸಿಕೊಳ್ಳಬೇಕು:

1. ನಿಮ್ಮ ರೆಪೊಸಿಟರಿಯ **Settings** -> **Actions** -> **General** ಗೆ ಹೋಗಿ.
2. ಕೆಳಗೆ ಸ್ಕ್ರಾಲ್ ಮಾಡಿ **Workflow permissions** ವಿಭಾಗಕ್ಕೆ ಹೋಗಿ.
3. **Read and write permissions** ಅನ್ನು ಆಯ್ಕೆಮಾಡಿ.
4. **Save** ಕ್ಲಿಕ್ ಮಾಡಿ.
5. ನಿಮ್ಮ ವರ್ಕ್‌ಫ್ಲೋ YAML ನಲ್ಲಿ, ಕೇವಲ `${{ secrets.GITHUB_TOKEN }}` ಅನ್ನು `github_token` ಇನ್‌ಪುಟ್‌ಗೆ ಪಾಸ್ ಮಾಡಿ (ಬಳಕೆಯ ಉದಾಹರಣೆಯಲ್ಲಿ ತೋರಿಸಿರುವಂತೆ).

## 📄 ಪರವಾನಗಿ (License)

ಈ ಪ್ರಾಜೆಕ್ಟ್ MIT ಲೈಸೆನ್ಸ್ ಅಡಿಯಲ್ಲಿ ಪರವಾನಗಿ ಪಡೆದಿದೆ - ಹೆಚ್ಚಿನ ವಿವರಗಳಿಗಾಗಿ [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) ಫೈಲ್ ಅನ್ನು ನೋಡಿ.