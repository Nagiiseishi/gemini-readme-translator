> 🌐 **Langues :** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Une GitHub Action qui traduit automatiquement votre `README.md` en plusieurs langues à l'aide de l'API Gemini. Elle injecte intelligemment un menu de navigation linguistique avec des liens croisés dans tous les fichiers et peut soit commiter les modifications directement, soit créer une Pull Request pour révision.

## 🚀 Fonctionnalités
* **Support multilingue :** Générez des READMEs pour plusieurs langues en une seule exécution.
* **Navigation automatique :** Insère et maintient automatiquement un menu standard de changement de langue en haut de vos fichiers (peut être désactivé). L'IA le stylise automatiquement !
* **Style personnalisé :** Vous pouvez fournir un paramètre de style de menu personnalisé afin que l'IA formate le sélecteur de langue exactement comme vous le souhaitez.

* **Suivi des jetons :** Affiche les statistiques d'utilisation des jetons Gemini.

## 🛠 Utilisation

Créez un fichier de workflow (par exemple, `.github/workflows/translate.yml`) :

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

## 📥 Entrées

| Entrée | Requis | Défaut | Description |
| --- | --- | --- | --- |
| `api_key` | Oui |  | Votre clé API Google Gemini. |
| `github_token` | Oui |  | Jeton GitHub standard (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Oui |  | Langues cibles séparées par des virgules (ex. `ru, es`). |
| `output_dir` | Non | | Répertoire où sauvegarder les fichiers traduits. Par défaut, le répertoire du fichier source. |
| `add_language_menu` | Non | `true` | Définissez sur `false` pour désactiver la génération automatique du menu des langues. |
| `menu_style` | Non | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Le style de référence utilisé par l'IA lors de la génération d'un nouveau menu des langues. |
| `commit_message` | Non | `docs: auto-translate README via Gemini` | Texte utilisé pour le message du commit git. |
| `model` | Non | `gemini-3.1-pro-preview` | Le modèle Gemini à utiliser. |
| `source_file` | Non | `README.md` | Le fichier de base à traduire. |

## 🔑 Comment obtenir une clé API Google Gemini

Pour utiliser cette action, vous avez besoin d'une clé API gratuite de Google AI Studio :

1. Allez sur [Google AI Studio](https://aistudio.google.com/).
2. Connectez-vous avec votre compte Google.
3. Dans le menu de navigation de gauche, cliquez sur **Get API key**.
4. Cliquez sur le bouton **Create API key**.
5. Copiez la clé générée.
6. Allez dans votre dépôt GitHub -> **Settings** (Paramètres) -> **Secrets and variables** -> **Actions**.
7. Cliquez sur **New repository secret**, nommez-le `GEMINI_API_KEY`, collez votre clé dans le champ Secret, et enregistrez.

## 🔑 Comment configurer le jeton GitHub standard

Cette action utilise le `GITHUB_TOKEN` intégré pour pousser les commits ou créer des Pull Requests. Vous **n'avez pas** besoin de créer manuellement un jeton d'accès personnel (PAT), mais vous **devez** vous assurer que le jeton par défaut dispose des autorisations correctes :

1. Allez dans les **Paramètres** (Settings) de votre dépôt -> **Actions** -> **Général** (General).
2. Faites défiler jusqu'à la section **Autorisations du workflow** (Workflow permissions).
3. Sélectionnez **Autorisations de lecture et d'écriture** (Read and write permissions).
4. Cliquez sur **Enregistrer** (Save).
5. Dans votre fichier YAML de workflow, passez simplement `${{ secrets.GITHUB_TOKEN }}` à l'entrée `github_token` (comme indiqué dans l'exemple d'utilisation).

## 📄 Licence

Ce projet est sous licence MIT - voir le fichier [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) pour plus de détails.