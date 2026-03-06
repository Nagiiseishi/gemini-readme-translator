> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Een GitHub Action die je `README.md` automatisch in meerdere talen vertaalt met behulp van de Gemini API. Het voegt op intelligente wijze een onderling gelinkt taalnavigatiemenu toe aan alle bestanden en kan wijzigingen direct committen of een Pull Request aanmaken voor beoordeling.

## 🚀 Functies
* **Ondersteuning voor meerdere talen:** Genereer README's voor meerdere talen in één run.
* **Auto-navigatie:** Voegt automatisch een standaard menu voor het wisselen van taal toe aan de bovenkant van je bestanden en houdt dit bij (kan worden uitgeschakeld). AI maakt het automatisch op!
* **Aangepaste opmaak:** Je kunt een parameter voor een aangepaste menustijl opgeven, zodat de AI de taalwisselaar precies opmaakt zoals jij wilt.

* **Token tracking:** Geeft statistieken over het tokengebruik van Gemini weer.

## 🛠 Gebruik

Maak een workflowbestand aan (bijv. `.github/workflows/translate.yml`):

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

## 📥 Invoerparameters

| Invoer | Vereist | Standaard | Beschrijving |
| --- | --- | --- | --- |
| `api_key` | Ja |  | Je Google Gemini API-sleutel. |
| `github_token` | Ja |  | Standaard GitHub-token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ja |  | Kommagescheiden doeltalen (bijv. `ru, es`). |
| `output_dir` | Nee | | Map om vertaalde bestanden op te slaan. Standaard is dit de map van het bronbestand. |
| `add_language_menu` | Nee | `true` | Stel in op `false` om het automatisch genereren van het taalmenu uit te schakelen. |
| `menu_style` | Nee | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | De referentiestijl die AI gebruikt bij het genereren van een nieuw taalmenu. |
| `commit_message` | Nee | `docs: auto-translate README via Gemini` | Tekst die wordt gebruikt voor het git commit-bericht. |
| `model` | Nee | `gemini-3.1-pro-preview` | Het te gebruiken Gemini-model. |
| `source_file` | Nee | `README.md` | Het basisbestand om te vertalen. |

## 🔑 Hoe je een Google Gemini API-sleutel kunt krijgen

Om deze action te gebruiken, heb je een gratis API-sleutel van Google AI Studio nodig:

1. Ga naar [Google AI Studio](https://aistudio.google.com/).
2. Log in met je Google-account.
3. Klik in het linkernavigatiemenu op **Get API key**.
4. Klik op de knop **Create API key**.
5. Kopieer de gegenereerde sleutel.
6. Ga naar je GitHub-repository -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klik op **New repository secret**, noem het `GEMINI_API_KEY`, plak je sleutel in het Secret-veld en sla op.

## 🔑 Hoe je het Standaard GitHub-token configureert

Deze action gebruikt het ingebouwde `GITHUB_TOKEN` om commits te pushen of Pull Requests aan te maken. Je hoeft **geen** Personal Access Token (PAT) handmatig aan te maken, maar je **moet** er wel voor zorgen dat het standaardtoken de juiste machtigingen heeft:

1. Ga naar je repository **Settings** -> **Actions** -> **General**.
2. Scrol naar beneden naar de sectie **Workflow permissions**.
3. Selecteer **Read and write permissions**.
4. Klik op **Save**.
5. In je workflow YAML geef je eenvoudig `${{ secrets.GITHUB_TOKEN }}` door aan de `github_token` invoer (zoals te zien in het gebruiksvoorbeeld).

## 📄 Licentie

Dit project is gelicentieerd onder de MIT-licentie - zie het [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) bestand voor details.