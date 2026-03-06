> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Prekladač Gemini README

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub akcia, ktorá automaticky prekladá váš súbor `README.md` do viacerých jazykov pomocou Gemini API. Inteligentne vkladá prepojené jazykové navigačné menu do všetkých súborov a dokáže zmeny buď priamo commitnúť, alebo vytvoriť Pull Request na revíziu.

## 🚀 Funkcie
* **Podpora viacerých jazykov:** Generovanie súborov README pre viacero jazykov v jednom behu.
* **Automatická navigácia:** Automaticky vkladá a spravuje štandardné menu na prepínanie jazykov na vrchu vašich súborov (dá sa zakázať). AI ho štýluje automaticky!
* **Vlastné štýlovanie:** Môžete zadať parameter pre vlastný štýl menu, takže AI naformátuje prepínač jazykov presne tak, ako chcete.
* **Sledovanie tokenov:** Zobrazuje štatistiky využitia tokenov Gemini.

## 🛠 Použitie

Vytvorte súbor pracovného postupu (workflow) (napr. `.github/workflows/translate.yml`):

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

## 📥 Vstupy

| Vstup | Povinné | Predvolené | Popis |
| --- | --- | --- | --- |
| `api_key` | Áno |  | Váš kľúč Google Gemini API. |
| `github_token` | Áno |  | Štandardný GitHub token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Áno |  | Cieľové jazyky oddelené čiarkou (napr. `ru, es`). |
| `output_dir` | Nie | | Adresár na uloženie preložených súborov. Predvolený je adresár zdrojového súboru. |
| `add_language_menu` | Nie | `true` | Nastavte na `false` pre zakázanie automatického generovania jazykového menu. |
| `menu_style` | Nie | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referenčný štýl, ktorý AI používa pri generovaní nového jazykového menu. |
| `commit_message` | Nie | `docs: auto-translate README via Gemini` | Text použitý pre správu git commitu. |
| `model` | Nie | `gemini-3.1-pro-preview` | Gemini model, ktorý sa má použiť. |
| `source_file` | Nie | `README.md` | Základný súbor na preklad. |

## 🔑 Ako získať kľúč Google Gemini API

Pre použitie tejto akcie potrebujete bezplatný API kľúč z Google AI Studio:

1. Prejdite na [Google AI Studio](https://aistudio.google.com/).
2. Prihláste sa pomocou svojho účtu Google.
3. V ľavom navigačnom menu kliknite na **Get API key**.
4. Kliknite na tlačidlo **Create API key**.
5. Skopírujte vygenerovaný kľúč.
6. Prejdite do svojho repozitára na GitHub-e -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Kliknite na **New repository secret**, pomenujte ho `GEMINI_API_KEY`, vložte svoj kľúč do poľa Secret a uložte.

## 🔑 Ako nakonfigurovať štandardný GitHub Token

Táto akcia používa vstavaný `GITHUB_TOKEN` na nahrávanie (push) commitov alebo vytváranie Pull Requestov. **Nemusíte** ručne vytvárať Personal Access Token (PAT), ale **musíte** zabezpečiť, aby mal predvolený token správne oprávnenia:

1. Prejdite v repozitári do **Settings** -> **Actions** -> **General**.
2. Prejdite nižšie na sekciu **Workflow permissions**.
3. Vyberte **Read and write permissions**.
4. Kliknite na **Save**.
5. Vo vašom YAML súbore pre workflow jednoducho odovzdajte `${{ secrets.GITHUB_TOKEN }}` vstupu `github_token` (ako je ukázané v príklade použitia).

## 📄 Licencia

Tento projekt je licencovaný pod MIT licenciou - pozrite si súbor [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) pre viac podrobností.