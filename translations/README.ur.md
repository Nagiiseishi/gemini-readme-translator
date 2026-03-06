> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README مترجم

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

یہ ایک GitHub Action ہے جو Gemini API کا استعمال کرتے ہوئے آپ کے `README.md` کا خودکار طور پر متعدد زبانوں میں ترجمہ کرتا ہے۔ یہ ہوشمندی کے ساتھ تمام فائلوں میں ایک کراس لنکڈ لینگویج نیویگیشن مینو شامل کرتا ہے اور تبدیلیوں کو براہ راست کمٹ (commit) کر سکتا ہے یا جائزے کے لیے پل ریکویسٹ (Pull Request) بنا سکتا ہے۔

## 🚀 خصوصیات
* **کثیر لسانی معاونت:** ایک ہی رن میں متعدد زبانوں کے لیے READMEs بنائیں۔
* **آٹو نیویگیشن:** خودکار طور پر آپ کی فائلوں کے اوپری حصے میں ایک معیاری لینگویج سوئچر مینو شامل اور برقرار رکھتا ہے (اسے غیر فعال بھی کیا جا سکتا ہے)۔ AI اسے خود بخود اسٹائل کرتا ہے!
* **کسٹم اسٹائلنگ:** آپ مینو کا ایک حسب ضرورت (custom) اسٹائل پیرامیٹر فراہم کر سکتے ہیں تاکہ AI لینگویج سوئچر کو بالکل اسی طرح فارمیٹ کرے جیسا آپ چاہتے ہیں۔

* **ٹوکن ٹریکنگ:** یہ Gemini ٹوکن کے استعمال کے اعدادوشمار دکھاتا ہے۔

## 🛠 استعمال کا طریقہ

ایک ورک فلو فائل بنائیں (مثلاً، `.github/workflows/translate.yml`):

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

## 📥 ان پٹس (Inputs)

| ان پٹ (Input) | ضروری | ڈیفالٹ | تفصیل |
| --- | --- | --- | --- |
| `api_key` | ہاں |  | آپ کی Google Gemini API کلید۔ |
| `github_token` | ہاں |  | معیاری GitHub ٹوکن (`${{ secrets.GITHUB_TOKEN }}`)۔ |
| `languages` | ہاں |  | کوما سے الگ کی گئی ہدف زبانیں (مثلاً `ru, es`)۔ |
| `output_dir` | نہیں | | ترجمہ شدہ فائلوں کو محفوظ کرنے کی ڈائرکٹری۔ بائی ڈیفالٹ یہ سورس فائل کی ڈائرکٹری ہوتی ہے۔ |
| `add_language_menu` | نہیں | `true` | لینگویج مینو کے خودکار بننے کو غیر فعال کرنے کے لیے `false` سیٹ کریں۔ |
| `menu_style` | نہیں | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | وہ حوالہ جاتی اسٹائل جسے AI نیا لینگویج مینو بناتے وقت استعمال کرتا ہے۔ |
| `commit_message` | نہیں | `docs: auto-translate README via Gemini` | git کمٹ میسج کے لیے استعمال ہونے والا متن۔ |
| `model` | نہیں | `gemini-3.1-pro-preview` | استعمال ہونے والا Gemini ماڈل۔ |
| `source_file` | نہیں | `README.md` | ترجمہ کرنے کے لیے بنیادی فائل۔ |

## 🔑 گوگل جیمنی (Google Gemini) API کلید کیسے حاصل کریں

اس ایکشن کو استعمال کرنے کے لیے، آپ کو Google AI Studio سے ایک مفت API کلید درکار ہے:

1. [Google AI Studio](https://aistudio.google.com/) پر جائیں۔
2. اپنے گوگل اکاؤنٹ سے سائن ان کریں۔
3. بائیں جانب نیویگیشن مینو میں، **Get API key** پر کلک کریں۔
4. **Create API key** بٹن پر کلک کریں۔
5. تیار کردہ کلید (key) کاپی کریں۔
6. اپنی GitHub ریپوزٹری پر جائیں -> **Settings** -> **Secrets and variables** -> **Actions**۔
7. **New repository secret** پر کلک کریں، اس کا نام `GEMINI_API_KEY` رکھیں، خفیہ (Secret) فیلڈ میں اپنی کلید پیسٹ کریں، اور محفوظ (save) کریں۔

## 🔑 معیاری گٹ ہب ٹوکن (GitHub Token) کو کیسے کنفیگر کریں

یہ ایکشن کمٹس کو پش (push) کرنے یا پل ریکوئسٹس (Pull Requests) بنانے کے لیے بلٹ ان `GITHUB_TOKEN` کا استعمال کرتا ہے۔ آپ کو دستی طور پر پرسنل ایکسیس ٹوکن (PAT) بنانے کی **ضرورت نہیں** ہے، لیکن آپ کو یہ یقینی بنانا **ضروری** ہے کہ ڈیفالٹ ٹوکن کے پاس درست اجازتیں (permissions) ہوں:

1. اپنی ریپوزٹری کی **Settings** -> **Actions** -> **General** پر جائیں۔
2. نیچے اسکرول کر کے **Workflow permissions** سیکشن میں جائیں۔
3. **Read and write permissions** کو منتخب کریں۔
4. **Save** پر کلک کریں۔
5. اپنے ورک فلو YAML میں، بس `${{ secrets.GITHUB_TOKEN }}` کو `github_token` ان پٹ کے طور پر پاس کریں (جیسا کہ استعمال کی مثال میں دکھایا گیا ہے)۔

## 📄 لائسنس

یہ پروجیکٹ MIT لائسنس کے تحت لائسنس یافتہ ہے - تفصیلات کے لیے [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) فائل دیکھیں۔