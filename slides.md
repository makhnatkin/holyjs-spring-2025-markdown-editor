---
theme: ../../gravity-ui/slidev-theme
# title of your slide, will inferred from the first header if not specified
title: "MarkdownEditor: следующий шаг в работе с текстом"
# titleTemplate for the webpage, `%s` will be replaced by the slides deck's title
titleTemplate: '%s - MarkdownEditor'
# information for your slides, can be a Markdown string
info: false
# author field for exported PDF or PPTX
author: Sergey Makhnatkin
# keywords field for exported PDF, comma-delimited
keywords: markdown-editor,holyjs

# enable presenter mode, can be boolean, 'dev' or 'build'
presenter: true
# enable browser exporter, can be boolean, 'dev' or 'build'
browserExporter: dev
# enabled pdf downloading in SPA build, can also be a custom url
download: false
# filename of the export file
exportFilename: slidev-exported
# export options
# use export CLI options in camelCase format
# Learn more: https://sli.dev/guide/exporting.html
export:
format: pdf
timeout: 30000
dark: false
withClicks: false
withToc: false
# enable twoslash, can be boolean, 'dev' or 'build'
twoslash: true
# show line numbers in code blocks
lineNumbers: false
# enable monaco editor, can be boolean, 'dev' or 'build'
monaco: true
# Where to load monaco types from, can be 'cdn', 'local' or 'none'
monacoTypesSource: local
# explicitly specify extra local packages to import the types for
monacoTypesAdditionalPackages: []
# explicitly specify extra local modules as dependencies of monaco runnable
monacoRunAdditionalDeps: []
# download remote assets in local using vite-plugin-remote-assets, can be boolean, 'dev' or 'build'
remoteAssets: false
# controls whether texts in slides are selectable
selectable: true
# enable slide recording, can be boolean, 'dev' or 'build'
record: dev
# enable Slidev's context menu, can be boolean, 'dev' or 'build'
contextMenu: true
# enable wake lock, can be boolean, 'dev' or 'build'
wakeLock: true
# take snapshot for each slide in the overview
overviewSnapshots: false

# force color schema for the slides, can be 'auto', 'light', or 'dark'
colorSchema: auto
# router mode for vue-router, can be "history" or "hash"
routerMode: history
# aspect ratio for the slides
aspectRatio: 16/9
# real width of the canvas, unit in px
canvasWidth: 980
# used for theme customization, will inject root styles as `--slidev-theme-x` for attribute `x`
themeConfig:
primary: '#5d8392'

# favicon, can be a local file path or URL
favicon: 'https://cdn.jsdelivr.net/gh/slidevjs/slidev/assets/favicon.png'
# URL of PlantUML server used to render diagrams
# fonts will be auto-imported from Google fonts
# Learn more: https://sli.dev/custom/config-fonts.html
fonts:
sans: Roboto
serif: Roboto Slab
mono: Fira Code

# HTML tag attributes
htmlAttrs:
dir: ltr
lang: ru
---

# MarkdownEditor: следующий шаг в работе с текстом

::footer::
### Сергей Махнаткин

разработчик интерфейсов
::tags::
Yandex / Gravity UI

<!--
3. добавить футер
4. починить зачеркивание
-->

---
src: ./slides/part1.md
---

---
src: ./slides/part2.md
---

---
src: ./slides/part3.md
---

---
src: ./slides/part4.md
---

---
src: ./slides/part5.md
---
