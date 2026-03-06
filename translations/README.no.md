> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Oversetter

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

En GitHub Action som automatisk oversetter din `README.md` til flere språk ved hjelp av Gemini API. Den setter på en intelligent måte inn en krysslenket meny for språknavigasjon i alle filer, og kan enten kommitere endringene direkte eller opprette en Pull Request for gjennomgang.

## 🚀 Funksjoner
* **Støtte for flere språk:** Generer README-filer for flere språk i én enkelt kjøring.
* **Autonavigasjon:** Setter automatisk inn og vedlikeholder en standard meny for språkvalg øverst i filene dine (kan deaktiveres). AI formaterer den automatisk!
* **Egendefinert stil:** Du kan oppgi en parameter for egendefinert menystil slik at AI-en formaterer språkvelgeren akkurat slik du ønsker.
* **Sporing av tokens:** Viser bruksstatistikk for Gemini-tokens.

## 🛠 Bruk

Opprett en arbeidsflytfil (f.eks. `.github/workflows/translate.yml`):

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

## 📥 Inndata

| Inndata | Påkrevd | Standard | Beskrivelse |
| --- | --- | --- | --- |
| `api_key` | Ja |  | Din Google Gemini API-nøkkel. |
| `github_token` | Ja |  | Standard GitHub-token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ja |  | Kommaseparerte målspråk (f.eks. `ru, es`). |
| `output_dir` | Nei | | Katalog for lagring av oversatte filer. Standard er kildefilens katalog. |
| `add_language_menu` | Nei | `true` | Sett til `false` for å deaktivere automatisk generering av språkmenyen. |
| `menu_style` | Nei | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referansestilen AI-en bruker ved generering av en ny språkmeny. |
| `commit_message` | Nei | `docs: auto-translate README via Gemini` | Tekst som brukes for git commit-meldingen. |
| `model` | Nei | `gemini-3.1-pro-preview` | Gemini-modellen som skal brukes. |
| `source_file` | Nei | `README.md` | Grunnfilen som skal oversettes. |

## 🔑 Slik får du en Google Gemini API-nøkkel

For å bruke denne handlingen trenger du en gratis API-nøkkel fra Google AI Studio:

1. Gå til [Google AI Studio](https://aistudio.google.com/).
2. Logg inn med din Google-konto.
3. I navigasjonsmenyen til venstre, klikk på **Get API key**.
4. Klikk på **Create API key**-knappen.
5. Kopier den genererte nøkkelen.
6. Gå til ditt GitHub-repositorium -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klikk på **New repository secret**, gi den navnet `GEMINI_API_KEY`, lim inn nøkkelen din i Secret-feltet, og lagre.

## 🔑 Slik konfigurerer du standard GitHub-token

Denne handlingen bruker den innebygde `GITHUB_TOKEN` for å pushe commits eller opprette Pull Requests. Du trenger **ikke** å opprette et Personal Access Token (PAT) manuelt, men du **må** sørge for at standardtokenet har de riktige tillatelsene:

1. Gå til ditt repositoriums **Settings** -> **Actions** -> **General**.
2. Rull ned til seksjonen **Workflow permissions**.
3. Velg **Read and write permissions**.
4. Klikk på **Save**.
5. I din YAML-arbeidsflyt sender du ganske enkelt `${{ secrets.GITHUB_TOKEN }}` til inndatafeltet `github_token` (som vist i brukseksempelet).

## 📄 Lisens

Dette prosjektet er lisensiert under MIT-lisensen - se filen [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) for detaljer.