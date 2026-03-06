> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Sebuah GitHub Action yang secara otomatis menerjemahkan `README.md` Anda ke dalam berbagai bahasa menggunakan API Gemini. Alat ini secara cerdas menyisipkan menu navigasi bahasa yang saling terhubung ke dalam semua file dan dapat melakukan commit perubahan secara langsung atau membuat Pull Request untuk ditinjau.

## 🚀 Fitur
* **Dukungan Multi-Bahasa:** Buat README untuk berbagai bahasa dalam satu kali proses.
* **Navigasi Otomatis:** Menyisipkan dan memelihara menu pengalih bahasa standar secara otomatis di bagian atas file Anda (dapat dinonaktifkan). AI akan mengatur gayanya secara otomatis!
* **Gaya Kustom:** Anda dapat memberikan parameter gaya menu kustom sehingga AI memformat pengalih bahasa persis seperti yang Anda inginkan.

* **Pelacakan Token:** Menampilkan statistik penggunaan token Gemini.

## 🛠 Penggunaan

Buat file alur kerja (contoh: `.github/workflows/translate.yml`):

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

| Input | Wajib | Default | Deskripsi |
| --- | --- | --- | --- |
| `api_key` | Ya |  | Kunci API Google Gemini Anda. |
| `github_token` | Ya |  | Token standar GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Ya |  | Bahasa target yang dipisahkan dengan koma (contoh: `ru, es`). |
| `output_dir` | Tidak | | Direktori untuk menyimpan file hasil terjemahan. Default-nya adalah direktori file sumber. |
| `add_language_menu` | Tidak | `true` | Atur ke `false` untuk menonaktifkan pembuatan otomatis menu bahasa. |
| `menu_style` | Tidak | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Gaya referensi yang digunakan AI saat membuat menu bahasa baru. |
| `commit_message` | Tidak | `docs: auto-translate README via Gemini` | Teks yang digunakan untuk pesan commit git. |
| `model` | Tidak | `gemini-3.1-pro-preview` | Model Gemini yang akan digunakan. |
| `source_file` | Tidak | `README.md` | File dasar yang akan diterjemahkan. |

## 🔑 Cara mendapatkan Kunci API Google Gemini

Untuk menggunakan action ini, Anda memerlukan kunci API gratis dari Google AI Studio:

1. Kunjungi [Google AI Studio](https://aistudio.google.com/).
2. Masuk menggunakan akun Google Anda.
3. Pada menu navigasi di sebelah kiri, klik **Get API key**.
4. Klik tombol **Create API key**.
5. Salin kunci yang dihasilkan.
6. Buka repositori GitHub Anda -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Klik **New repository secret**, beri nama `GEMINI_API_KEY`, tempelkan kunci Anda ke kolom Secret, dan simpan.

## 🔑 Cara mengonfigurasi Token Standar GitHub

Action ini menggunakan `GITHUB_TOKEN` bawaan untuk mendorong (push) commit atau membuat Pull Request. Anda **tidak** perlu membuat Personal Access Token (PAT) secara manual, tetapi Anda **harus** memastikan bahwa token default tersebut memiliki izin (permissions) yang benar:

1. Buka **Settings** repositori Anda -> **Actions** -> **General**.
2. Gulir ke bawah hingga ke bagian **Workflow permissions**.
3. Pilih **Read and write permissions**.
4. Klik **Save**.
5. Dalam YAML alur kerja Anda, cukup berikan `${{ secrets.GITHUB_TOKEN }}` pada input `github_token` (seperti yang ditunjukkan pada contoh penggunaan).

## 📄 Lisensi

Proyek ini dilisensikan di bawah Lisensi MIT - lihat file [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) untuk detailnya.