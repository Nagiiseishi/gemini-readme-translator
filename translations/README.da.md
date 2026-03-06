> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

En GitHub Action, der automatisk oversætter din `README.md` til flere sprog ved hjælp af Gemini API'en. Den indlejrer intelligent en krydslinket sprognavigationsmenu i alle filer og kan enten foretage commits direkte eller oprette en Pull Request til gennemsyn.

## 🚀 Funktioner
* **Flersproget understøttelse:** Generer README'er på flere sprog i en enkelt kørsel.
* **Auto-navigation:** Indsætter og vedligeholder automatisk en standard sprogskiftermenu øverst i dine filer (kan deaktiveres). AI styler det automatisk!
* **Brugerdefineret styling:** Du kan angive en brugerdefineret parameter til menustilen, så AI'en formaterer sprogskifteren præcis, som du ønsker det.
* **Token-sporing:** Viser statistik for Gemini token-forbrug.

## 🛠 Brug

Opret en workflow-fil (f.eks. `.github/workflows/translate.yml`):

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

## 📥 Input

| Input | Påkrævet | Standard | Beskrivelse |
| --- | --- | --- | --- |
| `api_key` | Ja |  | Din Google Gemini API-nøgle. |
| `github_token` | Ja |  | Standard GitHub-token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ja |  | Kommaadskilte målsprog (f.eks. `ru, es`). |
| `output_dir` | Nej | | Mappe til at gemme de oversatte filer. Som standard kildefilens mappe. |
| `add_language_menu` | Nej | `true` | Sæt til `false` for at deaktivere automatisk generering af sprogmenuen. |
| `menu_style` | Nej | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referencestilen, som AI'en bruger, når den genererer en ny sprogmenu. |
| `commit_message` | Nej | `docs: auto-translate README via Gemini` | Tekst der bruges til git commit-beskeden. |
| `model` | Nej | `gemini-3.1-pro-preview` | Den Gemini-model der skal bruges. |
| `source_file` | Nej | `README.md` | Basisfilen der skal oversættes. |

## 🔑 Sådan får du en Google Gemini API-nøgle

For at bruge denne action, skal du have en gratis API-nøgle fra Google AI Studio:

1. Gå til [Google AI Studio](https://aistudio.google.com/).
2. Log ind med din Google-konto.
3. I den venstre navigationsmenu, klik på **Get API key**.
4. Klik på knappen **Create API key**.
5. Kopiér den genererede nøgle.
6. Gå til dit GitHub-repository -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klik på **New repository secret**, navngiv den `GEMINI_API_KEY`, indsæt din nøgle i Secret-feltet, og gem.

## 🔑 Sådan konfigureres standard GitHub-tokenet

Denne action bruger det indbyggede `GITHUB_TOKEN` til at pushe commits eller oprette Pull Requests. Du behøver **ikke** at oprette et Personal Access Token (PAT) manuelt, men du **skal** sikre dig, at standardtokenet har de korrekte tilladelser:

1. Gå til dit repositorys **Settings** -> **Actions** -> **General**.
2. Rul ned til afsnittet **Workflow permissions**.
3. Vælg **Read and write permissions**.
4. Klik på **Save**.
5. I din workflow YAML skal du blot videregive `${{ secrets.GITHUB_TOKEN }}` til `github_token` inputtet (som vist i brugseksemplet).

## 📄 Licens

Dette projekt er licenseret under MIT-licensen - se filen [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) for detaljer.