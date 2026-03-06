> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README tulkotājs

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, kas automātiski tulko jūsu `README.md` vairākās valodās, izmantojot Gemini API. Tā viedi ievieto savstarpēji saistītu valodu navigācijas izvēlni visos failos un var vai nu tieši apstiprināt (commit) izmaiņas, vai izveidot Pull Request pārskatīšanai.

## 🚀 Funkcijas
* **Vairāku valodu atbalsts:** Ģenerējiet README failus vairākām valodām vienā piegājienā.
* **Automātiskā navigācija:** Automātiski ievieto un uztur standarta valodu pārslēdzēja izvēlni jūsu failu augšpusē (to var atspējot). AI to noformē automātiski!
* **Pielāgojams noformējums:** Varat norādīt pielāgotu izvēlnes stila parametru, lai AI noformētu valodu pārslēdzēju tieši tā, kā vēlaties.
* **Marķieru (Token) izsekošana:** Izvada Gemini marķieru lietojuma statistiku.

## 🛠 Lietošana

Izveidojiet darbplūsmas failu (piemēram, `.github/workflows/translate.yml`):

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

## 📥 Ievades parametri

| Ievade | Obligāts | Noklusējums | Apraksts |
| --- | --- | --- | --- |
| `api_key` | Jā |  | Jūsu Google Gemini API atslēga. |
| `github_token` | Jā |  | Standarta GitHub marķieris (token) (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Jā |  | Ar komatiem atdalītas mērķa valodas (piemēram, `ru, es`). |
| `output_dir` | Nē | | Direktorijs tulkoto failu saglabāšanai. Pēc noklusējuma tā ir avota faila direktorija. |
| `add_language_menu` | Nē | `true` | Iestatiet kā `false`, lai atspējotu valodu izvēlnes automātisko ģenerēšanu. |
| `menu_style` | Nē | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Atsauces stils, ko AI izmanto, ģenerējot jaunu valodu izvēlni. |
| `commit_message` | Nē | `docs: auto-translate README via Gemini` | Teksts, ko izmanto git apstiprinājuma (commit) ziņojumam. |
| `model` | Nē | `gemini-3.1-pro-preview` | Izmantojamais Gemini modelis. |
| `source_file` | Nē | `README.md` | Bāzes fails, kuru tulkot. |

## 🔑 Kā iegūt Google Gemini API atslēgu

Lai izmantotu šo darbību (action), jums ir nepieciešama bezmaksas API atslēga no Google AI Studio:

1. Dodieties uz [Google AI Studio](https://aistudio.google.com/).
2. Pierakstieties ar savu Google kontu.
3. Kreisajā navigācijas izvēlnē noklikšķiniet uz **Get API key**.
4. Noklikšķiniet uz pogas **Create API key**.
5. Nokopējiet ģenerēto atslēgu.
6. Dodieties uz savu GitHub repozitoriju -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Noklikšķiniet uz **New repository secret**, nosauciet to par `GEMINI_API_KEY`, ielīmējiet atslēgu laukā Secret un saglabājiet.

## 🔑 Kā konfigurēt standarta GitHub marķieri (Token)

Šī darbība izmanto iebūvēto `GITHUB_TOKEN`, lai nosūtītu apstiprinājumus (commits) vai izveidotu Pull Request. Jums **nav** manuāli jāizveido Personal Access Token (PAT), bet jums **ir jānodrošina**, ka noklusējuma marķierim ir pareizās atļaujas:

1. Dodieties uz sava repozitorija **Settings** -> **Actions** -> **General**.
2. Ritiniet uz leju līdz sadaļai **Workflow permissions**.
3. Atlasiet **Read and write permissions**.
4. Noklikšķiniet uz **Save**.
5. Savā darbplūsmas YAML failā vienkārši nododiet `${{ secrets.GITHUB_TOKEN }}` ievadei `github_token` (kā parādīts lietošanas piemērā).

## 📄 Licence

Šis projekts ir licencēts saskaņā ar MIT licenci - sīkāku informāciju skatiet failā [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).