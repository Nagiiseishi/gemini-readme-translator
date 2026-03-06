> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# مترجم Gemini README

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

یک اکشن گیت‌هاب (GitHub Action) که به‌طور خودکار فایل `README.md` شما را با استفاده از API جمنای به چندین زبان ترجمه می‌کند. این ابزار به‌طور هوشمند یک منوی ناوبری زبان متصل‌به‌هم را در تمامی فایل‌ها تزریق می‌کند و می‌تواند تغییرات را مستقیماً کامیت (commit) کند یا یک درخواست ادغام (Pull Request) برای بررسی ایجاد نماید.

## 🚀 ویژگی‌ها
* **پشتیبانی از چند زبان:** تولید فایل‌های README برای چندین زبان تنها در یک بار اجرا.
* **ناوبری خودکار:** به‌طور خودکار یک منوی استاندارد برای تغییر زبان را در بالای فایل‌های شما وارد و نگهداری می‌کند (قابل غیرفعال‌سازی). هوش مصنوعی به‌طور خودکار به آن استایل می‌دهد!
* **استایل‌دهی سفارشی:** می‌توانید پارامتری برای استایل سفارشی منو ارائه دهید تا هوش مصنوعی انتخاب‌گر زبان را دقیقاً همان‌طور که می‌خواهید قالب‌بندی کند.
* **ردیابی توکن:** آمار مصرف توکن جمنای را خروجی می‌دهد.

## 🛠 نحوه استفاده

یک فایل جریان کاری (workflow) ایجاد کنید (به عنوان مثال، `.github/workflows/translate.yml`):

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

## 📥 ورودی‌ها

| ورودی | الزامی | پیش‌فرض | توضیحات |
| --- | --- | --- | --- |
| `api_key` | بله |  | کلید API گوگل جمنای شما. |
| `github_token` | بله |  | توکن استاندارد گیت‌هاب (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | بله |  | زبان‌های هدف با جداکننده کاما (مانند `ru, es`). |
| `output_dir` | خیر | | پوشه برای ذخیره فایل‌های ترجمه شده. به‌طور پیش‌فرض در پوشه فایل مبدأ ذخیره می‌شود. |
| `add_language_menu` | خیر | `true` | برای غیرفعال کردن تولید خودکار منوی زبان، آن را روی `false` تنظیم کنید. |
| `menu_style` | خیر | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | استایل مرجعی که هوش مصنوعی هنگام تولید منوی جدید زبان از آن استفاده می‌کند. |
| `commit_message` | خیر | `docs: auto-translate README via Gemini` | متن استفاده شده برای پیام کامیت گیت. |
| `model` | خیر | `gemini-3.1-pro-preview` | مدل جمنای برای استفاده. |
| `source_file` | خیر | `README.md` | فایل پایه‌ای که باید ترجمه شود. |

## 🔑 نحوه دریافت کلید API گوگل جمنای

برای استفاده از این اکشن، به یک کلید API رایگان از Google AI Studio نیاز دارید:

۱. به [Google AI Studio](https://aistudio.google.com/) بروید.
۲. با حساب کاربری گوگل خود وارد شوید.
۳. در منوی ناوبری سمت چپ، روی **Get API key** کلیک کنید.
۴. روی دکمه **Create API key** کلیک کنید.
۵. کلید تولید شده را کپی کنید.
۶. به مخزن گیت‌هاب خود بروید -> **Settings** -> **Secrets and variables** -> **Actions**.
۷. روی **New repository secret** کلیک کنید، نام آن را `GEMINI_API_KEY` بگذارید، کلید خود را در فیلد Secret جای‌گذاری کرده و ذخیره کنید.

## 🔑 نحوه پیکربندی توکن استاندارد گیت‌هاب

این اکشن از `GITHUB_TOKEN` داخلی برای پوش کردن کامیت‌ها یا ایجاد درخواست‌های ادغام (Pull Requests) استفاده می‌کند. شما **نیازی ندارید** یک توکن دسترسی شخصی (PAT) به‌صورت دستی ایجاد کنید، اما **باید** مطمئن شوید که توکن پیش‌فرض دسترسی‌های لازم را دارد:

۱. به مسیر **Settings** -> **Actions** -> **General** در مخزن خود بروید.
۲. به پایین و بخش **Workflow permissions** اسکرول کنید.
۳. گزینه **Read and write permissions** را انتخاب کنید.
۴. روی **Save** کلیک کنید.
۵. در فایل YAML جریان کاری خود، به‌سادگی `${{ secrets.GITHUB_TOKEN }}` را به ورودی `github_token` پاس دهید (همان‌طور که در مثال نحوه استفاده نشان داده شده است).

## 📄 مجوز

این پروژه تحت مجوز MIT منتشر شده است - برای جزئیات بیشتر به فایل [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) مراجعه کنید.