> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action koji automatski prevodi vaš `README.md` na više jezika koristeći Gemini API. Inteligentno ubacuje međusobno povezani navigacijski izbornik za jezike u sve datoteke i može izravno izvršiti promjene (commit) ili stvoriti zahtjev za povlačenjem (Pull Request) za pregled.

## 🚀 Značajke
* **Višejezična podrška:** Generirajte README datoteke za više jezika u jednom pokretanju.
* **Automatska navigacija:** Automatski umeće i održava standardni izbornik za promjenu jezika na vrhu vaših datoteka (može se onemogućiti). UI ga automatski stilizira!
* **Prilagođeno stiliziranje:** Možete unijeti prilagođeni parametar stila izbornika kako bi UI formatirao izmjenjivač jezika točno onako kako želite.

* **Praćenje tokena:** Ispisuje statistiku korištenja Gemini tokena.

## 🛠 Korištenje

Stvorite datoteku tijeka rada (npr. `.github/workflows/translate.yml`):

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

| Parametar | Obavezno | Zadano | Opis |
| --- | --- | --- | --- |
| `api_key` | Da |  | Vaš Google Gemini API ključ. |
| `github_token` | Da |  | Standardni GitHub token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Da |  | Ciljani jezici odvojeni zarezom (npr. `ru, es`). |
| `output_dir` | Ne | | Direktorij za spremanje prevedenih datoteka. Zadano je direktorij izvorne datoteke. |
| `add_language_menu` | Ne | `true` | Postavite na `false` da biste onemogućili automatsko generiranje jezičnog izbornika. |
| `menu_style` | Ne | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referentni stil koji UI koristi pri generiranju novog jezičnog izbornika. |
| `commit_message` | Ne | `docs: auto-translate README via Gemini` | Tekst koji se koristi za git commit poruku. |
| `model` | Ne | `gemini-3.1-pro-preview` | Gemini model koji se koristi. |
| `source_file` | Ne | `README.md` | Osnovna datoteka za prijevod. |

## 🔑 Kako dobiti Google Gemini API ključ

Za korištenje ove akcije potreban vam je besplatan API ključ iz Google AI Studija:

1. Idite na [Google AI Studio](https://aistudio.google.com/).
2. Prijavite se svojim Google računom.
3. U lijevom navigacijskom izborniku kliknite na **Get API key**.
4. Kliknite gumb **Create API key**.
5. Kopirajte generirani ključ.
6. Idite na svoj GitHub repozitorij -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Kliknite **New repository secret**, nazovite ga `GEMINI_API_KEY`, zalijepite svoj ključ u polje Secret i spremite.

## 🔑 Kako konfigurirati Standardni GitHub token

Ova akcija koristi ugrađeni `GITHUB_TOKEN` za slanje (push) promjena (commita) ili stvaranje zahtjeva za povlačenjem (Pull Requests). **Ne morate** ručno stvarati osobni pristupni token (PAT), ali **morate** osigurati da zadani token ima ispravne dozvole:

1. Idite na **Settings** -> **Actions** -> **General** u svom repozitoriju.
2. Pomaknite se dolje do odjeljka **Workflow permissions**.
3. Odaberite **Read and write permissions**.
4. Kliknite **Save**.
5. U svom YAML tijeku rada jednostavno proslijedite `${{ secrets.GITHUB_TOKEN }}` u ulazni parametar `github_token` (kao što je prikazano u primjeru korištenja).

## 📄 Licenca

Ovaj projekt je licenciran pod MIT licencom - pogledajte datoteku [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) za detalje.