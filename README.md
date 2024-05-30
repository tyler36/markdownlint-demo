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

Here, we use the command-line package: <https://github.com/DavidAnson/markdownlint-cli2>

```shell
npm install markdownlint-cli2 --save-dev
```

- To check for errors (using `#` to _negate_ the glob):

```shell
markdownlint-cli2 '**/*.md' '#{node_modules,vendor}'
```

- To automatically fix errors:

```shell
markdownlint-cli2 '**/*.md' '#{node_modules,vendor} --fix'
```

Add helper scripts to `package.json`:

```json
  "scripts": {
    "lint:md": "markdownlint-cli2",
    "lint:md:fix": "markdownlint-cli2 --fix"
  },
```

### Checking errors

There is no easy way to simply.

To use a [markdownlint-cli2](https://hub.docker.com/r/davidanson/markdownlint-cli2) docker image:

```shell
docker run -v $PWD:/workdir davidanson/markdownlint-cli2:latest "**/*.md" "#node_modules"
```

## Configuration

`markdownlint-cli2` can use standard markdownlint configuration files.
However, `cli2` versions allow for complete control of markdownlint-cli2 and the vscode extension.
@see <https://github.com/DavidAnson/markdownlint-cli2#configuration>

The order of preference is:

- cli2: `.markdownlint-cli2.jsonc`, `.markdownlint-cli2.yaml`, `.markdownlint-cli2.cjs`
- JSON: `.markdownlint.jsonc`, `.markdownlint.json`
- YML: `.markdownlint.yaml`, `.markdownlint.yml`
- JavaScript: `.markdownlint-cli2.mjs`, `.markdownlint.cjs`, `.markdownlint.mjs`

```yaml
# .markdownlint-cli2.yml
config:
  ul-style:
    style: 'dash'
  ul-indent:
    indent: 2
  line-length:
    line_length: 120 # Line length 80 is far to short
  no-trailing-punctuation:
    punctuation: '.,;:!。，；:' # List of not allowed
  ol-prefix:
    style: 'one_or_ordered' # Ordered list item prefix
  no-inline-html: false # Allow inline HTML
  no-emphasis-as-heading: false # Emphasis used instead of a heading

# Define glob expressions to use (only valid at root)
globs:
  - "**/*.md"

# Ignore files referenced by .gitignore (only valid at root)
gitignore: true
```

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
https://www.npmjs.com/search?q=keywords:markdown-it-plugin
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
