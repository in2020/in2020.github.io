---
layout: post
title:  "Vue.js - 할일 목록 연습"
date:   2019-02-19 11:00:00 +0900
categories: vue
---

[참고 페이지 kr.vuejs.org v-for 와 컴포넌트](https://kr.vuejs.org/v2/guide/list.html#v-for-%EC%99%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)

~~~

is="todo-item" 속성을 보면 <li> 엘리먼트는 <ul> 안에서만 유효합니다. 

<todo-item>과 같은 일을 하지만 잠재적인 브라우저의 구문 분석 오류를 해결 합니다.

~~~

~~~ html

<div id="todo-list-example">
  <input
    v-model="newTodoText"
    @keyup.enter="addNewTodo"
    placeholder="Add a todo"
  >
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      :key="todo.id"
      :title="todo.title"
      @remove="todos.splice(index, 1)"
    ></li>
  </ul>
</div>

~~~

~~~ javascript

Vue.component('todo-item', {
  template: '\
    <li>\
      {{ title }}\
      <button v-on:click="$emit(\'remove\')">X</button>\
    </li>\
  ',
  props: ['title']
})

new Vue({
  el: '#todo-list-example',
  data: {
    newTodoText: '',
    todos: [
      {
        id: 1,
        title: 'Do the dishes',
      },
      {
        id: 2,
        title: 'Take out the trash',
      },
      {
        id: 3,
        title: 'Mow the lawn'
      }
    ],
    nextTodoId: 4
  },
  methods: {
    addNewTodo: function () {
      this.todos.push({
        id: this.nextTodoId++,
        title: this.newTodoText
      })
      this.newTodoText = ''
    }
  }
})

~~~