> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# מתרגם ה-README של Gemini

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action המתרגם אוטומטית את קובץ ה-`README.md` שלך למספר שפות באמצעות ממשק ה-API של Gemini. הוא משלב באופן חכם תפריט ניווט שפות המקושר בין כל הקבצים ויכול לבצע commit לשינויים ישירות או ליצור Pull Request לבדיקה.

## 🚀 תכונות
* **תמיכה בריבוי שפות:** צור קבצי README עבור מספר שפות בהרצה אחת.
* **ניווט אוטומטי:** מכניס ומתחזק אוטומטית תפריט החלפת שפות סטנדרטי בראש הקבצים שלך (ניתן לביטול). ה-AI מעצב אותו אוטומטית!
* **עיצוב מותאם אישית:** באפשרותך לספק פרמטר עיצוב תפריט מותאם אישית כדי שה-AI יעצב את מחליף השפות בדיוק כפי שתרצה.
* **מעקב אחר אסימונים (Tokens):** מציג סטטיסטיקות של שימוש באסימונים של Gemini.

## 🛠 שימוש

צור קובץ workflow (לדוגמה, `.github/workflows/translate.yml`):

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

## 📥 קלטים (Inputs)

| קלט | חובה | ברירת מחדל | תיאור |
| --- | --- | --- | --- |
| `api_key` | כן |  | מפתח ה-API של Google Gemini שלך. |
| `github_token` | כן |  | אסימון GitHub סטנדרטי (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | כן |  | שפות יעד מופרדות בפסיקים (לדוגמה `ru, es`). |
| `output_dir` | לא | | תיקייה לשמירת הקבצים המתורגמים. ברירת המחדל היא התיקייה של קובץ המקור. |
| `add_language_menu` | לא | `true` | הגדר כ-`false` כדי להשבית יצירה אוטומטית של תפריט השפות. |
| `menu_style` | לא | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | סגנון הייחוס בו ה-AI משתמש בעת יצירת תפריט שפות חדש. |
| `commit_message` | לא | `docs: auto-translate README via Gemini` | הטקסט שישמש כהודעת ה-commit ב-git. |
| `model` | לא | `gemini-3.1-pro-preview` | מודל ה-Gemini לשימוש. |
| `source_file` | לא | `README.md` | קובץ הבסיס לתרגום. |

## 🔑 כיצד להשיג מפתח API של Google Gemini

כדי להשתמש ב-Action זה, תזדקק למפתח API חינמי מ-Google AI Studio:

1. עבור אל [Google AI Studio](https://aistudio.google.com/).
2. היכנס עם חשבון ה-Google שלך.
3. בתפריט הניווט השמאלי, לחץ על **Get API key**.
4. לחץ על הכפתור **Create API key**.
5. העתק את המפתח שנוצר.
6. עבור למאגר ה-GitHub שלך -> **Settings** -> **Secrets and variables** -> **Actions**.
7. לחץ על **New repository secret**, תן לו את השם `GEMINI_API_KEY`, הדבק את המפתח שלך בשדה Secret, ושמור.

## 🔑 כיצד להגדיר את אסימון ה-GitHub הסטנדרטי

Action זה משתמש ב-`GITHUB_TOKEN` המובנה כדי לדחוף (push) commits או ליצור Pull Requests. **אינך** צריך ליצור Personal Access Token (PAT) ידנית, אך **חובה** עליך לוודא שלאסימון ברירת המחדל יש את ההרשאות המתאימות:

1. עבור למאגר שלך **Settings** -> **Actions** -> **General**.
2. גלול למטה לאזור **Workflow permissions**.
3. בחר **Read and write permissions**.
4. לחץ **Save**.
5. בקובץ ה-YAML של ה-workflow שלך, פשוט העבר את `${{ secrets.GITHUB_TOKEN }}` לקלט `github_token` (כפי שמוצג בדוגמת השימוש).

## 📄 רישיון

פרויקט זה מורשה תחת רישיון MIT - ראו את קובץ ה-[LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) לפרטים נוספים.