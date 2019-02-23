---
layout: post
title:  "Vue.js - 리스트 렌더링"
date:   2019-02-19 9:00:00 +0900
categories: vue
---

[참고 페이지 kr.vuejs.org 리스트 렌더링](https://kr.vuejs.org/v2/guide/list.html)

# 객체 

객체를 v-for를 이용해 출력 가능하며 key와 index도 사용 가능 하다

~~~ javascript

new Vue({
  el: '#v-for-object',
  data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
})

~~~

~~~ html

<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }} : {{ value }}
</div>

~~~

# v-bind:key

Vue가 각 노드의 ID를 추적하고 기존 엘리먼트를 재사용하고 재정렬할 수 있도록 힌트를 제공하려면 각 항목에 고유한 key 속성을 제공해야 합니다

"in-place-patch" 전략을 사용하기 때문에 목록의 출력 결과가 하위 컴포넌트 상태 또는 임시 DOM 상태(예: 폼 input)에 의존하지 않는 경우에 적합합니다.

key는 Vue가 노드를 식별하는 일반적인 메커니즘이기 때문에 v-for와 특별히 연관되지 않는 다른 용도로도 사용됩니다.

~~~ html

<div v-for="item in items" :key="item.id">
  <!-- content -->
</div>

~~~

# 배열 변경 감지

아래 배열 메소드는 뷰를 갱신 합니다.

- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

아래 배열 메소드는 원본 배열 변형없이 새 배열을 반환 합니다.

- filter()
- concat()
- slice()

감지 불가 변경 사항

- 인덱스로 배열에 있는 항목을 직접 설정한느 경우
- 배열 길이를 수정하는 경우 

~~~ javascript

vm.items[indexOfItem] = newValue;
vm.items.length = newLength

~~~

Vue.set, splice를 사용하여 위 사항 회피

~~~ javascript

Vue.set(example1.items, indexOfItem, newValue)
example1.items.splice(indexOfItem, 1, newValue)

example1.items.splice(newLength)

~~~

# 필터링 / 정렬 된 결과 표시하기

때로 원본 데이터를 실제로 변경하거나 재설정하지 않고 배열의 필터링 된 버전이나 정렬된 버전을 표시해야 할 필요가 있습니다. 

이 경우 필터링 된 배열이나 정렬된 배열을 반환하는 계산된 속성을 만들 수 있습니다.

~~~ html

<li v-for="n in evenNumbers">{{ n }}</li>

~~~

~~~ javascript

data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers: function () {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}

~~~

~~~ html

<li v-for="n in even(numbers)">{{ n }}</li>

~~~

~~~ javascript

data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
methods: {
  even: function (numbers) {
    return numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}

~~~

# 이외 v-for 기능

- 숫자를 사용하여 반복문 가능

~~~ html

<div>
  <span v-for="n in 10">{{ n }} </span>
</div>

~~~

- template 태그를 사용하여 블럭 렌더링 가능

~~~ html

<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>

~~~

- v-if와 함께 일부 항목 렌더링 가능

~~~ html

<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>

~~~

- v-for 실행을 조건부로 하는 목적일 경우 

~~~ html

<ul v-if="todos.length">
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ul>
<p v-else>No todos left!</p>

~~~