---
layout: post
title:  "Vue.js - 컴포넌트"
date:   2019-02-18 10:00:00 +0900
categories: vue
---

[참고 페이지 kr.vuejs.org](https://kr.vuejs.org/v2/guide/index.html#%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%9C-%EC%9E%91%EC%84%B1%EB%B0%A9%EB%B2%95)

[참고 페이지 kr.vuejs.org 컴포넌트](https://kr.vuejs.org/v2/guide/components.html)

정의된 컴포넌트는 사용자 정의 엘리먼트 형식으로 사용

# 전역 등록

~~~ javascript

Vue.component('todo-item', {
  template: '<li>할일 항목 하나입니다.</li>'
})
~~~

~~~ html

<ol>  
  <todo-item></todo-item>
</ol>

~~~

# 지역 등록

components 옵션 설정

~~~ javascript

new Vue({
    el: '#app',
    components: {
        'todo-item': {            
            template: '<li>할일 항목 하나입니다.</li>'
        }
    }
});

~~~

# 컴포넌트 데이터 

props에 template에서 사용할 변수명 정의(todo) 

props를 통해 데이터의 출처를 명확히 하면 다른 상황에서 컴포넌트를 재사용할 수 있습니다.

각 구성 요소에는 "키"를 제공해야함.

- 전역 등록

~~~ javascript

Vue.component('todo-item', {  
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
});

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})

~~~

- 지역 등록

~~~ javascript

new Vue({
    el: '#app',
    data: {
        groceryList: [
            { id: 1, text: 'item 1'},
            { id: 2, text: 'item 2'},
            { id: 3, text: 'item 3'},
        ]
    },
    components: {
        'todo-item': {
            props: ['todo'],
            template: '<li>{{ todo.text }}</li>'
        }
    }
});

~~~

~~~ html

<div id="app-7">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>

~~~

# 일부 엘리먼트 제한

- DOM을 템플릿으로 사용할 때 <ul>, <ol>, <table>, <select> 사용 제한 됨.
  문자열 템플릿을 사용하거나 'is' 특수 속성을 사용하여 제한 사항 해결 가능
  - 문자열 템플릿(가능한 경우 항상 문자열 템플릿을 사용하는 것이 좋습니다.)
    - <script type="text/x-template">
    - JavaScript 인라인 템플릿 문자열
    - .vue 컴포넌트
  - 'is' 특수 속성

~~~ html

<table>
  <tr is="my-row"></tr>
</table>

~~~

# 컴포넌트내 data는 함수여야합니다.

~~~ javascript

new Vue({
    el: '#app',
    components: {
        'my-component':{
            template: '<span>{{ message }}</span>',
            data: function() {
                return {
                    message: 'hello'
                };
            }
        }
    }
});

~~~

# 컴포넌트 props camelCase는 html 속서명 kebab-case로 매칭 된다.

~~~ javascript

Vue.component('child', {
  // JavaScript는 camelCase
  props: ['myMessage'],
  template: '<span>{{ myMessage }}</span>'
})

~~~

~~~ html

<!-- HTML는 kebab-case -->
<child my-message="안녕하세요!"></child>

~~~

# 부모-자식 컴포넌트 관계

Vue.js에서 부모-자식 컴포넌트 관계는 props는 아래로, events 위로 라고 요약 할 수 있습니다. 

부모는 props를 통해 자식에게 데이터를 전달하고 자식은 events를 통해 부모에게 메시지를 보냅니다

![부모-자식 컴포넌트 관계](https://kr.vuejs.org/images/props-events.png)

# v-on을 이용한 사용자 지정 이벤트($emit)

자식 컨포넌트가 부모에게 이벤트를 전송하는 방법

태그에 선언된 increment를 기준으로 부모 method를 바인딩하고 자식에서는 $emit('increment')를 통해 호출.

~~~ html

<div id="counter-event-example">
  <p>{{ total }}</p>
  <button-counter v-on:increment="incrementTotal"></button-counter>
  <button-counter v-on:increment="incrementTotal"></button-counter>
</div>

~~~

~~~ javascript

Vue.component('button-counter', {
  template: '<button v-on:click="incrementCounter">{{ counter }}</button>',
  data: function () {
    return {
      counter: 0
    }
  },
  methods: {
    incrementCounter: function () {
      this.counter += 1
      this.$emit('increment')
    }
  },
})

new Vue({
  el: '#counter-event-example',
  data: {
    total: 0
  },
  methods: {
    incrementTotal: function () {
      this.total += 1
    }
  }
})

~~~