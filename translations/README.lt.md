> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README vertėjas

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action veiksmas, kuris automatiškai išverčia jūsų `README.md` į kelias kalbas naudojant Gemini API. Jis išmaniai įterpia susietą kalbų naršymo meniu į visus failus ir gali tiesiogiai pateikti pakeitimus („commit“) arba sukurti peržiūrai skirtą „Pull Request“.

## 🚀 Funkcijos
* **Kelių kalbų palaikymas:** Vienu paleidimu sugeneruokite README failus keliomis kalbomis.
* **Automatinis naršymas:** Automatiškai įterpia ir palaiko standartinį kalbos perjungimo meniu jūsų failų viršuje (galima išjungti). AI jį suformatuoja automatiškai!
* **Tinkintas stilius:** Galite pateikti tinkintą meniu stiliaus parametrą, kad AI suformatuotų kalbos perjungiklį tiksliai taip, kaip norite.
* **Žetonų („Token“) stebėjimas:** Išveda Gemini žetonų naudojimo statistiką.

## 🛠 Naudojimas

Sukurkite darbo eigos failą (pvz., `.github/workflows/translate.yml`):

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

## 📥 Įvestys

| Įvestis | Privaloma | Numatytoji reikšmė | Aprašymas |
| --- | --- | --- | --- |
| `api_key` | Taip |  | Jūsų Google Gemini API raktas. |
| `github_token` | Taip |  | Standartinis GitHub žetonas (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Taip |  | Kableliais atskirtos tikslinės kalbos (pvz., `ru, es`). |
| `output_dir` | Ne | | Katalogas išverstiems failams išsaugoti. Numatytoji reikšmė yra šaltinio failo katalogas. |
| `add_language_menu` | Ne | `true` | Nustatykite `false`, kad išjungtumėte automatinį kalbų meniu generavimą. |
| `menu_style` | Ne | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Etaloninis stilius, kurį AI naudoja generuodamas naują kalbų meniu. |
| `commit_message` | Ne | `docs: auto-translate README via Gemini` | Tekstas, naudojamas git pakeitimų („commit“) pranešimui. |
| `model` | Ne | `gemini-3.1-pro-preview` | Naudojamas Gemini modelis. |
| `source_file` | Ne | `README.md` | Pagrindinis failas, kurį reikia išversti. |

## 🔑 Kaip gauti Google Gemini API raktą

Norėdami naudoti šį veiksmą, turite gauti nemokamą API raktą iš „Google AI Studio“:

1. Eikite į [Google AI Studio](https://aistudio.google.com/).
2. Prisijunkite su savo Google paskyra.
3. Kairiajame naršymo meniu spustelėkite **Get API key**.
4. Spustelėkite mygtuką **Create API key**.
5. Nukopijuokite sugeneruotą raktą.
6. Eikite į savo GitHub repozitoriją -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Spustelėkite **New repository secret**, pavadinkite ją `GEMINI_API_KEY`, įklijuokite savo raktą į laukelį „Secret“ ir išsaugokite.

## 🔑 Kaip sukonfigūruoti standartinį GitHub žetoną

Šis veiksmas naudoja įmontuotą `GITHUB_TOKEN`, kad pateiktų pakeitimus („push commits“) arba sukurtų „Pull Request“. Jums **nereikia** rankiniu būdu kurti asmeninio prieigos žetono (PAT), bet jūs **privalote** užtikrinti, kad numatytasis žetonas turi tinkamus leidimus:

1. Eikite į savo repozitorijos **Settings** -> **Actions** -> **General**.
2. Slinkite žemyn iki skilties **Workflow permissions**.
3. Pasirinkite **Read and write permissions**.
4. Spustelėkite **Save**.
5. Savo darbo eigos YAML faile tiesiog perduokite `${{ secrets.GITHUB_TOKEN }}` į `github_token` įvestį (kaip parodyta naudojimo pavyzdyje).

## 📄 Licencija

Šis projektas yra licencijuotas pagal MIT licenciją - daugiau informacijos rasite [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) faile.