---
layout: post
title:  "Vue.js 시작"
date:   2019-02-18 09:00:00 +0900
categories: vue
---

[참고](https://kr.vuejs.org/v2/guide/)

# 호환성 정보
Vue는 ECMAScript 5 기능을 사용하기 때문에 IE8 이하 버전을 지원하지 않습니다. 하지만 모든 ECMAScript 5 호환 브라우저를 지원합니다

# 빠른 시작
[JSFiddle Hello World 예제](https://jsfiddle.net/chrisvfritz/50wL7mdz/)

# 선언적 렌더링
- 템플릿 렌더링
~~~ html
<div id="app">
  {{ message }}
</div>
~~~

~~~ javascript
var app = new Vue({
  el: '#app',
  data: {
    message: '안녕하세요 Vue!'
  }
})
~~~

## 디렉티브

디렉티브는 Vue에서 제공하는 특수 속성임을 나타내는 v- 접두어가 붙어있으며 사용자가 짐작할 수 있듯 렌더링 된 DOM에 특수한 반응형 동작을 합니다.

- v-bind
Element 속성 설정
~~~ html
<div id="app-2">
  <span v-bind:title="message">
    내 위에 잠시 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
  <span :title="message">
    v-bind 생략 가능
  </span>
</div>
~~~

~~~ javascript
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '이 페이지는 ' + new Date() + ' 에 로드 되었습니다'
  }
})
~~~

- v-if
~~~ html
<div id="app-3">
  <p v-if="seen">이제 나를 볼 수 있어요</p>
</div>
~~~

~~~ javascript
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
~~~

- v-for
~~~ html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
~~~

~~~ javascript
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
    ]
  }
})
~~~

- v-on
이벤트 리스너 설정
~~~ html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">메시지 뒤집기</button>
</div>
~~~

~~~ javascript
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: '안녕하세요! Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
~~~

- v-model
양방향 바인딩
~~~ html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
~~~

~~~ javascript
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: '안녕하세요 Vue!'
  }
})
~~~