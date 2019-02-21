---
layout: post
title:  "Vue.js - slot"
date:   2019-02-21 13:00:00 +0900
categories: vue
---

[vuejs.org Slots](https://vuejs.org/v2/guide/components-slots.html)

컴포넌트 사용자 엘리먼트 사이에 데이터를 전달하고자 할때 slot을 사용한다.

- Fallback Content

<submit-button> 컴포넌트 template이 아래와 같다고 할때

~~~ html

<button type="submit">
  <slot>Submit</slot>
</button>

~~~

아래 처럼 엘리먼트 사이에 데이터를 전달하면 slot이 대체 된다.

데이터를 전달하지 않으면 slot 태그안의 내용이 노출 된다.

~~~ html

<submit-button>
  Save
</submit-button>

~~~

결과

~~~ html

<button type="submit">
  Save
</button>

~~~

- Named Slots

아래 <base-layout> 처럼 여러 slot이 필요할 경우 slot 이름을 설정하여 사용 가능 하다.

~~~ html

<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

~~~

v-slot으로 설정

~~~ html

<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>

~~~

- Scoped Slots

slot에 부모 컨포넌트의 데이터를 접근하기 위해서는 선언이 필요하다.

~~~ html

<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>

~~~

- #

v-slot을 #으로 표현 가능

~~~ html

<base-layout>
  <template #header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template #footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>

~~~