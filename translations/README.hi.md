> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

यह एक GitHub Action है जो Gemini API का उपयोग करके आपके `README.md` का स्वचालित रूप से कई भाषाओं में अनुवाद करता है। यह बुद्धिमानी से सभी फ़ाइलों में एक क्रॉस-लिंक्ड भाषा नेविगेशन मेनू डालता है और या तो सीधे बदलावों को कमिट कर सकता है या समीक्षा के लिए एक पुल रिक्वेस्ट (Pull Request) बना सकता है।

## 🚀 विशेषताएँ
* **बहु-भाषा समर्थन:** एक ही बार में कई भाषाओं के लिए README जनरेट करें।
* **ऑटो-नेविगेशन:** स्वचालित रूप से आपकी फ़ाइलों के शीर्ष पर एक मानक भाषा स्विचर मेनू सम्मिलित करता है और उसे बनाए रखता है (इसे अक्षम भी किया जा सकता है)। AI इसे स्वचालित रूप से स्टाइल करता है!
* **कस्टम स्टाइलिंग:** आप एक कस्टम मेनू स्टाइल पैरामीटर प्रदान कर सकते हैं ताकि AI भाषा स्विचर को ठीक उसी तरह से फॉर्मेट करे जैसा आप चाहते हैं।
* **टोकन ट्रैकिंग:** Gemini टोकन उपयोग के आँकड़े आउटपुट करता है।

## 🛠 उपयोग

एक वर्कफ़्लो फ़ाइल बनाएँ (जैसे, `.github/workflows/translate.yml`):

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

## 📥 इनपुट्स

| इनपुट | आवश्यक | डिफ़ॉल्ट | विवरण |
| --- | --- | --- | --- |
| `api_key` | हाँ |  | आपकी Google Gemini API key। |
| `github_token` | हाँ |  | मानक GitHub टोकन (`${{ secrets.GITHUB_TOKEN }}`)। |
| `languages` | हाँ |  | अल्पविराम द्वारा अलग की गई लक्ष्य भाषाएँ (जैसे `ru, es`)। |
| `output_dir` | नहीं | | अनुवादित फ़ाइलों को सहेजने के लिए डायरेक्टरी। डिफ़ॉल्ट रूप से स्रोत फ़ाइल की डायरेक्टरी। |
| `add_language_menu` | नहीं | `true` | भाषा मेनू के स्वतः-निर्माण को अक्षम (disable) करने के लिए `false` पर सेट करें। |
| `menu_style` | नहीं | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | नया भाषा मेनू बनाते समय AI द्वारा उपयोग की जाने वाली संदर्भ शैली। |
| `commit_message` | नहीं | `docs: auto-translate README via Gemini` | git कमिट संदेश के लिए उपयोग किया जाने वाला टेक्स्ट। |
| `model` | नहीं | `gemini-3.1-pro-preview` | उपयोग किया जाने वाला Gemini मॉडल। |
| `source_file` | नहीं | `README.md` | अनुवाद करने के लिए आधार फ़ाइल। |

## 🔑 Google Gemini API Key कैसे प्राप्त करें

इस Action का उपयोग करने के लिए, आपको Google AI Studio से एक मुफ़्त API key की आवश्यकता होगी:

1. [Google AI Studio](https://aistudio.google.com/) पर जाएँ।
2. अपने Google खाते से साइन इन करें।
3. बाएँ नेविगेशन मेनू में, **Get API key** पर क्लिक करें।
4. **Create API key** बटन पर क्लिक करें।
5. जनरेट की गई key को कॉपी करें।
6. अपनी GitHub रिपॉजिटरी में जाएँ -> **Settings** -> **Secrets and variables** -> **Actions**।
7. **New repository secret** पर क्लिक करें, इसे `GEMINI_API_KEY` नाम दें, Secret फ़ील्ड में अपनी key पेस्ट करें और सेव करें।

## 🔑 मानक GitHub टोकन को कैसे कॉन्फ़िगर करें

यह एक्शन कमिट पुश करने या पुल रिक्वेस्ट बनाने के लिए अंतर्निहित `GITHUB_TOKEN` का उपयोग करता है। आपको मैन्युअल रूप से पर्सनल एक्सेस टोकन (PAT) बनाने की आवश्यकता **नहीं** है, लेकिन आपको यह **ज़रूर** सुनिश्चित करना चाहिए कि डिफ़ॉल्ट टोकन के पास सही अनुमतियाँ (permissions) हैं:

1. अपनी रिपॉजिटरी की **Settings** -> **Actions** -> **General** में जाएँ।
2. नीचे स्क्रॉल करके **Workflow permissions** अनुभाग पर जाएँ।
3. **Read and write permissions** चुनें।
4. **Save** पर क्लिक करें।
5. अपने वर्कफ़्लो YAML में, बस `${{ secrets.GITHUB_TOKEN }}` को `github_token` इनपुट में पास करें (जैसा कि उपयोग के उदाहरण में दिखाया गया है)।

## 📄 लाइसेंस

यह प्रोजेक्ट MIT लाइसेंस के अंतर्गत लाइसेंस प्राप्त है - विवरण के लिए [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) फ़ाइल देखें।