> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

En GitHub Action som automatiskt översätter din `README.md` till flera språk med hjälp av Gemini API. Den infogar på ett intelligent sätt en korslänkad språknavigeringsmeny i alla filer och kan antingen checka in ändringarna direkt eller skapa en Pull Request för granskning.

## 🚀 Funktioner
* **Flerspråkigt stöd:** Generera README-filer för flera språk i en och samma körning.
* **Autonavigering:** Infogar och underhåller automatiskt en standardmeny för språkväxling högst upp i dina filer (kan inaktiveras). AI:n formaterar den automatiskt!
* **Anpassad formatering:** Du kan ange en parameter för anpassad menystil så att AI:n formaterar språkväljaren exakt som du vill.
* **Spårning av tokens:** Matar ut statistik över Geminis tokenanvändning.

## 🛠 Användning

Skapa en arbetsflödesfil (t.ex. `.github/workflows/translate.yml`):

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

## 📥 Indata

| Indata | Krävs | Standard | Beskrivning |
| --- | --- | --- | --- |
| `api_key` | Ja |  | Din Google Gemini API-nyckel. |
| `github_token` | Ja |  | Standard GitHub-token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ja |  | Kommaseparerade målspråk (t.ex. `ru, es`). |
| `output_dir` | Nej | | Katalog för att spara översatta filer. Som standard används källfilens katalog. |
| `add_language_menu` | Nej | `true` | Sätt till `false` för att inaktivera automatisk generering av språkmenyn. |
| `menu_style` | Nej | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Den referensstil som AI:n använder när en ny språkmeny genereras. |
| `commit_message` | Nej | `docs: auto-translate README via Gemini` | Text som används för git commit-meddelandet. |
| `model` | Nej | `gemini-3.1-pro-preview` | Gemini-modellen som ska användas. |
| `source_file` | Nej | `README.md` | Basfilen som ska översättas. |

## 🔑 Hur man skaffar en Google Gemini API-nyckel

För att använda denna GitHub Action behöver du en gratis API-nyckel från Google AI Studio:

1. Gå till [Google AI Studio](https://aistudio.google.com/).
2. Logga in med ditt Google-konto.
3. Klicka på **Get API key** i den vänstra navigeringsmenyn.
4. Klicka på knappen **Create API key**.
5. Kopiera den genererade nyckeln.
6. Gå till ditt GitHub-kodarkiv -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klicka på **New repository secret**, namnge den `GEMINI_API_KEY`, klistra in din nyckel i fältet Secret och spara.

## 🔑 Hur man konfigurerar den inbyggda GitHub-tokenen

Denna åtgärd använder den inbyggda `GITHUB_TOKEN` för att pusha incheckningar (commits) eller skapa Pull Requests. Du behöver **inte** skapa en personlig åtkomsttoken (PAT) manuellt, men du **måste** säkerställa att standardtokenen har rätt behörigheter:

1. Gå till ditt kodarkivs **Settings** -> **Actions** -> **General**.
2. Rulla ner till avsnittet **Workflow permissions**.
3. Välj **Read and write permissions**.
4. Klicka på **Save**.
5. I din arbetsflödes-YAML skickar du helt enkelt `${{ secrets.GITHUB_TOKEN }}` till indatan `github_token` (som visas i användningsexemplet).

## 📄 Licens

Detta projekt är licensierat under MIT-licensen - se filen [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) för mer information.