> 🌐 **Languages:** [English](README.md) | [English (en)](translations/README.en.md) | [Русский](translations/README.ru.md) | [ไทย](translations/README.th.md) | [简体中文](translations/README.zh-CN.md) | [繁體中文](translations/README.zh-TW.md) | [हिन्दी](translations/README.hi.md) | [Español](translations/README.es.md) | [Français](translations/README.fr.md) | [العربية](translations/README.ar.md) | [বাংলা](translations/README.bn.md) | [Português](translations/README.pt.md) | [اردو](translations/README.ur.md) | [Bahasa Indonesia](translations/README.id.md) | [Deutsch](translations/README.de.md) | [日本語](translations/README.ja.md) | [मराठी](translations/README.mr.md) | [తెలుగు](translations/README.te.md) | [Türkçe](translations/README.tr.md) | [தமிழ்](translations/README.ta.md) | [Tiếng Việt](translations/README.vi.md) | [한국어](translations/README.ko.md) | [Kiswahili](translations/README.sw.md) | [Italiano](translations/README.it.md) | [ગુજરાતી](translations/README.gu.md) | [فارسی](translations/README.fa.md) | [ಕನ್ನಡ](translations/README.kn.md) | [Polski](translations/README.pl.md) | [മലയാളം](translations/README.ml.md) | [Українська](translations/README.uk.md) | [Română](translations/README.ro.md) | [Nederlands](translations/README.nl.md) | [Ελληνικά](translations/README.el.md) | [Magyar](translations/README.hu.md) | [Svenska](translations/README.sv.md) | [Čeština](translations/README.cs.md) | [Српски](translations/README.sr.md) | [עברית](translations/README.he.md) | [Български](translations/README.bg.md) | [Dansk](translations/README.da.md) | [Suomi](translations/README.fi.md) | [Norsk](translations/README.no.md) | [Slovenčina](translations/README.sk.md) | [Hrvatski](translations/README.hr.md) | [Lietuvių](translations/README.lt.md) | [Slovenščina](translations/README.sl.md) | [Latviešu](translations/README.lv.md) | [Eesti](translations/README.et.md)

# Gemini README Translator

[![CI Pipeline](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml/badge.svg)](https://github.com/artryazanov/gemini-readme-translator/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/artryazanov/gemini-readme-translator/graph/badge.svg)](https://codecov.io/gh/artryazanov/gemini-readme-translator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

Una GitHub Action que traduce automáticamente tu `README.md` a múltiples idiomas utilizando la API de Gemini. Inyecta de forma inteligente un menú de navegación de idiomas con enlaces cruzados en todos los archivos y puede hacer un commit de los cambios directamente o crear un Pull Request para su revisión.

## 🚀 Características
* **Soporte Multilingüe:** Genera archivos README para múltiples idiomas en una sola ejecución.
* **Navegación Automática:** Inserta y mantiene automáticamente un menú estándar para cambiar de idioma en la parte superior de tus archivos (se puede desactivar). ¡La IA le da estilo automáticamente!
* **Estilos Personalizados:** Puedes proporcionar un parámetro de estilo de menú personalizado para que la IA formatee el selector de idioma exactamente como deseas.
* **Seguimiento de Tokens:** Muestra estadísticas del uso de tokens de Gemini.

## 🛠 Uso

Crea un archivo de flujo de trabajo (por ejemplo, `.github/workflows/translate.yml`):

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

| Entrada | Requerido | Por defecto | Descripción |
| --- | --- | --- | --- |
| `api_key` | Sí |  | Tu clave API de Google Gemini. |
| `github_token` | Sí |  | Token estándar de GitHub (`${{ secrets.GITHUB_TOKEN }}`). |
| `languages` | Sí |  | Idiomas de destino separados por comas (por ejemplo, `ru, es`). |
| `output_dir` | No | | Directorio para guardar los archivos traducidos. Por defecto es el directorio del archivo de origen. |
| `add_language_menu` | No | `true` | Establécelo en `false` para desactivar la generación automática del menú de idiomas. |
| `menu_style` | No | `> 🌐 **Languages:** [English](README.md) \| [Русский](README.ru.md)` | El estilo de referencia que utiliza la IA al generar un nuevo menú de idiomas. |
| `commit_message` | No | `docs: auto-translate README via Gemini` | Texto utilizado para el mensaje del commit de git. |
| `model` | No | `gemini-3.1-pro-preview` | El modelo de Gemini a utilizar. |
| `source_file` | No | `README.md` | El archivo base a traducir. |

## 🔑 Cómo obtener una clave API de Google Gemini

Para usar esta acción, necesitas una clave API gratuita de Google AI Studio:

1. Ve a [Google AI Studio](https://aistudio.google.com/).
2. Inicia sesión con tu cuenta de Google.
3. En el menú de navegación izquierdo, haz clic en **Get API key**.
4. Haz clic en el botón **Create API key**.
5. Copia la clave generada.
6. Ve a tu repositorio de GitHub -> **Configuración (Settings)** -> **Secretos y variables (Secrets and variables)** -> **Acciones (Actions)**.
7. Haz clic en **New repository secret**, nómbralo `GEMINI_API_KEY`, pega tu clave en el campo de Secret y guarda.

## 🔑 Cómo configurar el Token Estándar de GitHub

Esta acción utiliza el `GITHUB_TOKEN` integrado para hacer commits o crear Pull Requests. **No** necesitas crear un Personal Access Token (PAT) manualmente, pero **debes** asegurarte de que el token predeterminado tenga los permisos correctos:

1. Ve a la **Configuración (Settings)** de tu repositorio -> **Acciones (Actions)** -> **General**.
2. Desplázate hacia abajo hasta la sección **Permisos de flujo de trabajo (Workflow permissions)**.
3. Selecciona **Permisos de lectura y escritura (Read and write permissions)**.
4. Haz clic en **Guardar (Save)**.
5. En tu YAML de flujo de trabajo, simplemente pasa `${{ secrets.GITHUB_TOKEN }}` a la entrada `github_token` (como se muestra en el ejemplo de uso).

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - consulta el archivo [LICENSE](https://github.com/artryazanov/gemini-readme-translator/blob/main/LICENSE) para más detalles.