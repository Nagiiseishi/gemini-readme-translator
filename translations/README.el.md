> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Μια ενέργεια του GitHub (GitHub Action) που μεταφράζει αυτόματα το `README.md` σας σε πολλαπλές γλώσσες χρησιμοποιώντας το API του Gemini. Εισάγει έξυπνα ένα μενού πλοήγησης γλωσσών με διασταυρούμενους συνδέσμους σε όλα τα αρχεία και μπορεί είτε να υποβάλει (commit) τις αλλαγές απευθείας είτε να δημιουργήσει ένα Pull Request για έλεγχο.

## 🚀 Χαρακτηριστικά
* **Υποστήριξη Πολλαπλών Γλωσσών:** Δημιουργία README για πολλαπλές γλώσσες σε μία εκτέλεση.
* **Αυτόματη Πλοήγηση:** Εισάγει και διατηρεί αυτόματα ένα τυπικό μενού εναλλαγής γλώσσας στην κορυφή των αρχείων σας (μπορεί να απενεργοποιηθεί). Η τεχνητή νοημοσύνη (AI) το μορφοποιεί αυτόματα!
* **Προσαρμοσμένη Μορφοποίηση:** Μπορείτε να παρέχετε μια παράμετρο προσαρμοσμένου στιλ μενού, ώστε η AI να μορφοποιήσει τον διακόπτη γλώσσας ακριβώς όπως τον θέλετε.
* **Παρακολούθηση Token:** Εξάγει στατιστικά στοιχεία χρήσης των token του Gemini.

## 🛠 Χρήση

Δημιουργήστε ένα αρχείο ροής εργασιών (π.χ., `.github/workflows/translate.yml`):

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

## 📥 Είσοδοι (Inputs)

| Είσοδος | Απαιτείται | Προεπιλογή | Περιγραφή |
| --- | --- | --- | --- |
| `api_key` | Ναι |  | Το κλειδί API (API Key) του Google Gemini. |
| `github_token` | Ναι |  | Τυπικό token του GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ναι |  | Γλώσσες στόχοι διαχωρισμένες με κόμμα (π.χ. `ru, es`). |
| `output_dir` | Όχι | | Κατάλογος για την αποθήκευση των μεταφρασμένων αρχείων. Προεπιλογή είναι ο κατάλογος του αρχικού αρχείου. |
| `add_language_menu` | Όχι | `true` | Ορίστε το σε `false` για να απενεργοποιήσετε την αυτόματη δημιουργία του μενού γλωσσών. |
| `menu_style` | Όχι | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Το στιλ αναφοράς που χρησιμοποιεί η AI κατά τη δημιουργία ενός νέου μενού γλωσσών. |
| `commit_message` | Όχι | `docs: auto-translate README via Gemini` | Κείμενο που χρησιμοποιείται για το μήνυμα του git commit. |
| `model` | Όχι | `gemini-3.1-pro-preview` | Το μοντέλο Gemini που θα χρησιμοποιηθεί. |
| `source_file` | Όχι | `README.md` | Το βασικό αρχείο προς μετάφραση. |

## 🔑 Πώς να αποκτήσετε ένα API Key για το Google Gemini

Για να χρησιμοποιήσετε αυτήν την ενέργεια, χρειάζεστε ένα δωρεάν API key από το Google AI Studio:

1. Μεταβείτε στο [Google AI Studio](https://aistudio.google.com/).
2. Συνδεθείτε με τον λογαριασμό σας Google.
3. Στο αριστερό μενού πλοήγησης, κάντε κλικ στο **Get API key** (Λήψη κλειδιού API).
4. Κάντε κλικ στο κουμπί **Create API key** (Δημιουργία κλειδιού API).
5. Αντιγράψτε το κλειδί που δημιουργήθηκε.
6. Μεταβείτε στο αποθετήριο σας στο GitHub -> **Settings** (Ρυθμίσεις) -> **Secrets and variables** (Μυστικά και μεταβλητές) -> **Actions** (Ενέργειες).
7. Κάντε κλικ στο **New repository secret** (Νέο μυστικό αποθετηρίου), ονομάστε το `GEMINI_API_KEY`, επικολλήστε το κλειδί σας στο πεδίο Secret και αποθηκεύστε.

## 🔑 Πώς να διαμορφώσετε το Τυπικό Token του GitHub

Αυτή η ενέργεια χρησιμοποιεί το ενσωματωμένο `GITHUB_TOKEN` για την προώθηση των commits ή τη δημιουργία Pull Requests. **Δεν** χρειάζεται να δημιουργήσετε ένα Προσωπικό Token Πρόσβασης (PAT) χειροκίνητα, αλλά **πρέπει** να βεβαιωθείτε ότι το προεπιλεγμένο token έχει τα σωστά δικαιώματα:

1. Μεταβείτε στο αποθετήριο σας **Settings** (Ρυθμίσεις) -> **Actions** (Ενέργειες) -> **General** (Γενικά).
2. Κάντε κύλιση προς τα κάτω στην ενότητα **Workflow permissions** (Δικαιώματα ροής εργασιών).
3. Επιλέξτε **Read and write permissions** (Δικαιώματα ανάγνωσης και εγγραφής).
4. Κάντε κλικ στο **Save** (Αποθήκευση).
5. Στο YAML της ροής εργασιών σας, απλά περάστε το `${{ secrets.GITHUB_TOKEN }}` στην είσοδο `github_token` (όπως φαίνεται στο παράδειγμα χρήσης).

## 📄 Άδεια

Αυτό το έργο αδειοδοτείται υπό την Άδεια MIT - δείτε το αρχείο [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) για λεπτομέρειες.