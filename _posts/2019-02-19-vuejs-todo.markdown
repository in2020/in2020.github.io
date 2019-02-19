---
layout: post
title:  "Vue.js - 할일 목록 연습"
date:   2019-02-19 11:00:00 +0900
categories: vue
---

[참고 페이지 kr.vuejs.org v-for 와 컴포넌트](https://kr.vuejs.org/v2/guide/list.html#v-for-%EC%99%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)

[Simple list filter with Vue.js](https://codepen.io/blakewatson/pen/xEXApK)

# checkbox 필터 적용(check된 항목 제외 검색) todo list

~~~ html

<div id="app">
    <input type="text" v-model="todoText" @keyup.enter="addTodo">
    <input type="checkbox" v-model="filterCompleted" >
    <ul>
        <li
            v-for="(todo, index) in todosWithFilter"
            :todo="todo"
            :key="todo.id"
        >
            <input v-model="todosWithFilter[index].isCompleted" value="1" type="checkbox">
            {{ todo.text }}
            <button @click="removeTodo(index)">remove</button>
        </li>
    </ul>
</div>

~~~

~~~ javascript

new Vue({
        el: '#app',
        data: {
            todos: [],
            todoText: '',
            todoIndex: 0,
            filterCompleted: false
        },
        methods: {
            addTodo: function(){
                this.todos.push({ id: this.todoIndex++, text: this.todoText, isCompleted: false });
                this.todoText = '';
            },
            removeTodo: function(todoIndex){
                Vue.delete(this.todos, todoIndex);
            }
        },
        computed: {
            todosWithFilter: function(){
                var filterCompleted = this.filterCompleted;
                return this.todos.filter(function(todo){
                    if(filterCompleted){
                        return !todo.isCompleted;
                    }else{
                        return true;
                    }
                });
            }
        }
    });

~~~