> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

একটি গিটহাব অ্যাকশন (GitHub Action) যা জেমিনি এপিআই (Gemini API) ব্যবহার করে স্বয়ংক্রিয়ভাবে আপনার `README.md` ফাইলটিকে একাধিক ভাষায় অনুবাদ করে। এটি বুদ্ধিমত্তার সাথে সমস্ত ফাইলে একটি ক্রস-লিঙ্কড ভাষা নেভিগেশন মেনু যুক্ত করে এবং হয় সরাসরি পরিবর্তনগুলো কমিট (commit) করতে পারে অথবা পর্যালোচনার জন্য একটি পুল রিকোয়েস্ট (Pull Request) তৈরি করতে পারে।

## 🚀 বৈশিষ্ট্যসমূহ (Features)
* **একাধিক ভাষার সমর্থন (Multi-Language Support):** এক রানেই একাধিক ভাষার জন্য README তৈরি করুন।
* **স্বয়ংক্রিয়-নেভিগেশন (Auto-Navigation):** স্বয়ংক্রিয়ভাবে আপনার ফাইলগুলোর শীর্ষে একটি স্ট্যান্ডার্ড ভাষা পরিবর্তনের মেনু (language switcher menu) সন্নিবেশ এবং পরিচালনা করে (নিষ্ক্রিয় করা যেতে পারে)। এআই (AI) এটি স্বয়ংক্রিয়ভাবে স্টাইল করে!
* **কাস্টম স্টাইলিং (Custom Styling):** আপনি একটি কাস্টম মেনু স্টাইল প্যারামিটার প্রদান করতে পারেন যাতে এআই (AI) ভাষা পরিবর্তনের মেনুটিকে ঠিক আপনার পছন্দমতো ফরম্যাট করতে পারে।
* **টোকেন ট্র্যাকিং (Token Tracking):** জেমিনি টোকেন ব্যবহারের পরিসংখ্যান আউটপুট হিসেবে প্রদান করে।

## 🛠 ব্যবহার (Usage)

একটি ওয়ার্কফ্লো ফাইল তৈরি করুন (উদাহরণস্বরূপ, `.github/workflows/translate.yml`):

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

## 📥 ইনপুটসমূহ (Inputs)

| ইনপুট (Input) | প্রয়োজনীয় (Required) | ডিফল্ট (Default) | বর্ণনা (Description) |
| --- | --- | --- | --- |
| `api_key` | হ্যাঁ (Yes) |  | আপনার গুগল জেমিনি এপিআই কি (Google Gemini API Key)। |
| `github_token` | হ্যাঁ (Yes) |  | স্ট্যান্ডার্ড গিটহাব টোকেন (`${{ secrets.GITHUB_TOKEN }}`)। |
| `languages` | হ্যাঁ (Yes) |  | কমা দিয়ে আলাদা করা কাঙ্ক্ষিত ভাষাসমূহ (যেমন- `ru, es`)। |
| `output_dir` | না (No) | | অনুবাদিত ফাইলগুলো সেভ করার ডিরেক্টরি। ডিফল্টভাবে সোর্স ফাইলের ডিরেক্টরি ব্যবহার করে। |
| `add_language_menu` | না (No) | `true` | ভাষা মেনুর স্বয়ংক্রিয় তৈরি নিষ্ক্রিয় করতে `false` সেট করুন। |
| `menu_style` | না (No) | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | নতুন ভাষা মেনু তৈরি করার সময় এআই (AI) যে রেফারেন্স স্টাইলটি ব্যবহার করে। |
| `commit_message` | না (No) | `docs: auto-translate README via Gemini` | গিট (git) কমিট মেসেজের জন্য ব্যবহৃত টেক্সট। |
| `model` | না (No) | `gemini-3.1-pro-preview` | যে জেমিনি মডেলটি ব্যবহার করতে হবে। |
| `source_file` | না (No) | `README.md` | অনুবাদ করার জন্য মূল (base) ফাইল। |

## 🔑 কীভাবে গুগল জেমিনি এপিআই কি (Google Gemini API Key) পাবেন

এই অ্যাকশনটি ব্যবহার করতে, আপনার গুগল এআই স্টুডিও (Google AI Studio) থেকে একটি বিনামূল্যের API কী প্রয়োজন:

1. [Google AI Studio](https://aistudio.google.com/)-তে যান।
2. আপনার গুগল অ্যাকাউন্ট দিয়ে সাইন ইন করুন।
3. বাম দিকের নেভিগেশন মেনুতে, **Get API key**-এ ক্লিক করুন।
4. **Create API key** বোতামে ক্লিক করুন।
5. তৈরি করা কী (key) কপি করুন।
6. আপনার গিটহাব রিপোজিটরিতে যান -> **Settings** -> **Secrets and variables** -> **Actions**।
7. **New repository secret**-এ ক্লিক করুন, এর নাম দিন `GEMINI_API_KEY`, Secret ফিল্ডে আপনার কী-টি পেস্ট করুন এবং সেভ করুন।

## 🔑 কীভাবে স্ট্যান্ডার্ড গিটহাব টোকেন (Standard GitHub Token) কনফিগার করবেন

এই অ্যাকশনটি কমিট পুশ করতে বা পুল রিকোয়েস্ট তৈরি করতে বিল্ট-ইন `GITHUB_TOKEN` ব্যবহার করে। আপনাকে ম্যানুয়ালি কোনো পার্সোনাল অ্যাক্সেস টোকেন (PAT) তৈরি করার **প্রয়োজন নেই**, তবে আপনাকে **অবশ্যই** নিশ্চিত করতে হবে যে ডিফল্ট টোকেনটির সঠিক অনুমতি (permissions) আছে:

1. আপনার রিপোজিটরির **Settings** -> **Actions** -> **General**-এ যান।
2. নিচে স্ক্রোল করে **Workflow permissions** সেকশনে যান।
3. **Read and write permissions** নির্বাচন করুন।
4. **Save**-এ ক্লিক করুন।
5. আপনার ওয়ার্কফ্লো YAML ফাইলে, ব্যবহারবিধি উদাহরণের মতো `github_token` ইনপুটে কেবল `${{ secrets.GITHUB_TOKEN }}` পাস করুন।

## 📄 লাইসেন্স (License)

এই প্রজেক্টটি MIT লাইসেন্সের অধীনে লাইসেন্সকৃত - বিস্তারিত জানতে [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) ফাইলটি দেখুন।