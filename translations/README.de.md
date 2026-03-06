> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Eine GitHub Action, die Ihre `README.md` mithilfe der Gemini API automatisch in mehrere Sprachen übersetzt. Sie fügt auf intelligente Weise ein querverlinktes Sprachnavigationsmenü in alle Dateien ein und kann Änderungen entweder direkt committen oder einen Pull Request zur Überprüfung erstellen.

## 🚀 Funktionen
* **Mehrsprachige Unterstützung:** Generieren Sie READMEs für mehrere Sprachen in einem einzigen Durchlauf.
* **Auto-Navigation:** Fügt automatisch ein Standard-Sprachauswahlmenü oben in Ihren Dateien ein und pflegt dieses (kann deaktiviert werden). Die KI formatiert es automatisch!
* **Benutzerdefiniertes Styling:** Sie können einen Parameter für ein benutzerdefiniertes Menü-Design angeben, damit die KI den Sprachumschalter genau so formatiert, wie Sie es möchten.
* **Token-Tracking:** Gibt Statistiken zur Nutzung von Gemini-Tokens aus.

## 🛠 Verwendung

Erstellen Sie eine Workflow-Datei (z. B. `.github/workflows/translate.yml`):

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

## 📥 Eingaben

| Eingabe | Erforderlich | Standard | Beschreibung |
| --- | --- | --- | --- |
| `api_key` | Ja |  | Ihr Google Gemini API-Schlüssel. |
| `github_token` | Ja |  | Standard-GitHub-Token (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ja |  | Kommagetrennte Zielsprachen (z. B. `ru, es`). |
| `output_dir` | Nein | | Verzeichnis zum Speichern der übersetzten Dateien. Standardmäßig das Verzeichnis der Quelldatei. |
| `add_language_menu` | Nein | `true` | Auf `false` setzen, um die automatische Generierung des Sprachmenüs zu deaktivieren. |
| `menu_style` | Nein | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Der Referenzstil, den die KI verwendet, wenn sie ein neues Sprachmenü generiert. |
| `commit_message` | Nein | `docs: auto-translate README via Gemini` | Text, der für die Git-Commit-Nachricht verwendet wird. |
| `model` | Nein | `gemini-3.1-pro-preview` | Das zu verwendende Gemini-Modell. |
| `source_file` | Nein | `README.md` | Die zu übersetzende Basisdatei. |

## 🔑 So erhalten Sie einen Google Gemini API-Schlüssel

Um diese Action zu nutzen, benötigen Sie einen kostenlosen API-Schlüssel von Google AI Studio:

1. Gehen Sie zu [Google AI Studio](https://aistudio.google.com/).
2. Melden Sie sich mit Ihrem Google-Konto an.
3. Klicken Sie im linken Navigationsmenü auf **Get API key**.
4. Klicken Sie auf die Schaltfläche **Create API key**.
5. Kopieren Sie den generierten Schlüssel.
6. Gehen Sie zu Ihrem GitHub-Repository -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klicken Sie auf **New repository secret**, benennen Sie es `GEMINI_API_KEY`, fügen Sie Ihren Schlüssel in das Feld "Secret" ein und speichern Sie.

## 🔑 So konfigurieren Sie das Standard-GitHub-Token

Diese Action verwendet das integrierte `GITHUB_TOKEN`, um Commits zu pushen oder Pull Requests zu erstellen. Sie müssen **kein** Personal Access Token (PAT) manuell erstellen, aber Sie **müssen** sicherstellen, dass das Standard-Token über die richtigen Berechtigungen verfügt:

1. Gehen Sie zu den Repository-Einstellungen (**Settings**) -> **Actions** -> **General**.
2. Scrollen Sie nach unten zum Abschnitt **Workflow permissions**.
3. Wählen Sie **Read and write permissions**.
4. Klicken Sie auf **Save**.
5. Übergeben Sie in Ihrem Workflow-YAML einfach `${{ secrets.GITHUB_TOKEN }}` an die Eingabe `github_token` (wie im Verwendungsbeispiel gezeigt).

## 📄 Lizenz

Dieses Projekt ist unter der MIT-Lizenz lizenziert - siehe die Datei [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) für Details.