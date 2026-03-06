> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Uma GitHub Action que traduz automaticamente o seu `README.md` para vários idiomas usando a API do Gemini. Ela injeta de forma inteligente um menu de navegação de idiomas com links cruzados em todos os arquivos e pode submeter as alterações (commit) diretamente ou criar um Pull Request para revisão.

## 🚀 Recursos
* **Suporte a Vários Idiomas:** Gere READMEs para múltiplos idiomas em uma única execução.
* **Navegação Automática:** Insere e mantém automaticamente um menu padrão de alternância de idiomas no topo dos seus arquivos (pode ser desativado). A IA o estiliza automaticamente!
* **Estilização Personalizada:** Você pode fornecer um parâmetro de estilo de menu personalizado para que a IA formate o alternador de idiomas exatamente como você deseja.
* **Rastreamento de Tokens:** Exibe estatísticas de uso de tokens do Gemini.

## 🛠 Uso

Crie um arquivo de workflow (por exemplo, `.github/workflows/translate.yml`):

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

## 📥 Entradas

| Entrada | Obrigatório | Padrão | Descrição |
| --- | --- | --- | --- |
| `api_key` | Sim |  | Sua Chave de API do Google Gemini. |
| `github_token` | Sim |  | Token padrão do GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Sim |  | Idiomas de destino separados por vírgula (ex: `ru, es`). |
| `output_dir` | Não | | Diretório para salvar os arquivos traduzidos. O padrão é o diretório do arquivo de origem. |
| `add_language_menu` | Não | `true` | Defina como `false` para desativar a geração automática do menu de idiomas. |
| `menu_style` | Não | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | O estilo de referência que a IA usa ao gerar um novo menu de idiomas. |
| `commit_message` | Não | `docs: auto-translate README via Gemini` | Texto usado para a mensagem de commit do git. |
| `model` | Não | `gemini-3.1-pro-preview` | O modelo Gemini a ser usado. |
| `source_file` | Não | `README.md` | O arquivo base a ser traduzido. |

## 🔑 Como obter uma Chave de API do Google Gemini

Para usar esta action, você precisa de uma chave de API gratuita do Google AI Studio:

1. Acesse o [Google AI Studio](https://aistudio.google.com/).
2. Faça login com a sua conta do Google.
3. No menu de navegação esquerdo, clique em **Get API key**.
4. Clique no botão **Create API key**.
5. Copie a chave gerada.
6. Vá para o seu repositório do GitHub -> **Settings** -> **Secrets and variables** -> **Actions**.
7. Clique em **New repository secret**, nomeie como `GEMINI_API_KEY`, cole sua chave no campo Secret e salve.

## 🔑 Como configurar o Token Padrão do GitHub

Esta action usa o `GITHUB_TOKEN` integrado para fazer push de commits ou criar Pull Requests. Você **não** precisa criar um Token de Acesso Pessoal (PAT) manualmente, mas **deve** garantir que o token padrão tenha as permissões corretas:

1. Vá para as **Settings** (Configurações) do seu repositório -> **Actions** -> **General** (Geral).
2. Role para baixo até a seção **Workflow permissions** (Permissões de workflow).
3. Selecione **Read and write permissions** (Permissões de leitura e gravação).
4. Clique em **Save** (Salvar).
5. No seu YAML de workflow, simplesmente passe `${{ secrets.GITHUB_TOKEN }}` para a entrada `github_token` (como mostrado no exemplo de uso).

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) para mais detalhes.