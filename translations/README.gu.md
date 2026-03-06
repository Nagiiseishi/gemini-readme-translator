> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# જેમિની README ટ્રાન્સલેટર

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

એક GitHub Action જે Gemini API નો ઉપયોગ કરીને આપમેળે તમારા `README.md` નો બહુવિધ ભાષાઓમાં અનુવાદ કરે છે. તે બધી ફાઇલોમાં બુદ્ધિપૂર્વક ક્રોસ-લિંક્ડ ભાષા નેવિગેશન મેનૂ ઉમેરે છે અને સીધા ફેરફારોને કમિટ કરી શકે છે અથવા સમીક્ષા માટે Pull Request બનાવી શકે છે.

## 🚀 વિશેષતાઓ
* **બહુ-ભાષા સપોર્ટ:** એક જ રનમાં અનેક ભાષાઓ માટે READMEs જનરેટ કરો.
* **ઑટો-નેવિગેશન:** તમારી ફાઇલોની ટોચ પર આપમેળે સ્ટાન્ડર્ડ લેંગ્વેજ સ્વિચર મેનૂ દાખલ કરે છે અને જાળવે છે (નિષ્ક્રિય કરી શકાય છે). AI તેને આપમેળે સ્ટાઇલ કરે છે!
* **કસ્ટમ સ્ટાઇલિંગ:** તમે કસ્ટમ મેનૂ સ્ટાઇલ પેરામીટર પ્રદાન કરી શકો છો જેથી AI લેંગ્વેજ સ્વિચરને તમે ઇચ્છો તે જ રીતે ફોર્મેટ કરે.
* **ટોકન ટ્રેકિંગ:** જેમિની ટોકન વપરાશના આંકડા આઉટપુટ કરે છે.

## 🛠 ઉપયોગ

એક વર્કફ્લો ફાઇલ બનાવો (દા.ત., `.github/workflows/translate.yml`):

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

## 📥 ઇનપુટ્સ

| ઇનપુટ | જરૂરી | ડિફોલ્ટ | વર્ણન |
| --- | --- | --- | --- |
| `api_key` | હા |  | તમારી Google Gemini API કી. |
| `github_token` | હા |  | સ્ટાન્ડર્ડ GitHub ટોકન (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | હા |  | અલ્પવિરામથી અલગ કરેલી લક્ષ્ય ભાષાઓ (દા.ત. `ru, es`). |
| `output_dir` | ના | | અનુવાદિત ફાઇલો સાચવવા માટેની ડિરેક્ટરી. ડિફૉલ્ટ રૂપે સ્રોત ફાઇલની ડિરેક્ટરી વાપરે છે. |
| `add_language_menu` | ના | `true` | લેંગ્વેજ મેનૂના ઑટો-જનરેશનને નિષ્ક્રિય કરવા માટે `false` સેટ કરો. |
| `menu_style` | ના | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | નવું લેંગ્વેજ મેનૂ જનરેટ કરતી વખતે AI જે સંદર્ભ સ્ટાઇલનો ઉપયોગ કરે છે. |
| `commit_message` | ના | `docs: auto-translate README via Gemini` | ગિટ કમિટ મેસેજ માટે વપરાતો ટેક્સ્ટ. |
| `model` | ના | `gemini-3.1-pro-preview` | ઉપયોગમાં લેવાતું Gemini મૉડલ. |
| `source_file` | ના | `README.md` | અનુવાદ કરવા માટેની મૂળ ફાઇલ. |

## 🔑 Google Gemini API કી કેવી રીતે મેળવવી

આ ઍક્શનનો ઉપયોગ કરવા માટે, તમારે Google AI Studio માંથી એક મફત API કીની જરૂર પડશે:

1. [Google AI Studio](https://aistudio.google.com/) પર જાઓ.
2. તમારા Google એકાઉન્ટથી સાઇન ઇન કરો.
3. ડાબી બાજુના નેવિગેશન મેનૂમાં, **Get API key** પર ક્લિક કરો.
4. **Create API key** બટન પર ક્લિક કરો.
5. જનરેટ કરેલી કી કૉપિ કરો.
6. તમારી GitHub રિપોઝીટરીમાં જાઓ -> **Settings** -> **Secrets and variables** -> **Actions**.
7. **New repository secret** પર ક્લિક કરો, તેને `GEMINI_API_KEY` નામ આપો, સિક્રેટ ફીલ્ડમાં તમારી કી પેસ્ટ કરો, અને સેવ કરો.

## 🔑 સ્ટાન્ડર્ડ GitHub ટોકન કેવી રીતે કન્ફિગર કરવું

આ ઍક્શન કમિટ્સ પુશ કરવા અથવા Pull Requests બનાવવા માટે ઇન-બિલ્ટ `GITHUB_TOKEN` નો ઉપયોગ કરે છે. તમારે જાતે પર્સનલ એક્સેસ ટોકન (PAT) બનાવવાની જરૂર **નથી**, પરંતુ તમારે ખાતરી **કરવી જ જોઈએ** કે ડિફોલ્ટ ટોકન પાસે યોગ્ય પરવાનગીઓ છે:

1. તમારી રિપોઝીટરીના **Settings** -> **Actions** -> **General** માં જાઓ.
2. નીચે સ્ક્રોલ કરીને **Workflow permissions** વિભાગ પર જાઓ.
3. **Read and write permissions** પસંદ કરો.
4. **Save** પર ક્લિક કરો.
5. તમારા વર્કફ્લો YAML માં, ફક્ત `${{ secrets.GITHUB_TOKEN }}` ને `github_token` ઇનપુટમાં પાસ કરો (જેમ ઉપયોગના ઉદાહરણમાં દર્શાવ્યું છે).

## 📄 લાયસન્સ

આ પ્રોજેક્ટ MIT લાયસન્સ હેઠળ છે - વધુ વિગતો માટે [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) ફાઇલ જુઓ.