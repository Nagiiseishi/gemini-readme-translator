> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

GitHub Action ที่ช่วยแปลไฟล์ `README.md` ของคุณให้เป็นหลายภาษาโดยอัตโนมัติผ่าน Gemini API ซึ่งสามารถแทรกเมนูนำทางภาษาที่มีลิงก์เชื่อมโยงกันในทุกไฟล์ได้อย่างชาญฉลาด และสามารถคอมมิตการเปลี่ยนแปลงโดยตรงหรือสร้าง Pull Request เพื่อรอการตรวจสอบได้

## 🚀 คุณสมบัติ
* **รองรับหลายภาษา:** สร้างไฟล์ README สำหรับหลายภาษาในการทำงานเพียงครั้งเดียว
* **การนำทางอัตโนมัติ:** แทรกและรักษาเมนูสลับภาษามาตรฐานไว้ที่ด้านบนสุดของไฟล์คุณโดยอัตโนมัติ (สามารถปิดการใช้งานได้) AI จะจัดรูปแบบให้โดยอัตโนมัติ!
* **กำหนดรูปแบบเองได้:** คุณสามารถระบุพารามิเตอร์รูปแบบเมนูที่กำหนดเองได้ เพื่อให้ AI จัดรูปแบบตัวสลับภาษาให้ตรงตามความต้องการของคุณ
* **การติดตาม Token:** แสดงสถิติการใช้งาน Token ของ Gemini

## 🛠 วิธีใช้งาน

สร้างไฟล์ workflow (เช่น `.github/workflows/translate.yml`):

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

## 📥 ข้อมูลนำเข้า (Inputs)

| Input | จำเป็น (Required) | ค่าเริ่มต้น (Default) | คำอธิบาย (Description) |
| --- | --- | --- | --- |
| `api_key` | ใช่ |  | Google Gemini API Key ของคุณ |
| `github_token` | ใช่ |  | GitHub token มาตรฐาน (`${{ secrets.GITHUB_TOKEN }}`) |
| `languages` | ใช่ |  | ภาษาปลายทางที่คั่นด้วยเครื่องหมายจุลภาค (เช่น `ru, es`) |
| `output_dir` | ไม่ | | ไดเรกทอรีสำหรับบันทึกไฟล์ที่แปลแล้ว ค่าเริ่มต้นคือไดเรกทอรีของไฟล์ต้นฉบับ |
| `add_language_menu` | ไม่ | `true` | ตั้งค่าเป็น `false` เพื่อปิดใช้งานการสร้างเมนูภาษาอัตโนมัติ |
| `menu_style` | ไม่ | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | รูปแบบอ้างอิงที่ AI ใช้เมื่อสร้างเมนูภาษาใหม่ |
| `commit_message` | ไม่ | `docs: auto-translate README via Gemini` | ข้อความที่ใช้สำหรับคอมมิตของ git |
| `model` | ไม่ | `gemini-3.1-pro-preview` | โมเดล Gemini ที่จะใช้งาน |
| `source_file` | ไม่ | `README.md` | ไฟล์ต้นฉบับที่ต้องการแปล |

## 🔑 วิธีรับ Google Gemini API Key

ในการใช้งาน action นี้ คุณต้องมี API key ฟรีจาก Google AI Studio:

1. ไปที่ [Google AI Studio](https://aistudio.google.com/)
2. เข้าสู่ระบบด้วยบัญชี Google ของคุณ
3. ในเมนูการนำทางด้านซ้าย ให้คลิกที่ **Get API key**
4. คลิกปุ่ม **Create API key**
5. คัดลอกคีย์ที่สร้างขึ้นมา
6. ไปที่ repository ใน GitHub ของคุณ -> **Settings** -> **Secrets and variables** -> **Actions**
7. คลิก **New repository secret** ตั้งชื่อเป็น `GEMINI_API_KEY` วางคีย์ของคุณลงในช่อง Secret แล้วกดบันทึก (save)

## 🔑 วิธีตั้งค่า Standard GitHub Token

Action นี้ใช้ `GITHUB_TOKEN` ที่มีอยู่แล้วในระบบเพื่อพุช (push) คอมมิตหรือสร้าง Pull Request คุณ **ไม่จำเป็น** ต้องสร้าง Personal Access Token (PAT) ด้วยตัวเอง แต่คุณ **ต้อง** ตรวจสอบให้แน่ใจว่า token เริ่มต้นนี้มีสิทธิ์ที่ถูกต้อง:

1. ไปที่ **Settings** -> **Actions** -> **General** ของ repository คุณ
2. เลื่อนลงมาที่ส่วนของ **Workflow permissions**
3. เลือก **Read and write permissions**
4. คลิก **Save**
5. ในไฟล์ YAML สำหรับ workflow ของคุณ เพียงแค่ส่ง `${{ secrets.GITHUB_TOKEN }}` ไปยังอินพุต `github_token` (ดังที่แสดงในตัวอย่างวิธีการใช้งาน)

## 📄 สัญญาอนุญาต (License)

โปรเจกต์นี้อยู่ภายใต้สัญญาอนุญาต MIT - ดูรายละเอียดเพิ่มเติมได้ที่ไฟล์ [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE)