> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action, które automatycznie tłumaczy Twój plik `README.md` na wiele języków za pomocą API Gemini. Inteligentnie wstrzykuje menu nawigacyjne języków z linkami krzyżowymi do wszystkich plików i może bezpośrednio zatwierdzić zmiany (commit) lub utworzyć Pull Request do recenzji.

## 🚀 Funkcje
* **Obsługa wielu języków:** Generuj pliki README dla wielu języków w jednym uruchomieniu.
* **Automatyczna nawigacja:** Automatycznie wstawia i utrzymuje standardowe menu przełączania języków na górze Twoich plików (można wyłączyć). AI stylizuje je automatycznie!
* **Niestandardowe stylizowanie:** Możesz podać niestandardowy parametr stylu menu, aby AI sformatowało przełącznik języków dokładnie tak, jak chcesz.
* **Śledzenie tokenów:** Zwraca statystyki zużycia tokenów Gemini.

## 🛠 Użycie

Utwórz plik przepływu pracy (np. `.github/workflows/translate.yml`):

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

## 📥 Parametry wejściowe

| Parametr | Wymagany | Domyślnie | Opis |
| --- | --- | --- | --- |
| `api_key` | Tak |  | Twój klucz API Google Gemini. |
| `github_token` | Tak |  | Standardowy token GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Tak |  | Docelowe języki oddzielone przecinkami (np. `ru, es`). |
| `output_dir` | Nie | | Katalog do zapisania przetłumaczonych plików. Domyślnie jest to katalog pliku źródłowego. |
| `add_language_menu` | Nie | `true` | Ustaw na `false`, aby wyłączyć automatyczne generowanie menu językowego. |
| `menu_style` | Nie | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Styl referencyjny, którego używa AI podczas generowania nowego menu językowego. |
| `commit_message` | Nie | `docs: auto-translate README via Gemini` | Tekst używany do komunikatu zatwierdzenia (commit) w git. |
| `model` | Nie | `gemini-3.1-pro-preview` | Model Gemini do użycia. |
| `source_file` | Nie | `README.md` | Plik bazowy do przetłumaczenia. |

## 🔑 Jak uzyskać klucz API Google Gemini

Aby skorzystać z tej akcji, potrzebujesz darmowego klucza API z Google AI Studio:

1. Przejdź do [Google AI Studio](https://aistudio.google.com/).
2. Zaloguj się na swoje konto Google.
3. W lewym menu nawigacyjnym kliknij **Get API key** (Pobierz klucz API).
4. Kliknij przycisk **Create API key** (Utwórz klucz API).
5. Skopiuj wygenerowany klucz.
6. Przejdź do swojego repozytorium na GitHubie -> **Settings** (Ustawienia) -> **Secrets and variables** (Sekrety i zmienne) -> **Actions** (Akcje).
7. Kliknij **New repository secret** (Nowy sekret repozytorium), nazwij go `GEMINI_API_KEY`, wklej swój klucz w polu Secret i zapisz.

## 🔑 Jak skonfigurować standardowy token GitHub

Ta akcja używa wbudowanego `GITHUB_TOKEN` do wypychania commitów lub tworzenia Pull Requestów. **Nie** musisz ręcznie tworzyć Personal Access Token (PAT), ale **musisz** upewnić się, że domyślny token ma odpowiednie uprawnienia:

1. Przejdź do repozytorium **Settings** (Ustawienia) -> **Actions** (Akcje) -> **General** (Ogólne).
2. Przewiń w dół do sekcji **Workflow permissions** (Uprawnienia przepływów pracy).
3. Wybierz **Read and write permissions** (Uprawnienia do odczytu i zapisu).
4. Kliknij **Save** (Zapisz).
5. W pliku YAML przepływu pracy po prostu przekaż `${{ secrets.GITHUB_TOKEN }}` do wejścia `github_token` (jak pokazano w przykładzie użycia).

## 📄 Licencja

Ten projekt jest udostępniany na licencji MIT - zobacz plik [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE), aby uzyskać szczegóły.