> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README மொழிபெயர்ப்பாளர்

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Gemini API-ஐப் பயன்படுத்தி உங்கள் `README.md` கோப்பை தானியங்கியாகப் பல மொழிகளில் மொழிபெயர்க்கும் ஒரு GitHub Action இது. இது அனைத்து கோப்புகளிலும் இணைக்கப்பட்ட மொழி வழிசெலுத்தல் மெனுவை (language navigation menu) புத்திசாலித்தனமாகச் செருகுகிறது, மேலும் மாற்றங்களை நேரடியாக கமிட் (commit) செய்யலாம் அல்லது மதிப்பாய்வுக்காக ஒரு புல் ரெக்வெஸ்ட்டை (Pull Request) உருவாக்கலாம்.

## 🚀 அம்சங்கள்
* **பன்மொழி ஆதரவு:** ஒரே செயல்பாட்டில் பல மொழிகளுக்கான README-களை உருவாக்கலாம்.
* **தானியங்கு-வழிசெலுத்தல் (Auto-Navigation):** உங்கள் கோப்புகளின் மேற்புறத்தில் ஒரு நிலையான மொழி மாற்றி மெனுவை தானாகவே செருகி பராமரிக்கிறது (இதை முடக்கவும் முடியும்). AI இதனைத் தானாகவே வடிவமைக்கிறது!
* **தனிப்பயன் வடிவமைப்பு (Custom Styling):** நீங்கள் தனிப்பயன் மெனு வடிவமைப்பு அளவுருவை (parameter) வழங்கலாம், இதன் மூலம் மொழி மாற்றியை நீங்கள் விரும்பும் விதத்திலேயே AI வடிவமைக்கும்.

* **டோக்கன் கண்காணிப்பு:** Gemini டோக்கன் பயன்பாட்டுப் புள்ளிவிவரங்களை வெளியிடுகிறது.

## 🛠 பயன்பாடு

ஒரு வொர்க்ஃப்ளோ (workflow) கோப்பை உருவாக்கவும் (எ.கா., `.github/workflows/translate.yml`):

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

## 📥 உள்ளீடுகள் (Inputs)

| உள்ளீடு (Input) | தேவையானது (Required) | இயல்புநிலை (Default) | விளக்கம் (Description) |
| --- | --- | --- | --- |
| `api_key` | ஆம் (Yes) |  | உங்களின் Google Gemini API திறவுகோல் (Key). |
| `github_token` | ஆம் (Yes) |  | நிலையான GitHub டோக்கன் (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | ஆம் (Yes) |  | காற்புள்ளியால் பிரிக்கப்பட்ட இலக்கு மொழிகள் (எ.கா. `ru, es`). |
| `output_dir` | இல்லை (No) | | மொழிபெயர்க்கப்பட்ட கோப்புகளைச் சேமிக்க வேண்டிய கோப்பகம். இயல்புநிலையாக மூலக் கோப்பின் கோப்பகத்தில் சேமிக்கப்படும். |
| `add_language_menu` | இல்லை (No) | `true` | மொழி மெனு தானாக உருவாக்கப்படுவதை முடக்க `false` என அமைக்கவும். |
| `menu_style` | இல்லை (No) | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | புதிய மொழி மெனுவை உருவாக்கும் போது AI பயன்படுத்தும் குறிப்பு வடிவமைப்பு (reference style). |
| `commit_message` | இல்லை (No) | `docs: auto-translate README via Gemini` | git கமிட் (commit) செய்திக்குப் பயன்படுத்தப்படும் உரை. |
| `model` | இல்லை (No) | `gemini-3.1-pro-preview` | பயன்படுத்த வேண்டிய Gemini மாடல். |
| `source_file` | இல்லை (No) | `README.md` | மொழிபெயர்க்க வேண்டிய அடிப்படை கோப்பு. |

## 🔑 Google Gemini API Key-ஐப் பெறுவது எப்படி

இந்த Action-ஐப் பயன்படுத்த, Google AI Studio-விலிருந்து ஒரு இலவச API திறவுகோல் (API key) தேவை:

1. [Google AI Studio](https://aistudio.google.com/) இணையதளத்திற்குச் செல்லவும்.
2. உங்கள் Google கணக்கைக் கொண்டு உள்நுழையவும்.
3. இடதுபுற வழிசெலுத்தல் மெனுவில், **Get API key** என்பதைக் கிளிக் செய்யவும்.
4. **Create API key** பொத்தானைக் கிளிக் செய்யவும்.
5. உருவாக்கப்பட்ட திறவுகோலை நகலெடுக்கவும் (Copy).
6. உங்கள் GitHub ரெபோசிட்டரிக்குச் செல்லவும் -> **Settings** -> **Secrets and variables** -> **Actions**.
7. **New repository secret** என்பதைக் கிளிக் செய்து, அதற்கு `GEMINI_API_KEY` எனப் பெயரிட்டு, Secret புலத்தில் உங்கள் திறவுகோலை ஒட்டி, சேமிக்கவும்.

## 🔑 நிலையான GitHub டோக்கனை (Standard GitHub Token) உள்ளமைப்பது எப்படி

கமிட்களை (commits) புஷ் செய்ய அல்லது புல் ரெக்வெஸ்ட்டுகளை (Pull Requests) உருவாக்க இந்த Action உள்ளமைக்கப்பட்ட `GITHUB_TOKEN`-ஐப் பயன்படுத்துகிறது. நீங்கள் கைமுறையாக ஒரு Personal Access Token (PAT)-ஐ உருவாக்க **தேவையில்லை**, ஆனால் இயல்புநிலை டோக்கனுக்குச் சரியான அனுமதிகள் இருப்பதை நீங்கள் **கட்டாயம்** உறுதிசெய்ய வேண்டும்:

1. உங்கள் ரெபோசிட்டரியின் **Settings** -> **Actions** -> **General**-க்குச் செல்லவும்.
2. கீழே ஸ்க்ரோல் செய்து **Workflow permissions** பகுதிக்குச் செல்லவும்.
3. **Read and write permissions** என்பதைத் தேர்ந்தெடுக்கவும்.
4. **Save** என்பதைக் கிளிக் செய்யவும்.
5. உங்களின் workflow YAML கோப்பில், `github_token` உள்ளீட்டிற்கு (பயன்பாட்டு எடுத்துக்காட்டில் காட்டப்பட்டுள்ளபடி) `${{ secrets.GITHUB_TOKEN }}`-ஐ வழங்கவும்.

## 📄 உரிமம் (License)

இந்தத் திட்டம் MIT உரிமத்தின் கீழ் உரிமம் பெற்றுள்ளது - விவரங்களுக்கு [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) கோப்பைப் பார்க்கவும்.