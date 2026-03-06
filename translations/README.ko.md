> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Gemini API를 사용하여 `README.md`를 여러 언어로 자동 번역하는 GitHub Action입니다. 모든 파일에 상호 연결된 언어 탐색 메뉴를 지능적으로 주입하며, 변경 사항을 직접 커밋하거나 리뷰를 위한 풀 리퀘스트(Pull Request)를 생성할 수 있습니다.

## 🚀 주요 기능
* **다국어 지원:** 한 번의 실행으로 여러 언어의 README를 생성합니다.
* **자동 탐색:** 파일 상단에 표준 언어 전환 메뉴를 자동으로 삽입하고 유지 관리합니다(비활성화 가능). AI가 자동으로 스타일을 지정합니다!
* **사용자 지정 스타일링:** 사용자 지정 메뉴 스타일 매개변수를 제공하여 AI가 원하는 방식으로 언어 전환기 포맷을 지정하도록 할 수 있습니다.

* **토큰 추적:** Gemini 토큰 사용량 통계를 출력합니다.

## 🛠 사용법

워크플로 파일(예: `.github/workflows/translate.yml`)을 생성합니다:

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

## 📥 입력

| 입력 | 필수 여부 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `api_key` | 예 |  | Google Gemini API 키입니다. |
| `github_token` | 예 |  | 표준 GitHub 토큰입니다 (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | 예 |  | 쉼표로 구분된 대상 언어입니다 (예: `ru, es`). |
| `output_dir` | 아니요 | | 번역된 파일을 저장할 디렉터리입니다. 기본값은 원본 파일의 디렉터리입니다. |
| `add_language_menu` | 아니요 | `true` | 언어 메뉴의 자동 생성을 비활성화하려면 `false`로 설정합니다. |
| `menu_style` | 아니요 | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | AI가 새 언어 메뉴를 생성할 때 사용하는 참조 스타일입니다. |
| `commit_message` | 아니요 | `docs: auto-translate README via Gemini` | git 커밋 메시지에 사용되는 텍스트입니다. |
| `model` | 아니요 | `gemini-3.1-pro-preview` | 사용할 Gemini 모델입니다. |
| `source_file` | 아니요 | `README.md` | 번역할 기본 파일입니다. |

## 🔑 Google Gemini API 키 발급 방법

이 Action을 사용하려면 Google AI Studio에서 무료 API 키를 발급받아야 합니다:

1. [Google AI Studio](https://aistudio.google.com/)로 이동합니다.
2. Google 계정으로 로그인합니다.
3. 왼쪽 탐색 메뉴에서 **Get API key**를 클릭합니다.
4. **Create API key** 버튼을 클릭합니다.
5. 생성된 키를 복사합니다.
6. GitHub 리포지토리의 **Settings** -> **Secrets and variables** -> **Actions**로 이동합니다.
7. **New repository secret**을 클릭하고, 이름을 `GEMINI_API_KEY`로 지정한 후, 복사한 키를 Secret 필드에 붙여넣고 저장합니다.

## 🔑 표준 GitHub 토큰 구성 방법

이 Action은 내장된 `GITHUB_TOKEN`을 사용하여 커밋을 푸시하거나 풀 리퀘스트(Pull Request)를 생성합니다. 개인 액세스 토큰(PAT)을 수동으로 생성할 필요는 **없지만**, 기본 토큰에 올바른 권한이 있는지 **반드시** 확인해야 합니다:

1. 리포지토리의 **Settings** -> **Actions** -> **General**로 이동합니다.
2. **Workflow permissions** 섹션으로 아래로 스크롤합니다.
3. **Read and write permissions**를 선택합니다.
4. **Save**를 클릭합니다.
5. 워크플로 YAML 파일에서, (사용법 예제에 나와 있는 것처럼) `${{ secrets.GITHUB_TOKEN }}`을 `github_token` 입력으로 전달하기만 하면 됩니다.

## 📄 라이선스

이 프로젝트는 MIT 라이선스에 따라 라이선스가 부여됩니다. 자세한 내용은 [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) 파일을 참조하세요.