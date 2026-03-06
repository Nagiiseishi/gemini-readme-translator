> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Một GitHub Action tự động dịch tệp `README.md` của bạn sang nhiều ngôn ngữ khác nhau bằng cách sử dụng Gemini API. Nó tự động chèn một menu điều hướng ngôn ngữ liên kết chéo vào tất cả các tệp một cách thông minh và có thể tự động commit các thay đổi trực tiếp hoặc tạo một Pull Request để xem xét.

## 🚀 Tính năng
* **Hỗ trợ Đa ngôn ngữ:** Tạo tệp README cho nhiều ngôn ngữ trong một lần chạy.
* **Tự động Điều hướng:** Tự động chèn và duy trì một menu chuyển đổi ngôn ngữ chuẩn ở đầu các tệp của bạn (có thể vô hiệu hóa). AI sẽ tự động định dạng menu này!
* **Tùy chỉnh Định dạng:** Bạn có thể cung cấp một tham số kiểu menu tùy chỉnh để AI định dạng bộ chuyển đổi ngôn ngữ chính xác theo cách bạn muốn.

* **Theo dõi Token:** Xuất thông tin thống kê về việc sử dụng token của Gemini.

## 🛠 Sử dụng

Tạo một tệp workflow (ví dụ: `.github/workflows/translate.yml`):

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

## 📥 Đầu vào

| Đầu vào | Bắt buộc | Mặc định | Mô tả |
| --- | --- | --- | --- |
| `api_key` | Có |  | Google Gemini API Key của bạn. |
| `github_token` | Có |  | Token GitHub tiêu chuẩn (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Có |  | Các ngôn ngữ đích được phân tách bằng dấu phẩy (ví dụ: `ru, es`). |
| `output_dir` | Không | | Thư mục để lưu các tệp đã dịch. Mặc định là thư mục của tệp nguồn. |
| `add_language_menu` | Không | `true` | Đặt thành `false` để tắt tính năng tự động tạo menu ngôn ngữ. |
| `menu_style` | Không | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Kiểu tham chiếu mà AI sử dụng khi tạo một menu ngôn ngữ mới. |
| `commit_message` | Không | `docs: auto-translate README via Gemini` | Văn bản được sử dụng cho thông báo git commit. |
| `model` | Không | `gemini-3.1-pro-preview` | Mô hình Gemini sẽ được sử dụng. |
| `source_file` | Không | `README.md` | Tệp gốc cần dịch. |

## 🔑 Cách nhận API Key của Google Gemini

Để sử dụng action này, bạn cần một API key miễn phí từ Google AI Studio:

1. Truy cập [Google AI Studio](https://aistudio.google.com/).
2. Đăng nhập bằng tài khoản Google của bạn.
3. Ở menu điều hướng bên trái, nhấp vào **Get API key**.
4. Nhấp vào nút **Create API key**.
5. Sao chép key vừa được tạo.
6. Đi đến kho lưu trữ GitHub của bạn -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Nhấp vào **New repository secret**, đặt tên là `GEMINI_API_KEY`, dán key của bạn vào trường Secret, và lưu lại.

## 🔑 Cách cấu hình Standard GitHub Token

Action này sử dụng `GITHUB_TOKEN` được tích hợp sẵn để đẩy (push) các commit hoặc tạo Pull Request. Bạn **không cần** phải tạo Personal Access Token (PAT) theo cách thủ công, nhưng bạn **phải** đảm bảo token mặc định có các quyền chính xác:

1. Đi đến **Settings** -> **Actions** -> **General** trong kho lưu trữ của bạn.
2. Cuộn xuống phần **Workflow permissions**.
3. Chọn **Read and write permissions**.
4. Nhấp vào **Save**.
5. Trong tệp YAML của workflow, bạn chỉ cần truyền `${{ secrets.GITHUB_TOKEN }}` vào đầu vào `github_token` (như được hiển thị trong ví dụ sử dụng).

## 📄 Giấy phép

Dự án này được cấp phép theo Giấy phép MIT - xem tệp [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) để biết thêm chi tiết.