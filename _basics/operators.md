---
title: 연산자
description: Liquid 템플릿 언어에서 계산을 위해 연산자 사용하기
---

<!-- Liquid includes many logical and comparison operators. You can use operators to create logic with [control flow]({{ "/tags/control-flow/" | prepend: site.baseurl }}) tags. -->

Liquid에는 다양한 논리/비교 연산자가 있습니다. [흐름 제어]({{ "/tags/control-flow/" | prepend: site.baseurl }}) 태그와 함께 로직을 위한 연산자를 사용할 수 있습니다.

## 기본 연산자

<table>
  <tbody>
    <tr>
      <td><code>==</code></td>
      <td>같음</td>
    </tr>
    <tr>
      <td><code>!=</code></td>
      <td>같지 않음</td>
    </tr>
    <tr>
      <td><code>&gt;</code></td>
      <td>큰</td>
    </tr>
    <tr>
      <td><code>&lt;</code></td>
      <td>작은</td>
    </tr>
    <tr>
      <td><code>&gt;=</code></td>
      <td>같거나 큰</td>
    </tr>
    <tr>
      <td><code>&lt;=</code></td>
      <td>같거나 작은</td>
    </tr>
    <tr>
      <td><code>or</code></td>
      <td>또는</td>
    </tr>
    <tr>
      <td><code>and</code></td>
      <td>그리고</td>
    </tr>
  </tbody>
</table>

<!-- For example: -->

예를 들어:

```liquid
{%- raw -%}
{% if product.title == "Awesome Shoes" %}
  These shoes are awesome!
{% endif %}
{% endraw %}
```

<!-- You can do multiple comparisons in a tag using the `and` and `or` operators: -->

`and`와 `or` 연산자를 사용해 태그 내에서 여러 개의 비교 구문을 사용할 수 있습니다:

```liquid
{%- raw -%}
{% if product.type == "Shirt" or product.type == "Shoes" %}
  This is a shirt or a pair of shoes.
{% endif %}
{% endraw %}
```

## contains

<!-- `contains` checks for the presence of a substring inside a string. -->

`contains`는 문자열 내에 부분 문자열이 있는지 확인합니다.

```liquid
{%- raw -%}
{% if product.title contains "Pack" %}
  This product's title contains the word Pack.
{% endif %}
{% endraw %}
```

<!-- `contains` can also check for the presence of a string in an array of strings. -->

`contains`는 문자열로 구성된 배열에 문자열이 존재하는지 확인할 수도 있습니다.

```liquid
{%- raw -%}
{% if product.tags contains "Hello" %}
  This product has been tagged with "Hello".
{% endif %}
{% endraw %}
```

<!-- `contains` can only search strings. You cannot use it to check for an object in an array of objects. -->

`contains`는 오직 문자열만을 확인합니다. 오브젝트로 구성된 배열 안의 오브젝트를 확인하기 위해서는 사용할 수 없습니다.

## 연산자의 순서

<!-- In tags with more than one `and` or `or` operator, operators are checked in order *from right to left*. You cannot change the order of operations using parentheses — parentheses are invalid characters in Liquid and will prevent your tags from working. -->

`and` 또는 `or` 연산자가 하나 이상 있는 태그 내에서, 연산자는 *오른쪽에서 왼쪽* 순서로 적용됩니다. 괄호를 사용하여 이 순서를 바꿀 수 없습니다 - Liquid에서 괄호는 유효하지 않은 문자이므로 태그가 작동하지 않을 것입니다.

```liquid
{%- raw -%}
{% if true or false and false %}
  이것은 `and` 조건이 먼저 적용되므로 참으로 판별됩니다.
{% endif %}
{% endraw %}
```

```liquid
{%- raw -%}
{% if true and false and false or true %}
  태그는 아래처럼 적용되므로 거짓으로 판별됩니다:

  true and (false and (false or true))
  true and (false and true)
  true and false
  false
{% endif %}
{% endraw %}
```
