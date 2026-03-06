> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

ही एक GitHub Action आहे जी Gemini API चा वापर करून तुमच्या `README.md` चे आपोआप अनेक भाषांमध्ये भाषांतर करते. ती हुशारीने सर्व फायलींमध्ये क्रॉस-लिंक्ड भाषा नेव्हिगेशन मेनू जोडते आणि थेट बदल कमिट करू शकते किंवा पुनरावलोकनासाठी पुल रिक्वेस्ट (Pull Request) तयार करू शकते.

## 🚀 वैशिष्ट्ये
* **बहु-भाषा समर्थन:** एकाच रनमध्ये अनेक भाषांसाठी README तयार करा.
* **स्वयं-नेव्हिगेशन (Auto-Navigation):** तुमच्या फायलींच्या शीर्षस्थानी एक मानक भाषा बदलणारा मेनू आपोआप समाविष्ट करते आणि व्यवस्थापित करते (अक्षम केले जाऊ शकते). एआय (AI) ते स्वयंचलितपणे स्टाईल करते!
* **सानुकूल स्टायलिंग (Custom Styling):** तुम्ही सानुकूल मेनू स्टाईल पॅरामीटर प्रदान करू शकता जेणेकरून AI भाषा स्विचिंग मेनू तुम्हाला हवा तसा फॉरमॅट करेल.
* **टोकन ट्रॅकिंग:** Gemini टोकन वापराची आकडेवारी आउटपुट करते.

## 🛠 वापर (Usage)

एक वर्कफ्लो फाईल तयार करा (उदा. `.github/workflows/translate.yml`):

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

## 📥 इनपुट्स (Inputs)

| इनपुट (Input) | आवश्यक (Required) | डीफॉल्ट (Default) | वर्णन (Description) |
| --- | --- | --- | --- |
| `api_key` | होय |  | तुमची Google Gemini API की (Key). |
| `github_token` | होय |  | मानक GitHub टोकन (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | होय |  | स्वल्पविरामाने वेगळ्या केलेल्या लक्ष्य भाषा (उदा. `ru, es`). |
| `output_dir` | नाही | | अनुवादित फायली सेव्ह करण्यासाठी डिरेक्टरी. डीफॉल्टनुसार सोर्स फाईलची डिरेक्टरी. |
| `add_language_menu` | नाही | `true` | भाषा मेनू स्वयंचलितपणे तयार होणे अक्षम करण्यासाठी `false` वर सेट करा. |
| `menu_style` | नाही | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | नवीन भाषा मेनू तयार करताना AI द्वारे वापरली जाणारी संदर्भ स्टाईल. |
| `commit_message` | नाही | `docs: auto-translate README via Gemini` | git कमिट मेसेजसाठी वापरला जाणारा मजकूर. |
| `model` | नाही | `gemini-3.1-pro-preview` | वापरण्यासाठी असलेले Gemini मॉडेल. |
| `source_file` | नाही | `README.md` | भाषांतर करण्यासाठी मूळ फाईल. |

## 🔑 Google Gemini API Key कशी मिळवायची

ही ॲक्शन वापरण्यासाठी, तुम्हाला Google AI Studio कडून एक मोफत API की आवश्यक आहे:

1. [Google AI Studio](https://aistudio.google.com/) वर जा.
2. तुमच्या Google खात्याने साईन इन करा.
3. डावीकडील नेव्हिगेशन मेनूमध्ये, **Get API key** वर क्लिक करा.
4. **Create API key** बटणावर क्लिक करा.
5. तयार झालेली की (Key) कॉपी करा.
6. तुमच्या GitHub रिपॉजिटरीमध्ये जा -> **Settings** -> **Secrets and variables** -> **Actions**.
7. **New repository secret** वर क्लिक करा, त्याला `GEMINI_API_KEY` असे नाव द्या, तुमची की Secret फील्डमध्ये पेस्ट करा आणि सेव्ह करा.

## 🔑 स्टँडर्ड GitHub Token कसे कॉन्फिगर करावे

कमिट पुश करण्यासाठी किंवा पुल रिक्वेस्ट्स तयार करण्यासाठी ही ॲक्शन अंगभूत (built-in) `GITHUB_TOKEN` चा वापर करते. तुम्हाला स्वहस्ते पर्सनल ॲक्सेस टोकन (PAT) तयार करण्याची **गरज नाही**, पण तुम्ही हे निश्चित **करणे आवश्यक आहे** की डीफॉल्ट टोकनकडे योग्य परवानग्या (permissions) आहेत:

1. तुमच्या रिपॉजिटरीच्या **Settings** -> **Actions** -> **General** मध्ये जा.
2. खाली स्क्रोल करून **Workflow permissions** विभागात जा.
3. **Read and write permissions** निवडा.
4. **Save** वर क्लिक करा.
5. तुमच्या वर्कफ्लो YAML मध्ये, केवळ `${{ secrets.GITHUB_TOKEN }}` ला `github_token` इनपुटमध्ये पास करा (जसे की वापर उदाहरणात दाखवले आहे).

## 📄 परवाना (License)

हा प्रकल्प MIT परवान्याअंतर्गत परवानाकृत आहे - अधिक माहितीसाठी [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) फाईल पहा.