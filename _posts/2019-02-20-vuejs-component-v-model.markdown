---
layout: post
title:  "Vue.js - v-model"
date:   2019-02-20 09:00:00 +0900
categories: vue
---

[kr.vuejs.org 사용자 정의 이벤트를 사용하여 폼 입력 컴포넌트 만들기](https://kr.vuejs.org/v2/guide/components.html#%EC%82%AC%EC%9A%A9%EC%9E%90-%EC%A0%95%EC%9D%98-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%ED%8F%BC-%EC%9E%85%EB%A0%A5-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0)

Vue 이해 부족으로 아래와 같이 된다고 생각 했다.

~~~ html
<div id="app">
<my-component    
    v-model="message"
    ></my-component>
</div>
~~~

~~~ javascript

Vue.component('my-component', {
    props: { message },
    template: '<div> <input type="text" :message> {{ message }} </div>'
})

new Vue({
    el: '#app',
    data: {
        message: ''
    }
})

~~~

v-model을 부모에 선언하면 v-model이 v-bind:value와 @input으로 설정된다. 

~~~ html

<input type="text" :value="message"  @input="this.message=$event.target.value">

~~~