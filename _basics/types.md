---
title: 자료형
description: An overview of data types in the Liquid template language.
description: Liquid 템플릿 언어에서의 자료형에 대한 개요
---

Liquid 객체는 여섯 개의 자료형 중 하나가 될 수 있습니다:

- [문자열(String)](#string)
- [숫자(Number)](#number)
- [불리언(Boolean)](#boolean)
- [Nil](#nil)
- [배열(Array)](#array)
- [EmptyDrop](#emptydrop)

<!-- You can initialize Liquid variables using [`assign`]({{ "/tags/variable/#assign" | prepend: site.baseurl }}) or [`capture`]({{ "/tags/variable/#capture" | prepend: site.baseurl }}) tags. -->

Liquid 변수는 [`assign`]({{ "/tags/variable/#assign" | prepend: site.baseurl }})이나 [`capture`]({{ "/tags/variable/#capture" | prepend: site.baseurl }}) 태그를 사용하여 초기화할 수 있습니다.

## 문자열(String)

<!-- Strings are sequences of characters wrapped in single or double quotes: -->

문자열은 따옴표 또는 상따옴표로 감싸진 문자들의 시퀀스입니다.

```liquid
{%- raw -%}
{% assign my_string = "Hello World!" %}
{% endraw %}
```

<!-- Liquid does not convert escape sequences into special characters. -->

Liquid는 특수 문자를 이스케이프 시퀀스로 변환하지 않습니다.

## 숫자(Number)

<!-- Numbers include floats and integers: -->

숫자 자료형은 실수와 정수를 포함합니다:

```liquid
{%- raw -%}
{% assign my_int = 25 %}
{% assign my_float = -39.756 %}
{% endraw %}
```

## 불리언(Boolean)

<!-- Booleans are either `true` or `false`. No quotations are necessary when declaring a boolean: -->

불리언은 `true`나 `false`중 하나입니다. 불리언을 선언할 때는 따옴표가 필요하지 않습니다:

```liquid
{%- raw -%}
{% assign foo = true %}
{% assign bar = false %}
{% endraw %}
```

## Nil

<!-- Nil is a special empty value that is returned when Liquid code has no results. It is **not** a string with the characters "nil". -->

Nil은 Liquid 코드가 결과값이 없을 경우에 반환하는 특별한 빈 값입니다. 이는 문자로 구성된 문자열 "nil"이 **아닙니다**.

<!-- Nil is [treated as false]({{ "/basics/truthy-and-falsy/#falsy" | prepend: site.baseurl }}) in the conditions of `if` blocks and other Liquid tags that check the truthfulness of a statement. -->

Nil은 `if` 블록과 참/거짓을 판별하는 다른 Liquid 태그의 조건 구문에서 [거짓(false)으로 취급]({{ "/basics/truthy-and-falsy/#falsy" | prepend: site.baseurl }})됩니다.

<!-- In the following example, if the user does not exist (that is, `user` returns `nil`), Liquid will not print the greeting: -->

아래의 예시에서, 사용자가 없을 경우(즉 `user`가 `nil`을 반환하면), Liquid는 환영 인사를 출력하지 않습니다.

```liquid
{%- raw -%}
{% if user %}
  Hello {{ user.name }}!
{% endif %}
{% endraw %}
```

Tags or outputs that return `nil` will not print anything to the page.

`nil`을 반환하는 태그 또는 출력은 페이지에 어떤 것도 출력하지 않습니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
The current user is {{ user.name }}
{% endraw %}
```

<p class="code-label">출력</p>
```text
The current user is
```

## 배열(Array)

<!-- Arrays hold lists of variables of any type. -->

배열은 모든 자료형에 대한 변수를 담을 수 있습니다.

### 배열의 아이템 가져오기

<!-- To access all the items in an array, you can loop through each item in the array using an [iteration tag]({{ "/tags/iteration/" | prepend: site.baseurl }}). -->

배열 내의 모든 아이템에 접근하기 위해서, [반복 태그(iteration tag)]({{ "/tags/iteration/" | prepend: site.baseurl }})를 사용해 배열의 각 아이템을 순회할 수 있습니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
<!-- if site.users = "Tobi", "Laura", "Tetsuro", "Adam" -->
{% for user in site.users %}
  {{ user }}
{% endfor %}
{% endraw %}
```

<p class="code-label">출력</p>
```text
  Tobi Laura Tetsuro Adam
```

### 배열의 특정 아이템 가져오기

<!-- You can use square bracket `[` `]` notation to access a specific item in an array. Array indexing starts at zero. A negative index will count from the end of the array. -->

배열의 특정 아이템에 접근하기 위해서 대괄호 `[`, `]` 표기를 사용할 수 있습니다. 배열의 인덱스는 0에서부터 시작합니다. 음수 인덱스는 배열의 끝에서부터 계산됩니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
<!-- if site.users = "Tobi", "Laura", "Tetsuro", "Adam" -->
{{ site.users[0] }}
{{ site.users[1] }}
{{ site.users[-1] }}
{% endraw %}
```

<p class="code-label">출력</p>
```text
Tobi
Laura
Adam
```

### 배열 초기화

<!-- You cannot initialize arrays using only Liquid. -->

Liquid 만을 사용해서 배열을 초기화하는 방법은 없습니다.

<!-- You can, however, use the [`split`]({{ "/filters/split/" | prepend: site.baseurl }}) filter to break a string into an array of substrings. -->

다만, [`split`]({{ "/filters/split/" | prepend: site.baseurl }}) 필터를 이용해 부분 문자열의 배열에 문자열을 분리하는 방법으로 사용할 수 있습니다.

## EmptyDrop

<!-- An EmptyDrop object is returned if you try to access a deleted object. In the example below, `page_1`, `page_2` and `page_3` are all EmptyDrop objects: -->

EmptyDrop은 삭제한 객체에 접근하려 할 때 반환되는 객체입니다. 아래의 예시에서 `page_1`과 `page_2`, `page_3`은 모드 EmptyDrop 객체입니다.

```liquid
{%- raw -%}
{% assign variable = "hello" %}
{% assign page_1 = pages[variable] %}
{% assign page_2 = pages["does-not-exist"] %}
{% assign page_3 = pages.this-handle-does-not-exist %}
{% endraw %}
```

### 비어있는지 확인하기

<!-- You can check to see if an object exists or not before you access any of its attributes. -->

여러분은 해당 속성(attributes)에 접근하기 전에 객체가 존재하는지 여부를 확인할 수 있습니다.

```liquid
{%- raw -%}
{% unless pages == empty %}
  <h1>{{ pages.frontpage.title }}</h1>
  <div>{{ pages.frontpage.content }}</div>
{% endunless %}
{% endraw %}
```

<!-- Both empty strings and empty arrays will return `true` if checked for equivalence with `empty`. -->

`empty`와 일치하는지 확인해보면, 빈 문자열과 빈 배열 둘다 `true`를 반환할 것입니다.
