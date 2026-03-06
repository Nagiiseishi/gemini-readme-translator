> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Çevirmeni

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Gemini API'sini kullanarak `README.md` dosyanızı otomatik olarak birden çok dile çeviren bir GitHub Eylemi. Tüm dosyalara çapraz bağlantılı bir dil gezinme menüsünü akıllıca enjekte eder ve değişiklikleri doğrudan işleyebilir (commit) veya inceleme için bir Çekme İsteği (Pull Request) oluşturabilir.

## 🚀 Özellikler
* **Çoklu Dil Desteği:** Tek bir çalıştırmada birden fazla dil için README dosyaları oluşturun.
* **Otomatik Gezinme:** Dosyalarınızın en üstüne standart bir dil değiştirici menüsünü otomatik olarak ekler ve korur (devre dışı bırakılabilir). Yapay Zeka bunu otomatik olarak biçimlendirir!
* **Özel Biçimlendirme:** Yapay Zekanın dil değiştiriciyi tam olarak istediğiniz gibi biçimlendirmesi için özel bir menü stili parametresi sağlayabilirsiniz.
* **Jeton (Token) Takibi:** Gemini jeton kullanım istatistiklerini çıktı olarak verir.

## 🛠 Kullanım

Bir iş akışı dosyası oluşturun (örneğin, `.github/workflows/translate.yml`):

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

## 📥 Girdiler

| Girdi | Gerekli | Varsayılan | Açıklama |
| --- | --- | --- | --- |
| `api_key` | Evet |  | Google Gemini API Anahtarınız. |
| `github_token` | Evet |  | Standart GitHub belirteci (token) (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Evet |  | Virgülle ayrılmış hedef diller (ör. `ru, es`). |
| `output_dir` | Hayır | | Çevrilmiş dosyaların kaydedileceği dizin. Varsayılan olarak kaynak dosyanın dizinidir. |
| `add_language_menu` | Hayır | `true` | Dil menüsünün otomatik oluşturulmasını devre dışı bırakmak için `false` olarak ayarlayın. |
| `menu_style` | Hayır | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | Yeni bir dil menüsü oluştururken yapay zekanın kullandığı referans stili. |
| `commit_message` | Hayır | `docs: auto-translate README via Gemini` | Git commit mesajı için kullanılan metin. |
| `model` | Hayır | `gemini-3.1-pro-preview` | Kullanılacak Gemini modeli. |
| `source_file` | Hayır | `README.md` | Çevrilecek temel dosya. |

## 🔑 Google Gemini API Anahtarı nasıl alınır

Bu eylemi kullanmak için Google AI Studio'dan ücretsiz bir API anahtarına ihtiyacınız vardır:

1. [Google AI Studio](https://aistudio.google.com/) adresine gidin.
2. Google hesabınızla giriş yapın.
3. Sol gezinme menüsünde **Get API key** (API anahtarı al) seçeneğine tıklayın.
4. **Create API key** (API anahtarı oluştur) düğmesine tıklayın.
5. Oluşturulan anahtarı kopyalayın.
6. GitHub deponuza gidin -> **Settings** (Ayarlar) -> **Secrets and variables** (Sırlar ve değişkenler) -> **Actions** (Eylemler).
7. **New repository secret** (Yeni depo sırrı) düğmesine tıklayın, adını `GEMINI_API_KEY` yapın, anahtarınızı Secret (Sır) alanına yapıştırın ve kaydedin.

## 🔑 Standart GitHub Token (Belirteç) nasıl yapılandırılır

Bu eylem, işlemeleri (commit) göndermek veya Çekme İstekleri (Pull Request) oluşturmak için yerleşik `GITHUB_TOKEN`'ı kullanır. Manuel olarak bir Kişisel Erişim Belirteci (PAT) oluşturmanıza **gerek yoktur**, ancak varsayılan belirtecin doğru izinlere sahip olduğundan emin **olmalısınız**:

1. Deponuzun **Settings** (Ayarlar) -> **Actions** (Eylemler) -> **General** (Genel) bölümüne gidin.
2. **Workflow permissions** (İş akışı izinleri) bölümüne kaydırın.
3. **Read and write permissions** (Okuma ve yazma izinleri) seçeneğini seçin.
4. **Save** (Kaydet) düğmesine tıklayın.
5. İş akışı YAML dosyanızda, `${{ secrets.GITHUB_TOKEN }}` değerini `github_token` girdisine geçirmeniz yeterlidir (kullanım örneğinde gösterildiği gibi).

## 📄 Lisans

Bu proje MIT Lisansı altında lisanslanmıştır - detaylar için [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) dosyasına bakın.