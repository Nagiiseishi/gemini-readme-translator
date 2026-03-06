> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# مترجم Gemini لملفات README

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

إجراء GitHub (GitHub Action) يقوم تلقائيًا بترجمة ملف `README.md` الخاص بك إلى لغات متعددة باستخدام واجهة برمجة تطبيقات Gemini (Gemini API). يقوم بذكاء بإدراج قائمة تنقل للغات مرتبطة ببعضها البعض في جميع الملفات ويمكنه إما إيداع التغييرات (commit) مباشرة أو إنشاء طلب سحب (Pull Request) للمراجعة.

## 🚀 الميزات
* **دعم لغات متعددة:** إنشاء ملفات README بلغات متعددة في عملية تشغيل واحدة.
* **التنقل التلقائي:** يقوم تلقائيًا بإدراج قائمة قياسية للتبديل بين اللغات في أعلى ملفاتك ويحافظ عليها (يمكن تعطيلها). يقوم الذكاء الاصطناعي بتنسيقها تلقائيًا!
* **تنسيق مخصص:** يمكنك توفير معامل نمط قائمة مخصص بحيث يقوم الذكاء الاصطناعي بتنسيق مبدل اللغة بالطريقة التي تريدها بالضبط.
* **تتبع الرموز (Tokens):** يخرج إحصائيات استخدام رموز Gemini.

## 🛠 الاستخدام

قم بإنشاء ملف سير عمل (على سبيل المثال، `.github/workflows/translate.yml`):

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

## 📥 المدخلات

| المدخل (Input) | مطلوب | الافتراضي | الوصف |
| --- | --- | --- | --- |
| `api_key` | نعم |  | مفتاح واجهة برمجة تطبيقات Google Gemini الخاص بك. |
| `github_token` | نعم |  | رمز GitHub القياسي (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | نعم |  | اللغات المستهدفة مفصولة بفواصل (مثل `ru, es`). |
| `output_dir` | لا | | الدليل لحفظ الملفات المترجمة. الافتراضي هو دليل الملف المصدر. |
| `add_language_menu` | لا | `true` | اضبط على `false` لتعطيل الإنشاء التلقائي لقائمة اللغات. |
| `menu_style` | لا | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | النمط المرجعي الذي يستخدمه الذكاء الاصطناعي عند إنشاء قائمة لغات جديدة. |
| `commit_message` | لا | `docs: auto-translate README via Gemini` | النص المستخدم لرسالة إيداع (commit) git. |
| `model` | لا | `gemini-3.1-pro-preview` | نموذج Gemini المراد استخدامه. |
| `source_file` | لا | `README.md` | الملف الأساسي المراد ترجمته. |

## 🔑 كيفية الحصول على مفتاح واجهة برمجة تطبيقات Google Gemini

لاستخدام هذا الإجراء، تحتاج إلى مفتاح واجهة برمجة تطبيقات مجاني من Google AI Studio:

1. اذهب إلى [Google AI Studio](https://aistudio.google.com/).
2. سجل الدخول باستخدام حساب Google الخاص بك.
3. في قائمة التنقل اليسرى، انقر على **Get API key** (الحصول على مفتاح واجهة برمجة التطبيقات).
4. انقر على زر **Create API key** (إنشاء مفتاح واجهة برمجة التطبيقات).
5. انسخ المفتاح المُنشأ.
6. اذهب إلى مستودع GitHub الخاص بك -> **Settings** (الإعدادات) -> **Secrets and variables** (الأسرار والمتغيرات) -> **Actions** (الإجراءات).
7. انقر على **New repository secret** (سر مستودع جديد)، وقم بتسميته `GEMINI_API_KEY`، ثم الصق المفتاح الخاص بك في حقل "Secret" (السر)، واحفظه.

## 🔑 كيفية تكوين رمز GitHub القياسي (Standard GitHub Token)

يستخدم هذا الإجراء الرمز المدمج `GITHUB_TOKEN` لدفع الإيداعات (commits) أو إنشاء طلبات سحب (Pull Requests). أنت **لست بحاجة** إلى إنشاء رمز وصول شخصي (PAT) يدويًا، ولكن **يجب عليك** التأكد من أن الرمز الافتراضي يمتلك الأذونات الصحيحة:

1. اذهب إلى **Settings** (الإعدادات) في مستودعك -> **Actions** (الإجراءات) -> **General** (عام).
2. قم بالتمرير لأسفل إلى قسم **Workflow permissions** (أذونات سير العمل).
3. حدد **Read and write permissions** (أذونات القراءة والكتابة).
4. انقر على **Save** (حفظ).
5. في ملف سير العمل YAML، ما عليك سوى تمرير `${{ secrets.GITHUB_TOKEN }}` إلى المدخل `github_token` (كما هو موضح في مثال الاستخدام).

## 📄 الترخيص

هذا المشروع مرخص بموجب ترخيص MIT - راجع ملف [الترخيص](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) (LICENSE) للحصول على التفاصيل.