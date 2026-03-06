> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub akcija (Action), ki z uporabo Gemini API-ja samodejno prevede vaš `README.md` v več jezikov. Inteligentno vstavi medsebojno povezan jezikovni navigacijski meni v vse datoteke in lahko bodisi neposredno uveljavi (commit) spremembe ali ustvari zahtevek za poteg (Pull Request) za pregled.

## 🚀 Funkcionalnosti
* **Večjezična podpora:** Generiranje datotek README za več jezikov v enem zagonu.
* **Samodejna navigacija:** Samodejno vstavi in vzdržuje standardni meni za preklop med jeziki na vrhu vaših datotek (lahko se onemogoči). Umetna inteligenca ga samodejno oblikuje!
* **Prilagodljivo oblikovanje:** Podate lahko parameter za slog po meri, tako da umetna inteligenca meni za izbiro jezika oblikuje točno tako, kot želite.
* **Sledenje žetonom:** Izpiše statistiko porabe žetonov za Gemini.

## 🛠 Uporaba

Ustvarite datoteko s potekom dela (npr. `.github/workflows/translate.yml`):

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

## 📥 Vnosi

| Vnos | Obvezno | Privzeto | Opis |
| --- | --- | --- | --- |
| `api_key` | Da |  | Vaš Google Gemini API ključ. |
| `github_token` | Da |  | Standardni GitHub žeton (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Da |  | Ciljni jeziki, ločeni z vejico (npr. `ru, es`). |
| `output_dir` | Ne | | Imenik za shranjevanje prevedenih datotek. Privzeto je imenik izvorne datoteke. |
| `add_language_menu` | Ne | `true` | Nastavite na `false`, da onemogočite samodejno generiranje jezikovnega menija. |
| `menu_style` | Ne | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Referenčni slog, ki ga umetna inteligenca uporabi pri generiranju novega jezikovnega menija. |
| `commit_message` | Ne | `docs: auto-translate README via Gemini` | Besedilo, uporabljeno za sporočilo pri uveljavitvi git (commit message). |
| `model` | Ne | `gemini-3.1-pro-preview` | Model Gemini, ki naj se uporabi. |
| `source_file` | Ne | `README.md` | Osnovna datoteka za prevajanje. |

## 🔑 Kako pridobiti API ključ za Google Gemini

Za uporabo te akcije potrebujete brezplačen API ključ iz storitve Google AI Studio:

1. Pojdite na [Google AI Studio](https://aistudio.google.com/).
2. Prijavite se s svojim Google računom.
3. V levem navigacijskem meniju kliknite **Get API key**.
4. Kliknite gumb **Create API key**.
5. Kopirajte ustvarjeni ključ.
6. Pojdite v vaš repozitorij na GitHubu -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Kliknite **New repository secret**, poimenujte ga `GEMINI_API_KEY`, prilepite svoj ključ v polje Secret in shranite.

## 🔑 Kako konfigurirati standardni GitHub žeton

Ta akcija uporablja vgrajeni `GITHUB_TOKEN` za potiskanje uveljavitev (commits) ali ustvarjanje zahtevkov za poteg (Pull Requests). **Ni vam treba** ročno ustvariti osebnega žetona za dostop (PAT), vendar **morate** zagotoviti, da ima privzeti žeton ustrezna dovoljenja:

1. Pojdite v nastavitve vašega repozitorija: **Settings** -> **Actions** -> **General**.
2. Pomaknite se navzdol do razdelka **Workflow permissions**.
3. Izberite **Read and write permissions**.
4. Kliknite **Save**.
5. V vaši YAML datoteki poteka dela preprosto podajte `${{ secrets.GITHUB_TOKEN }}` vnosu `github_token` (kot je prikazano v primeru uporabe).

## 📄 Licenca

Ta projekt je licenciran pod licenco MIT - za podrobnosti glejte datoteko [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE).