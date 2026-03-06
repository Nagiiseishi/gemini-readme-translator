> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action koji automatski prevodi vaš `README.md` na više jezika koristeći Gemini API. Pametno ubacuje međusobno povezan meni za navigaciju po jezicima u sve fajlove i može ili direktno komitovati izmene ili kreirati Pull Request za pregled.

## 🚀 Funkcionalnosti
* **Višejezična podrška:** Generiše README fajlove za više jezika u jednom pokretanju.
* **Auto-navigacija:** Automatski ubacuje i održava standardni meni za promenu jezika na vrhu vaših fajlova (može se onemogućiti). AI ga automatski stilizuje!
* **Prilagođeno stilizovanje:** Možete proslediti parametar za prilagođeni stil menija kako bi AI formatirala prebacivač jezika tačno onako kako želite.
* **Praćenje tokena:** Prikazuje statistiku korišćenja Gemini tokena.

## 🛠 Upotreba

Kreirajte workflow fajl (npr. `.github/workflows/translate.yml`):

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

## 📥 Ulazni parametri

| Parametar | Obavezno | Podrazumevano | Opis |
| --- | --- | --- | --- |
| `api_key` | Da |  | Vaš Google Gemini API ključ. |
| `github_token` | Da |  | Standardni GitHub token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Da |  | Ciljni jezici odvojeni zarezom (npr. `ru, es`). |
| `output_dir` | Ne | | Direktorijum za čuvanje prevedenih fajlova. Podrazumevano je direktorijum izvornog fajla. |
| `add_language_menu` | Ne | `true` | Postavite na `false` da biste onemogućili auto-generisanje jezičkog menija. |
| `menu_style` | Ne | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referentni stil koji AI koristi pri generisanju novog jezičkog menija. |
| `commit_message` | Ne | `docs: auto-translate README via Gemini` | Tekst koji se koristi za git commit poruku. |
| `model` | Ne | `gemini-3.1-pro-preview` | Gemini model koji se koristi. |
| `source_file` | Ne | `README.md` | Osnovni fajl koji se prevodi. |

## 🔑 Kako da dobijete Google Gemini API ključ

Da biste koristili ovu akciju, potreban vam je besplatan API ključ iz Google AI Studio-a:

1. Idite na [Google AI Studio](https://aistudio.google.com/).
2. Prijavite se sa vašim Google nalogom.
3. U levom navigacionom meniju, kliknite na **Get API key**.
4. Kliknite na dugme **Create API key**.
5. Kopirajte generisani ključ.
6. Idite u vaš GitHub repozitorijum -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Kliknite na **New repository secret**, nazovite ga `GEMINI_API_KEY`, nalepite vaš ključ u polje Secret i sačuvajte.

## 🔑 Kako konfigurisati standardni GitHub token

Ova akcija koristi ugrađeni `GITHUB_TOKEN` za slanje komita (push) ili kreiranje Pull Request-ova. **Ne morate** ručno da kreirate Personal Access Token (PAT), ali **morate** da se uverite da podrazumevani token ima ispravne dozvole:

1. Idite u **Settings** vašeg repozitorijuma -> **Actions** -> **General**.
2. Skrolujte dole do sekcije **Workflow permissions**.
3. Izaberite **Read and write permissions**.
4. Kliknite na **Save**.
5. U vašem YAML workflow-u, jednostavno prosledite `${{ secrets.GITHUB_TOKEN }}` u `github_token` ulazni parametar (kao što je prikazano u primeru upotrebe).

## 📄 Licenca

Ovaj projekat je licenciran pod MIT licencom - pogledajte [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) fajl za detalje.