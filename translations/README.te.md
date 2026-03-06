> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README అనువాదకుడు

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Gemini API ని ఉపయోగించి మీ `README.md` ని బహుళ భాషల్లోకి స్వయంచాలకంగా అనువదించే GitHub Action ఇది. ఇది అన్ని ఫైల్‌లలో క్రాస్-లింక్డ్ భాషా నావిగేషన్ మెనుని తెలివిగా చొప్పిస్తుంది మరియు మార్పులను నేరుగా కమిట్ చేయగలదు లేదా సమీక్ష కోసం పుల్ రిక్వెస్ట్‌ను సృష్టించగలదు.

## 🚀 ఫీచర్లు
* **బహుళ-భాషా మద్దతు:** ఒకే రన్‌లో బహుళ భాషల కోసం READMEలను రూపొందించండి.
* **ఆటో-నావిగేషన్:** మీ ఫైల్‌ల పైభాగంలో ప్రామాణిక భాష మార్పిడి మెనుని స్వయంచాలకంగా చొప్పిస్తుంది మరియు నిర్వహిస్తుంది (నిలిపివేయవచ్చు). AI దాన్ని స్వయంచాలకంగా స్టైల్ చేస్తుంది!
* **కస్టమ్ స్టైలింగ్:** మీరు అనుకూల మెను స్టైల్ పరామితిని అందించవచ్చు, తద్వారా AI భాషా స్విచ్చర్‌ను మీరు కోరుకున్న విధంగానే ఫార్మాట్ చేస్తుంది.

* **టోకెన్ ట్రాకింగ్:** జెమిని టోకెన్ వినియోగ గణాంకాలను అవుట్‌పుట్ చేస్తుంది.

## 🛠 వాడుక

ఒక వర్క్‌ఫ్లో ఫైల్‌ను సృష్టించండి (ఉదా., `.github/workflows/translate.yml`):

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

## 📥 ఇన్‌పుట్‌లు

| ఇన్‌పుట్ | అవసరం | డిఫాల్ట్ | వివరణ |
| --- | --- | --- | --- |
| `api_key` | అవును |  | మీ Google Gemini API కీ. |
| `github_token` | అవును |  | ప్రామాణిక GitHub టోకెన్ (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | అవును |  | కామాలతో వేరుచేయబడిన లక్ష్య భాషలు (ఉదా. `ru, es`). |
| `output_dir` | కాదు | | అనువదించబడిన ఫైల్‌లను సేవ్ చేయడానికి డైరెక్టరీ. డిఫాల్ట్‌గా మూల ఫైల్ డైరెక్టరీకి సేవ్ అవుతుంది. |
| `add_language_menu` | కాదు | `true` | భాషా మెను యొక్క స్వయంచాలక ఉత్పత్తిని నిలిపివేయడానికి `false` కు సెట్ చేయండి. |
| `menu_style` | కాదు | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | కొత్త భాషా మెనుని రూపొందించేటప్పుడు AI ఉపయోగించే సూచన (రెఫరెన్స్) శైలి. |
| `commit_message` | కాదు | `docs: auto-translate README via Gemini` | git కమిట్ సందేశం కోసం ఉపయోగించే వచనం. |
| `model` | కాదు | `gemini-3.1-pro-preview` | ఉపయోగించాల్సిన జెమిని మోడల్. |
| `source_file` | కాదు | `README.md` | అనువదించడానికి ఆధార ఫైల్. |

## 🔑 Google Gemini API కీని ఎలా పొందాలి

ఈ యాక్షన్‌ను ఉపయోగించడానికి, మీకు Google AI Studio నుండి ఉచిత API కీ అవసరం:

1. [Google AI Studio](https://aistudio.google.com/) కు వెళ్ళండి.
2. మీ Google ఖాతాతో సైన్ ఇన్ చేయండి.
3. ఎడమవైపు నావిగేషన్ మెనులో, **Get API key** పై క్లిక్ చేయండి.
4. **Create API key** బటన్‌పై క్లిక్ చేయండి.
5. సృష్టించబడిన కీని కాపీ చేయండి.
6. మీ GitHub రిపోజిటరీకి వెళ్లి -> **Settings** -> **Secrets and variables** -> **Actions** కు నావిగేట్ చేయండి.
7. **New repository secret** ని క్లిక్ చేసి, దానికి `GEMINI_API_KEY` అని పేరు పెట్టి, మీ కీని Secret ఫీల్డ్‌లో పేస్ట్ చేసి, సేవ్ చేయండి.

## 🔑 ప్రామాణిక GitHub టోకెన్‌ను ఎలా కాన్ఫిగర్ చేయాలి

ఈ యాక్షన్ కమిట్‌లను పుష్ చేయడానికి లేదా పుల్ రిక్వెస్ట్‌లను సృష్టించడానికి అంతర్నిర్మిత `GITHUB_TOKEN` ను ఉపయోగిస్తుంది. మీరు మాన్యువల్‌గా పర్సనల్ యాక్సెస్ టోకెన్ (PAT) సృష్టించాల్సిన **అవసరం లేదు**, కానీ డిఫాల్ట్ టోకెన్‌కు సరైన అనుమతులు ఉన్నాయని మీరు **తప్పక** నిర్ధారించుకోవాలి:

1. మీ రిపోజిటరీ **Settings** -> **Actions** -> **General** కు వెళ్ళండి.
2. క్రిందికి స్క్రోల్ చేసి **Workflow permissions** విభాగానికి వెళ్ళండి.
3. **Read and write permissions** ను ఎంచుకోండి.
4. **Save** క్లిక్ చేయండి.
5. మీ వర్క్‌ఫ్లో YAML లో, (ఉపయోగ ఉదాహరణలో చూపిన విధంగా) `github_token` ఇన్‌పుట్‌కు `${{ secrets.GITHUB_TOKEN }}` ను పాస్ చేయండి.

## 📄 లైసెన్స్

ఈ ప్రాజెక్ట్ MIT లైసెన్స్ క్రింద లైసెన్స్ పొందింది - వివరాల కోసం [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) ఫైల్‌ను చూడండి.