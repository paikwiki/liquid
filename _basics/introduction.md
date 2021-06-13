---
title: 소개
description: An overview of objects, tags, and filters in the Liquid template language.
description: Liquid 템플릿의 객체와 태그, 필터에 대한 개요
redirect_from: /basics/
---

<!-- Liquid uses a combination of [**objects**](#objects), [**tags**](#tags), and [**filters**](#filters) inside **template files** to display dynamic content. -->

Liquid는 동적 컨텐츠를 보여주기 위해 **템플릿 파일**에 [**객체(objects)**](#objects)와 [**태그**](#tags), [**필터**](#filters)를 조합하여 사용합니다.

## 객체(Objects)

<!-- **Objects** contain the content that Liquid displays on a page. Objects and variables are displayed when enclosed in double curly braces: `{% raw %}{{{% endraw %}` and `{% raw %}}}{% endraw %}`. -->

**객체**는 Liquid가 페이지에 출력하는 컨텐츠를 담고 있습니다. 객체와 변수(variables)는 `{% raw %}{{{% endraw %}`와 `{% raw %}}}{% endraw %}`처럼 이중 중괄호로 감싸서 출력할 수 있습니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
{{ page.title }}
{% endraw %}
```

<p class="code-label">출력</p>
```text
{{ page.title }}
```

<!-- In this case, Liquid is rendering the content of the `title` property of the `page` object, which contains the text `{{ page.title }}`. -->

이렇게 하면 Liquid는 `{{ page.title }}`라는 텍스트를 담고있는, `page` 객체의 `title` 속성의 컨텐츠를 가공해 보여줍니다.

## 태그(Tags)

<!-- **Tags** create the logic and control flow for templates. The curly brace percentage delimiters `{% raw %}{%{% endraw %}` and `{% raw %}%}{% endraw %}` and the text that they surround do not produce any visible output when the template is rendered. This lets you assign variables and create conditions or loops without showing any of the Liquid logic on the page. -->

**태그**는 템플릿을 위한 로직과 제어 흐름을 만듭니다. 중괄호-퍼센트 기호인 `{% raw %}{%{% endraw %}`와 `{% raw %}%}{% endraw %}`와 그 내부의 텍스트는 템플릿을 렌더링할 때 어떤 가시적인 출력물을 생성하지 않습니다. 이것은 여러분이 출력 페이지에서 그 어떤 Liquid의 로직도 드러내지 않은 상태로 변수를 대입하고 조건문과 반복문을 사용할 수 있게 해줍니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
{% if user %}
  Hello {{ user.name }}!
{% endif %}
{% endraw %}
```

<p class="code-label">출력</p>
```text
  Hello Adam!
```

<!-- Tags can be categorized into various types: -->

태그는 다양한 유형으로 구분할 수 있습니다.

<!-- - [Control flow]({{ "/tags/control-flow/" | prepend: site.baseurl }})
- [Iteration]({{ "/tags/iteration/" | prepend: site.baseurl }})
- [Template]({{ "/tags/template/" | prepend: site.baseurl }})
- [Variable assignment]({{ "/tags/variable/" | prepend: site.baseurl }}) -->

- [흐름 제어]({{ "/tags/control-flow/" | prepend: site.baseurl }})
- [반복]({{ "/tags/iteration/" | prepend: site.baseurl }})
- [템플릿]({{ "/tags/template/" | prepend: site.baseurl }})
- [변수 대입]({{ "/tags/variable/" | prepend: site.baseurl }})

<!-- You can read more about each type of tag in their respective sections. -->

각 태그의 유형에 대해서는 각각의 섹션에서 더 살펴볼 수 있습니다.

## 필터(Filters)

**Filters** change the output of a Liquid object or variable. They are used within double curly braces `{% raw %}{{ }}{% endraw %}` and [variable assignment]({{ "/tags/variable/" | prepend: site.baseurl }}), and are separated by a pipe character `|`.

**필터**는 Liquid 객체와 변수의 출력을 바꿔 줍니다. 이중 중괄호 `{% raw %}{{ }}{% endraw %}` 내부에서 사용하며, [변수를 대입]({{ "/tags/variable/" | prepend: site.baseurl }})합니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
{{ "/my/fancy/url" | append: ".html" }}
{% endraw %}
```

<p class="code-label">출력</p>
```text
{{ "/my/fancy/url" | append: ".html" }}
```

<!-- Multiple filters can be used on one output, and are applied from left to right. -->

하나의 출력을 위해 여러 개의 필터를 사용할 수 있으며, 이는 왼쪽에서 오른쪽으로 적용됩니다.

<p class="code-label">입력</p>
```liquid
{%- raw -%}
{{ "adam!" | capitalize | prepend: "Hello " }}
{% endraw %}
```

<p class="code-label">출력</p>
```text
{{ "adam!" | capitalize | prepend: "Hello " }}
```
