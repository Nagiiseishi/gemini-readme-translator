> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Kifasiri cha README cha Gemini

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action inayotafsiri faili lako la `README.md` kiotomatiki katika lugha nyingi kwa kutumia API ya Gemini. Inaingiza kiakili menyu ya urambazaji ya lugha iliyounganishwa kwa faili zote na inaweza kufanya commit ya mabadiliko moja kwa moja au kuunda Pull Request kwa ajili ya ukaguzi.

## 🚀 Vipengele
* **Usaidizi wa Lugha Nyingi:** Tengeneza faili za README za lugha nyingi katika mkondo mmoja.
* **Urambazaji Kiotomatiki:** Huweka na kudumisha menyu ya kawaida ya kubadili lugha kiotomatiki juu ya faili zako (inaweza kuzimwa). AI huipamba kiotomatiki!
* **Mtindo Maalum:** Unaweza kutoa kigezo cha mtindo wa menyu maalum ili AI iweke umbizo la kibadilishaji lugha jinsi unavyotaka haswa.
* **Ufuatiliaji wa Tokeni:** Hutoa takwimu za matumizi ya tokeni za Gemini.

## 🛠 Matumizi

Unda faili la workflow (k.m., `.github/workflows/translate.yml`):

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

## 📥 Pembejeo

| Pembejeo | Inahitajika | Chaguo-msingi | Maelezo |
| --- | --- | --- | --- |
| `api_key` | Ndiyo |  | Ufunguo wako wa API wa Google Gemini. |
| `github_token` | Ndiyo |  | Tokeni ya kawaida ya GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ndiyo |  | Lugha lengwa zilizotenganishwa kwa koma (k.m. `ru, es`). |
| `output_dir` | Hapana | | Saraka ya kuhifadhi faili zilizotafsiriwa. Ikiwa haijawekwa itatumia saraka ya faili asili. |
| `add_language_menu` | Hapana | `true` | Weka `false` ili kuzima uundaji kiotomatiki wa menyu ya lugha. |
| `menu_style` | Hapana | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Mtindo wa rejea ambao AI inatumia wakati wa kuunda menyu mpya ya lugha. |
| `commit_message` | Hapana | `docs: auto-translate README via Gemini` | Maandishi yanayotumika kwa ujumbe wa git commit. |
| `model` | Hapana | `gemini-3.1-pro-preview` | Mfumo (model) wa Gemini wa kutumia. |
| `source_file` | Hapana | `README.md` | Faili la msingi la kutafsiri. |

## 🔑 Jinsi ya kupata Ufunguo wa API wa Google Gemini

Ili kutumia Action hii, unahitaji ufunguo wa API wa bure kutoka Google AI Studio:

1. Nenda [Google AI Studio](https://aistudio.google.com/).
2. Ingia (Sign in) kwa kutumia akaunti yako ya Google.
3. Kwenye menyu ya urambazaji upande wa kushoto, bofya **Get API key**.
4. Bofya kitufe cha **Create API key**.
5. Nakili ufunguo uliotengenezwa.
6. Nenda kwenye repository yako ya GitHub -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Bofya **New repository secret**, ipe jina `GEMINI_API_KEY`, weka (paste) ufunguo wako kwenye sehemu ya Secret, kisha hifadhi.

## 🔑 Jinsi ya kusanidi Tokeni ya Kawaida ya GitHub

Action hii inatumia `GITHUB_TOKEN` iliyojengewa ndani kupush commits au kuunda Pull Requests. **Huhitaji** kuunda Personal Access Token (PAT) kwa mikono, lakini **lazima** uhakikishe tokeni ya chaguo-msingi ina ruhusa sahihi:

1. Nenda kwenye **Settings** za repository yako -> **Actions** -> **General**.
2. Tembeza chini hadi kwenye sehemu ya **Workflow permissions**.
3. Chagua **Read and write permissions**.
4. Bofya **Save**.
5. Katika YAML yako ya workflow, pitisha tu `${{ secrets.GITHUB_TOKEN }}` kwenye pembejeo ya `github_token` (kama inavyoonyeshwa kwenye mfano wa matumizi).

## 📄 Leseni

Mradi huu umepewa leseni chini ya Leseni ya MIT - angalia faili la [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) kwa maelezo zaidi.