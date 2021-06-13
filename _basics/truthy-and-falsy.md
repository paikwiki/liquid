---
title: 참-같은-값(truthy)과 거짓-같은-값(falsy)
description: Liquid 템플릿 언어에서 불리언 로직에 대한 개요
---

<!-- When a non-boolean [data type]({{ "/basics/types/" | prepend: site.baseurl }}) is used in a boolean context (such as a conditional tag), Liquid decides whether to evaluate it as `true` or `false`. Data types that return `true` by default are called **truthy**. Data types that return false by default are called **falsy**. -->

불리언 유형이 아닌 [자료형]({{ "/basics/types/" | prepend: site.baseurl }})을 불리언 문맥에서 사용할 때, Liquid는 `true`인지 `false`인지 판별합니다. 기본적으로 `true`를 반환하는 자료형을 **참-값은-값**이라고 부르고, `false`를 반환하는 자료형을 **거짓-값은-값**이라고 부릅니다.

## 참-같은-값(Truthy)

<!-- All values in Liquid are truthy except `nil` and `false`. -->

Liquid에서 `nil`과 `false`를 제외한 모든 값은 참-같은-값입니다.

<!-- In the example below, the text "Tobi" is not a boolean, but it is truthy in a conditional: -->

아래의 예시에서, "Tobi"라는 텍스트는 불리언 타입이 아니지만, 조건식에서는 참-같은-값입니다.

```liquid
{%- raw -%}
{% assign name = "Tobi" %}

{% if name %}
  "name"이 정의되어 있다면 이 텍스트를 항상 출력합니다.
{% endif %}
{% endraw %}
```

<!-- [Strings]({{ "/basics/types/#string" | prepend: site.baseurl }}), even when empty, are truthy. The example below will create empty HTML tags if `page.category` exists but is empty: -->

비어 있는 [문자열(Strings)]({{ "/basics/types/#string" | prepend: site.baseurl }})이라 해도, 참-같은-값입니다. 아래의 예시에서 `page.category`가 빈 채로 존재한다면, 비어있는 HTML 태그가 생성될 것입니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
{% if page.category %}
  <h1>{{ page.category }}</h1>
{% endif %}
{% endraw %}
```

<p class="code-label">출력</p>
```html
  <h1></h1>
```

## 거짓-같은-값(Falsy)

<!-- The only values that are falsy in Liquid are [`nil`]({{ "/basics/types/#nil" | prepend: site.baseurl }}) and [`false`]({{ "/basics/types/#boolean" | prepend: site.baseurl }}). -->

Liquid에서는 오직 [`nil`]({{ "/basics/types/#nil" | prepend: site.baseurl }})과 [`false`]({{ "/basics/types/#boolean" | prepend: site.baseurl }})만이 거짓-같은-값입니다.

## 요약

The table below summarizes what is truthy or falsy in Liquid.
Liquid에서 참-같은-값과 거짓-같은-값이 무엇인지 아래의 표에 요약했습니다.

|                       | 참-같은-값(truthy) | 거짓-같은-값(falsy) |
| --------------------- | :----: | :---: |
| 참(true)              |   •    |       |
| 거짓(false)            |        |   •   |
| nil                   |        |   •   |
| 문자열(string)         |   •    |       |
| 빈 문자열(empty string) |   •    |       |
| 0                     |   •    |       |
| 정수(integer)          |   •    |       |
| 실수(float)            |   •    |       |
| 배열(array)            |   •    |       |
| 빈 배열(empty array)    |   •    |       |
| 페이지(page)            |   •    |       |
| EmptyDrop             |   •    |       |
