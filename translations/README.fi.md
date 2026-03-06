> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, joka kääntää `README.md`-tiedostosi automaattisesti useille kielille Gemini API:n avulla. Se lisää älykkäästi ristiinlinkitetyn kielivalikon kaikkiin tiedostoihin ja voi joko viedä muutokset (commit) suoraan tai luoda Pull Request -pyynnön tarkistettavaksi.

## 🚀 Ominaisuudet
* **Monikielinen tuki:** Luo README-tiedostot useille kielille yhdellä ajolla.
* **Automaattinen navigointi:** Lisää ja ylläpitää automaattisesti vakiomuotoista kielivalikkoa tiedostojen yläosassa (voidaan poistaa käytöstä). Tekoäly tyylittelee sen automaattisesti!
* **Mukautettava tyyli:** Voit antaa mukautetun valikkotyyliparametrin, jotta tekoäly muotoilee kielivalikon juuri haluamallasi tavalla.
* **Tokenien seuranta:** Tulostaa Geminin tokenien käyttötilastot.

## 🛠 Käyttö

Luo työnkulkutiedosto (esim. `.github/workflows/translate.yml`):

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

## 📥 Syötteet

| Syöte | Pakollinen | Oletus | Kuvaus |
| --- | --- | --- | --- |
| `api_key` | Kyllä |  | Google Gemini API -avaimesi. |
| `github_token` | Kyllä |  | Vakio-GitHub-tunnus (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Kyllä |  | Pilkulla erotetut kohdekielet (esim. `ru, es`). |
| `output_dir` | Ei | | Hakemisto, johon käännetyt tiedostot tallennetaan. Oletuksena lähdetiedoston hakemisto. |
| `add_language_menu` | Ei | `true` | Aseta arvoon `false` poistaaksesi kielivalikon automaattisen luonnin käytöstä. |
| `menu_style` | Ei | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Viitetyyli, jota tekoäly käyttää luodessaan uutta kielivalikkoa. |
| `commit_message` | Ei | `docs: auto-translate README via Gemini` | Git-kommitin viestinä käytettävä teksti. |
| `model` | Ei | `gemini-3.1-pro-preview` | Käytettävä Gemini-malli. |
| `source_file` | Ei | `README.md` | Käännettävä perustiedosto. |

## 🔑 Miten saada Google Gemini API -avain

Tämän toiminnon käyttämiseksi tarvitset ilmaisen API-avaimen Google AI Studiolta:

1. Siirry osoitteeseen [Google AI Studio](https://aistudio.google.com/).
2. Kirjaudu sisään Google-tililläsi.
3. Napsauta vasemmassa navigointivalikossa **Get API key**.
4. Napsauta **Create API key** -painiketta.
5. Kopioi luotu avain.
6. Siirry GitHub-repositoriosi kohtaan **Settings** -> **Secrets and variables** -> **Actions**.
7. Napsauta **New repository secret**, nimeä se `GEMINI_API_KEY`, liitä avaimesi Secret-kenttään ja tallenna.

## 🔑 Vakio-GitHub-tunnuksen (GITHUB_TOKEN) määrittäminen

Tämä toiminto käyttää sisäänrakennettua `GITHUB_TOKEN`-tunnusta muutosten viemiseen (push) tai Pull Request -pyyntöjen luomiseen. Sinun **ei** tarvitse luoda henkilökohtaista käyttöoikeustunnusta (Personal Access Token, PAT) manuaalisesti, mutta sinun **täytyy** varmistaa, että oletustunnuksella on oikeat käyttöoikeudet:

1. Siirry repositoriosi kohtaan **Settings** -> **Actions** -> **General**.
2. Vieritä alas kohtaan **Workflow permissions**.
3. Valitse **Read and write permissions**.
4. Napsauta **Save**.
5. Välitä työnkulun YAML-tiedostossa pelkkä `${{ secrets.GITHUB_TOKEN }}` `github_token`-syötteelle (kuten käyttöesimerkissä on näytetty).

## 📄 Lisenssi

Tämä projekti on lisensoitu MIT-lisenssillä - katso lisätietoja tiedostosta [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).