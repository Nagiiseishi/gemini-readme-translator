> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Una GitHub Action che traduce automaticamente il tuo `README.md` in più lingue utilizzando l'API di Gemini. Inserisce in modo intelligente un menu di navigazione delle lingue con collegamenti incrociati in tutti i file e può eseguire direttamente il commit delle modifiche o creare una Pull Request per la revisione.

## 🚀 Funzionalità
* **Supporto multilingua:** Genera README per più lingue in una singola esecuzione.
* **Navigazione automatica:** Inserisce e mantiene automaticamente un menu standard per il cambio lingua in cima ai tuoi file (può essere disabilitato). L'IA lo formatta automaticamente!
* **Stile personalizzato:** Puoi fornire un parametro per lo stile del menu in modo che l'IA formatti il selettore di lingua esattamente come desideri.
* **Tracciamento dei token:** Restituisce le statistiche sull'utilizzo dei token di Gemini.

## 🛠 Utilizzo

Crea un file di workflow (es. `.github/workflows/translate.yml`):

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

## 📥 Input

| Input | Obbligatorio | Predefinito | Descrizione |
| --- | --- | --- | --- |
| `api_key` | Sì |  | La tua chiave API di Google Gemini. |
| `github_token` | Sì |  | Token standard di GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Sì |  | Lingue di destinazione separate da virgola (es. `ru, es`). |
| `output_dir` | No | | Directory in cui salvare i file tradotti. Per impostazione predefinita è la directory del file di origine. |
| `add_language_menu` | No | `true` | Imposta su `false` per disabilitare la generazione automatica del menu delle lingue. |
| `menu_style` | No | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Lo stile di riferimento che l'IA utilizza quando genera un nuovo menu delle lingue. |
| `commit_message` | No | `docs: auto-translate README via Gemini` | Testo utilizzato per il messaggio di commit git. |
| `model` | No | `gemini-3.1-pro-preview` | Il modello Gemini da utilizzare. |
| `source_file` | No | `README.md` | Il file di base da tradurre. |

## 🔑 Come ottenere una chiave API di Google Gemini

Per utilizzare questa action, hai bisogno di una chiave API gratuita da Google AI Studio:

1. Vai su [Google AI Studio](https://aistudio.google.com/).
2. Accedi con il tuo account Google.
3. Nel menu di navigazione a sinistra, fai clic su **Get API key**.
4. Fai clic sul pulsante **Create API key**.
5. Copia la chiave generata.
6. Vai al tuo repository GitHub -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Fai clic su **New repository secret**, chiamalo `GEMINI_API_KEY`, incolla la tua chiave nel campo Secret e salva.

## 🔑 Come configurare il token standard di GitHub

Questa action utilizza il `GITHUB_TOKEN` integrato per inviare commit o creare Pull Request. **Non** è necessario creare manualmente un Personal Access Token (PAT), ma **devi** assicurarti che il token predefinito abbia i permessi corretti:

1. Vai nel tuo repository su **Settings** -> **Actions** -> **General**.
2. Scorri in basso fino alla sezione **Workflow permissions**.
3. Seleziona **Read and write permissions**.
4. Fai clic su **Save**.
5. Nel tuo YAML di workflow, passa semplicemente `${{ secrets.GITHUB_TOKEN }}` all'input `github_token` (come mostrato nell'esempio di utilizzo).

## 📄 Licenza

Questo progetto è concesso in licenza ai sensi della Licenza MIT: vedi il file [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) per i dettagli.