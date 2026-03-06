> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHubi Action, mis tõlgib sinu `README.md` faili Gemini API abil automaatselt mitmesse keelde. See lisab nutikalt kõikidesse failidesse ristviidetega keele navigeerimismenüü ning võib muudatused otse commitida või luua ülevaatamiseks Pull Request'i.

## 🚀 Omadused
* **Mitme keele tugi:** Loo README failid mitmes keeles ühe käivitamisega.
* **Automaatne navigeerimine:** Sisestab ja haldab failide ülaosas automaatselt standardset keelevahetusmenüüd (saab välja lülitada). Tehisintellekt (AI) kujundab selle automaatselt!
* **Kohandatud kujundus:** Saad määrata kohandatud menüüstiili parameetri, et AI vormindaks keelevahetaja täpselt sinu soovi järgi.
* **Tokenite jälgimine:** Väljastab Gemini tokenite kasutusstatistika.

## 🛠 Kasutamine

Loo töövoo fail (nt `.github/workflows/translate.yml`):

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

## 📥 Sisendid

| Sisend | Nõutud | Vaikimisi | Kirjeldus |
| --- | --- | --- | --- |
| `api_key` | Jah |  | Sinu Google Gemini API võti. |
| `github_token` | Jah |  | Standardne GitHubi token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Jah |  | Komadega eraldatud sihtkeeled (nt `ru, es`). |
| `output_dir` | Ei | | Kataloog tõlgitud failide salvestamiseks. Vaikimisi lähtefaili kataloog. |
| `add_language_menu` | Ei | `true` | Määra väärtuseks `false`, et keelata keelemenüü automaatne loomine. |
| `menu_style` | Ei | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Viitestiil, mida AI uue keelemenüü loomisel kasutab. |
| `commit_message` | Ei | `docs: auto-translate README via Gemini` | Tekst, mida kasutatakse giti commiti sõnumina. |
| `model` | Ei | `gemini-3.1-pro-preview` | Kasutatav Gemini mudel. |
| `source_file` | Ei | `README.md` | Tõlgitav alusfail. |

## 🔑 Kuidas saada Google Gemini API võtit

Selle Actioni kasutamiseks vajad tasuta API võtit Google AI Studiost:

1. Mine [Google AI Studiosse](https://aistudio.google.com/).
2. Logi sisse oma Google'i kontoga.
3. Klõpsa vasakpoolses navigeerimismenüüs nupule **Get API key**.
4. Klõpsa nupule **Create API key**.
5. Kopeeri loodud võti.
6. Mine oma GitHubi hoidlasse -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klõpsa **New repository secret**, pane nimeks `GEMINI_API_KEY`, kleebi oma võti lahtrisse Secret ja salvesta.

## 🔑 Kuidas seadistada standardset GitHubi tokenit

See Action kasutab sisseehitatud `GITHUB_TOKEN`it, et edastada commite või luua Pull Request'e. Sa **ei pea** käsitsi looma Personal Access Tokenit (PAT), kuid sa **pead** veenduma, et vaiketokenil on õiged õigused:

1. Mine oma hoidlas **Settings** -> **Actions** -> **General**.
2. Keri alla jaotiseni **Workflow permissions**.
3. Vali **Read and write permissions**.
4. Klõpsa **Save**.
5. Oma töövoo YAML-failis anna lihtsalt `${{ secrets.GITHUB_TOKEN }}` edasi sisendile `github_token` (nagu on näidatud kasutamise näites).

## 📄 Litsents

See projekt on litsentsitud MIT litsentsi all - vaata täpsemat teavet failist [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).