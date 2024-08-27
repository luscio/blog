---
title: php-cs-fixer代码格式化
date: 2019/03/19 13:35
tags:
  - php
categories:
  - php
---

## composer全局安装php-cs-fixer

```bash
composer global require friendsofphp/php-cs-fixer
```

## 新建.php_cs文件

```php
<?php

$finder = PhpCsFixer\Finder::create()
    ->in(__DIR__)
    ->exclude('public/static')
    ->exclude('public/upload')
    ->exclude('vendor');

$rules = [
    '@PSR1' => true,
    '@PSR2' => true,
    '@PhpCsFixer' => true,
    // 数组定义语法短括号
    'array_syntax' => [
        'syntax' => 'short',
    ],
    // 二进制运算符应按配置包含在空格中
    'binary_operator_spaces' => [
        'default' => 'single_space',
    ],
    // .连接符两边空格
    'concat_space' => [
        'spacing' => 'one',
    ],
    // 删除多余的空行
    'no_extra_blank_lines' => [
        'tokens' => ['break', 'case', 'continue', 'curly_brace_block', 'default', 'extra', 'parenthesis_brace_block', 'return', 'square_brace_block', 'switch', 'throw', 'use', 'useTrait', 'use_trait'],
    ],
    // 必须以空行开头的语句列表
    'blank_line_before_statement' => [
        'statements' => [],
    ],
    // 类的属性方法必须用一个空行分隔
    'class_attributes_separation' => [
        'elements' => ['const', 'method', 'property'],
    ],
    // 在结束分号之前禁止多行空格或将分号移动到新行
    'multiline_whitespace_before_semicolons' => [
        'strategy' => 'no_multi_line',
    ],
    // 分号后修复空格
    'space_after_semicolon' => [
        'remove_in_empty_for_expressions' => true,
    ],
    // 将双引号转换为简单字符串的单引号
    'single_quote' => [
        'strings_containing_single_quote_chars' => true,
    ],
    // 只有一行实际内容的单行注释和多行注释应使用//语法。
    'single_line_comment_style' => [
        'comment_types' => ['hash'],
    ],
];

return PhpCsFixer\Config::create()
    ->setRiskyAllowed(true)
    ->setFinder($finder)
    ->setRules($rules)
    ->setCacheFile(__DIR__ . '/runtime/.php_cs.cache');
```