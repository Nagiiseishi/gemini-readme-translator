> 🌐 **Jazyky:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, která automaticky překládá váš `README.md` do více jazyků pomocí Gemini API. Inteligentně vkládá křížově odkazované navigační menu jazyků do všech souborů a může změny buď přímo commitnout, nebo vytvořit Pull Request ke kontrole.

## 🚀 Funkce
* **Podpora více jazyků:** Generování README pro více jazyků v jednom běhu.
* **Automatická navigace:** Automaticky vkládá a udržuje standardní menu pro přepínání jazyků v horní části vašich souborů (lze vypnout). Umělá inteligence jej automaticky nastyluje!
* **Vlastní stylizace:** Můžete poskytnout parametr pro vlastní styl menu, aby umělá inteligence zformátovala přepínač jazyků přesně podle vašich představ.
* **Sledování tokenů:** Vypisuje statistiky využití tokenů Gemini.

## 🛠 Použití

Vytvořte soubor workflow (např. `.github/workflows/translate.yml`):

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

| Vstup | Vyžadováno | Výchozí | Popis |
| --- | --- | --- | --- |
| `api_key` | Ano |  | Váš klíč k Google Gemini API. |
| `github_token` | Ano |  | Standardní GitHub token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ano |  | Cílové jazyky oddělené čárkou (např. `ru, es`). |
| `output_dir` | Ne | | Adresář pro uložení přeložených souborů. Výchozí je adresář zdrojového souboru. |
| `add_language_menu` | Ne | `true` | Nastavte na `false` pro zakázání automatického generování jazykového menu. |
| `menu_style` | Ne | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referenční styl, který AI použije při generování nového jazykového menu. |
| `commit_message` | Ne | `docs: auto-translate README via Gemini` | Text použitý pro zprávu git commitu. |
| `model` | Ne | `gemini-3.1-pro-preview` | Model Gemini, který se má použít. |
| `source_file` | Ne | `README.md` | Základní soubor k překladu. |

## 🔑 Jak získat Google Gemini API klíč

Pro použití této akce potřebujete bezplatný API klíč z Google AI Studio:

1. Přejděte do [Google AI Studio](https://aistudio.google.com/).
2. Přihlaste se pomocí svého účtu Google.
3. V levém navigačním menu klikněte na **Get API key**.
4. Klikněte na tlačítko **Create API key**.
5. Zkopírujte vygenerovaný klíč.
6. Přejděte do svého repozitáře na GitHubu -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klikněte na **New repository secret**, pojmenujte jej `GEMINI_API_KEY`, vložte svůj klíč do pole Secret a uložte.

## 🔑 Jak nakonfigurovat standardní GitHub Token

Tato akce používá vestavěný `GITHUB_TOKEN` k nahrávání commitů (push) nebo vytváření Pull Requestů. **Nemusíte** ručně vytvářet Personal Access Token (PAT), ale **musíte** zajistit, aby měl výchozí token správná oprávnění:

1. Přejděte v repozitáři do **Settings** -> **Actions** -> **General**.
2. Sjeďte dolů do sekce **Workflow permissions**.
3. Vyberte **Read and write permissions**.
4. Klikněte na **Save**.
5. Ve svém YAML souboru workflow jednoduše předejte `${{ secrets.GITHUB_TOKEN }}` do vstupu `github_token` (jak je ukázáno v příkladu použití).

## 📄 Licence

Tento projekt je licencován pod licencí MIT - podrobnosti naleznete v souboru [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).