---
name: json-lint
description: "使用 jsonlint 工具检查和格式化 JSON 文件。适用于 JSON 语法校验、格式化、排序 key、schema 验证等场景。"
---

# json-lint

## 概述

本技能使用 [jsonlint](https://github.com/zaach/jsonlint) 对 JSON 文件进行语法检查、格式化、key 排序及 JSON Schema 验证。当需要校验或整理 JSON 时，应使用此技能。

## 何时使用

- 用户或工具报告 JSON 文件有语法错误，需要定位并修复
- 需要将 JSON 格式化（缩进、换行）以便阅读或版本对比
- 需要按 key 字母顺序重排对象属性
- 需要按 JSON Schema 校验 JSON 是否符合约定结构

## 前置条件

安装 jsonlint（全局）：

```bash
npm install jsonlint -g
```

## 工作流程

1. **仅检查语法**：对指定文件运行 `jsonlint <file>`，无错误则无输出；有错误会打印行号与原因。
2. **格式化并原地覆盖**：`jsonlint -i <file>`，可选 `-t "  "` 指定缩进字符。
3. **按 key 排序**：`jsonlint -s -i <file>`，排序后写回原文件。
4. **使用 JSON Schema 验证**：`jsonlint -V <schema.json> <file>`，可选 `-e` 指定 schema 版本（默认 json-schema-draft-03）。
5. **紧凑错误显示**：`jsonlint -c <file>`，错误信息更简洁。
6. **无效时也强制美化输出**：`jsonlint -p <file>`，便于查看无效 JSON 的结构。

更多用法可用 `jsonlint -h` 查看。

## 命令参考

```
$ jsonlint -h

Usage: jsonlint [file] [options]

file     file to parse; otherwise uses stdin

Options:
   -v, --version            print version and exit
   -s, --sort-keys          sort object keys
   -i, --in-place           overwrite the file
   -t CHAR, --indent CHAR   character(s) to use for indentation  [  ]
   -c, --compact            compact error display
   -V, --validate           a JSON schema to use for validation
   -e, --environment        which specification of JSON Schema the validation file uses  [json-schema-draft-03]
   -q, --quiet              do not print the parsed json to STDOUT  [false]
   -p, --pretty-print       force pretty printing even if invalid
```
