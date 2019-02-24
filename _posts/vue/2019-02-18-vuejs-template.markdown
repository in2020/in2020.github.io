---
layout: post
title:  "Vue.js - 템플릿"
date:   2019-02-18 12:00:00 +0900
tags: [vue]
categories: vue
---

[참고 페이지 kr.vuejs.org 템플릿 문법](https://kr.vuejs.org/v2/guide/syntax.html)

# 원시 HTML

- 실제 HTML을 출력하려면 v-html 디렉티브를 사용해야 합니다.

~~~ html

<p>Using v-html directive: <span v-html="rawHtml"></span></p>

~~~

# computed 속성

raw 데이터 가공 표현

메소드와 같은 효과를 볼수 있지만 캐싱기능이 있어 동일 데이터를 추출 해야 할 경우 computed 효율 적이다.

~~~ html

<div id="example">
  <p>원본 메시지: "{{ message }}"</p>
  <p>역순으로 표시한 메시지: "{{ reversedMessage }}"</p>
</div>

~~~

~~~ javascript

var vm = new Vue({
  el: '#example',
  data: {
    message: '안녕하세요'
  },
  computed: {
    // 계산된 getter
    reversedMessage: function () {
      // `this` 는 vm 인스턴스를 가리킵니다.
      return this.message.split('').reverse().join('')
    }
  }
})

~~~

