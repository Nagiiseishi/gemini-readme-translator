> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Egy GitHub Action, amely a Gemini API segítségével automatikusan lefordítja a `README.md` fájlodat több nyelvre. Intelligensen beilleszt egy keresztlinkekkel ellátott nyelvi navigációs menüt az összes fájlba, és képes a változtatásokat közvetlenül kommitálni, vagy Pull Requestet nyitni ellenőrzés céljából.

## 🚀 Funkciók
* **Többnyelvű támogatás:** Generálj README fájlokat több nyelven egyetlen futtatással.
* **Automatikus navigáció:** Automatikusan beszúr és karbantart egy szabványos nyelvváltó menüt a fájljaid tetején (kikapcsolható). Az AI automatikusan formázza!
* **Egyéni formázás:** Megadhatsz egy egyéni menüstílus paramétert, így az AI pontosan úgy formázza a nyelvváltót, ahogyan szeretnéd.
* **Tokenkövetés:** Megjeleníti a Gemini tokenhasználati statisztikákat.

## 🛠 Használat

Hozz létre egy munkafolyamat (workflow) fájlt (pl. `.github/workflows/translate.yml`):

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

## 📥 Bemenetek

| Bemenet | Kötelező | Alapértelmezett | Leírás |
| --- | --- | --- | --- |
| `api_key` | Igen |  | A Google Gemini API kulcsod. |
| `github_token` | Igen |  | Szabványos GitHub token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Igen |  | Vesszővel elválasztott célnyelvek (pl. `ru, es`). |
| `output_dir` | Nem | | Könyvtár a lefordított fájlok mentéséhez. Alapértelmezés szerint a forrásfájl könyvtára. |
| `add_language_menu` | Nem | `true` | Állítsd `false` értékre a nyelvi menü automatikus generálásának letiltásához. |
| `menu_style` | Nem | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | A referenciastílus, amelyet az AI az új nyelvi menü generálásakor használ. |
| `commit_message` | Nem | `docs: auto-translate README via Gemini` | A git kommit üzenethez használt szöveg. |
| `model` | Nem | `gemini-3.1-pro-preview` | A használni kívánt Gemini modell. |
| `source_file` | Nem | `README.md` | A lefordítandó alapfájl. |

## 🔑 Hogyan szerezz Google Gemini API kulcsot

Ennek az action-nek a használatához egy ingyenes API kulcsra van szükséged a Google AI Studióból:

1. Látogass el a [Google AI Studio](https://aistudio.google.com/) oldalra.
2. Jelentkezz be a Google fiókoddal.
3. A bal oldali navigációs menüben kattints a **Get API key** gombra.
4. Kattints a **Create API key** gombra.
5. Másold ki a generált kulcsot.
6. Nyisd meg a GitHub repódat -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Kattints a **New repository secret** gombra, nevezd el `GEMINI_API_KEY`-nek, illeszd be a kulcsodat a Secret mezőbe, és mentsd el.

## 🔑 A szabványos GitHub Token konfigurálása

Ez az action a beépített `GITHUB_TOKEN`-t használja a kommitok pusholására vagy a Pull Requestek létrehozására. **Nem** kell manuálisan Personal Access Token-t (PAT) létrehoznod, de gondoskodnod **kell** arról, hogy az alapértelmezett token megfelelő jogosultságokkal rendelkezzen:

1. Lépj a repód **Settings** -> **Actions** -> **General** menüjébe.
2. Görgess le a **Workflow permissions** szakaszhoz.
3. Válaszd a **Read and write permissions** lehetőséget.
4. Kattints a **Save** gombra.
5. A workflow YAML fájlodban egyszerűen add át a `${{ secrets.GITHUB_TOKEN }}`-t a `github_token` bemenetnek (ahogyan a használati példában is látható).

## 📄 Licenc

Ez a projekt az MIT Licenc alatt áll - a részletekért lásd a [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) fájlt.