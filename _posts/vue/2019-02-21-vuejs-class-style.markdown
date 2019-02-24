---
layout: post
title:  "Vue.js - 클래스와 스타일 바인딩"
date:   2019-02-21 11:00:00 +0900
tags: [vue]
categories: vue
---

[kr.vuejs.org 클래스와 스타일 바인딩](https://kr.vuejs.org/v2/guide/class-and-style.html)

# class와 style에 대한 v-bind 향상된 기능
## class
### 객체 구문

- 인라인 설정

active 클래스의 존재 여부가 데이터 속성 isActive 의 참 속성에 의해 결정되는 것을 의미합니다.

~~~ html

<div v-bind:class="{ active: isActive }"></div>

~~~

- data 객체로 설정

~~~ html

<div v-bind:class="classObject"></div>

~~~

~~~ javascript

data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}

~~~

- computed 설정

~~~ html

<div v-bind:class="classObject"></div>

~~~

~~~ javascript

data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}

~~~

### 배열 구문

~~~ html

<div v-bind:class="[activeClass, errorClass]"></div>

~~~

~~~ javascript

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

~~~

결과

~~~ html

<div class="active text-danger"></div>

~~~

- 배열 구문 내에서 객체 구문 사용 가능

~~~ html

<div v-bind:class="[{ active: isActive }, errorClass]"></div>

~~~

### 컴포넌트와 함께 사용하는 방법

사용자 정의 컴포넌트로 class 속성을 사용하면, 클래스가 컴포넌트의 루트 엘리먼트에 추가 됩니다.

~~~ javascript

Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})

~~~

isActive = true;

~~~ html

<my-component v-bind:class="{ active: isActive }"></my-component>

~~~

~~~ html

<p class="foo bar active">Hi</p>

~~~

## style

- 객체 구문

~~~ html

<div v-bind:style="styleObject"></div>

~~~

~~~ javascript
 
  data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
 
~~~


- 배열 구문

여러 개의 스타일 객체를 사용할 수 있게 합니다.

~~~ html

<div v-bind:style="[baseStyles, overridingStyles]"></div>

~~~

- 다중, 자동 스타일 설정

브라우저 벤더 접두어가 필요한 CSS 속성을 사용하면 Vue는 자동으로 해당 접두어를 감지하여 스타일을 적용합니다

~~~ html 
 
  <div v-bind:style="transform"></div>
 
~~~

브라우저가 지원하는 배열의 마지막 값만 렌더링합니다. 

~~~ html 
 
  <div v-bind:style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
 
~~~