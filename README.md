# MarkdownLint <!-- omit in toc -->

- [Overview](#overview)
- [Usage](#usage)
  - [Install](#install)
  - [Checking errors](#checking-errors)
- [Configuration](#configuration)
- [Rules](#rules)
  - [Disabling rules](#disabling-rules)
- [Others](#others)
  - [Plugins](#plugins)
  - [Online demo](#online-demo)
  - [VSCode extension](#vscode-extension)

## Overview

[MarkdownLint](https://github.com/DavidAnson/markdownlint) is a Node.js style checker and linting tool for markdown.

## Usage

### Install

```shell
npm install markdownlint --save-dev
```

@see [VSCode extension](#vscode-extension) to automate workflow.

### Checking errors

There is no easy way to simply.

Using Docker:

```shell
docker run --rm \
    -v "$(pwd)/README.md:/README.md:ro" \
    avtodev/markdown-lint:v1 \
    /README.md
```

## Configuration

May be one of the following files:

- JSON: `.markdownlint.jsonc`, `.markdownlint.json`
- YML: `.markdownlint.yaml`, `.markdownlint.yml`
- JavaScript: `.markdownlint.cjs`, `.markdownlint.mjs`

```yml
# .markdownlint.yml
ul-style:
  style: 'dash'
ul-indent:
  indent: 4
line-length:
  line_length: 120
no-trailing-punctuation:
  punctuation: ".,;:!。，；:"    # List of not allowed
ol-prefix:
  style: "one_or_ordered"       # Ordered list item prefix
no-inline-html: false           # Allow inline HTML
no-emphasis-as-heading: false   # Emphasis used instead of a heading
```

## Rules

 [List of rules](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md)

### Disabling rules

- Disable all rules: `<!-- markdownlint-disable -->`
- Enable all rules: `<!-- markdownlint-enable -->`
- Disable all rules for the current line: `<!-- markdownlint-disable-line -->`
- Disable all rules for the next line: `<!-- markdownlint-disable-next-line -->`
- Disable one or more rules by name: `<!-- markdownlint-disable MD001 MD005 -->`
- Enable one or more rules by name: `<!-- markdownlint-enable MD001 MD005 -->`
- Disable one or more rules by name for the current line: `<!-- markdownlint-disable-line MD001 MD005 -->`
- Disable one or more rules by name for the next line: `<!-- markdownlint-disable-next-line MD001 MD005 -->`
- Capture the current rule configuration: `<!-- markdownlint-capture -->`
- Restore the captured rule configuration: `<!-- markdownlint-restore -->`

## Others

### Plugins

[Additional plugins](https://www.npmjs.com/search?q=keywords:markdown-it-plugin)

### Online demo

[markdownlint demo](https://dlaa.me/markdownlint/)

### VSCode extension

Homepage: [DavidAnson.vscode-markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

```json
  "[markdown]": {
      "editor.formatOnSave": true,
      "editor.formatOnPaste": true
  },
  "editor.codeActionsOnSave": {
    "source.fixAll.markdownlint": true
  }
  "markdownlint.run": "onType"
```
