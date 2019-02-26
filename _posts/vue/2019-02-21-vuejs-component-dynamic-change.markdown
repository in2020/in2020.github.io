---
layout: post
title:  "Vue.js - Dynamic Components"
date:   2019-02-21 13:00:00 +0900
tags: [vue]
categories: vue
---

[vuejs.org Dynamic & Async Components](https://vuejs.org/v2/guide/components-dynamic-async.html#keep-alive-with-Dynamic-Components)

[Passing props dynamically to dynamic component in VueJS](https://stackoverflow.com/questions/43658481/passing-props-dynamically-to-dynamic-component-in-vuejs)

컴포넌트 변경 방법

~~~ html 
 
<component v-bind:is="currentTabComponent"></component>
 
~~~

위와 같이 컴포넌트를 component 태그와 currentTabComponent 변수에 바인드하여 사용할때

currentTabComponent 변수는 component의 옵션 객체만 설정하여 넘겨 주면 된다.

~~~ html

<div id="app">
        <div>
            <button v-for="tab in tabs" @click="switchContents(tab.contentsComponent)">
                <span>{{ tab.name }}</span>
            </button>

            <component :is="currentTabComponent"></component>

        </div>
    </div>

    <template id="template1">
        <div class="content contents1"></div>
    </template>
    <template id="template2">
        <div class="content contents2"></div>
    </template>
    <template id="template3">
        <div class="content contents3"></div>
    </template>

~~~

~~~ javascript

    var contents1Component = {template: '#template1'};
    var contents2Component = {template: '#template2'};
    var contents3Component = {template: '#template3'};

    var vm = new Vue({
        el: '#app',
        data: {
            tabs: [
                {name: 'tab1', contentsComponent: contents1Component},
                {name: 'tab2', contentsComponent: contents2Component},
                {name: 'tab3', contentsComponent: contents3Component}
            ],
            currentTabComponent: contents1Component
        },
        methods: {
            switchContents: function(contentsComponent) {
                this.currentTabComponent = contentsComponent;
            }
        }
    });

~~~


컴포넌트 변경 전 변경전 컨포넌트 변경사항을 유지하는 방법

~~~ html

<!-- Inactive components will be cached! -->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>

~~~

컴포넌트 동적 변경시 데이터 전달 방법

~~~ html

<component :is="currentComponent" v-bind="currentProperties"></component>

~~~

~~~ javascript

data: function () {
  return {
    currentComponent: 'myComponent',
  }
},
computed: {
  currentProperties: function() {
    if (this.currentComponent === 'myComponent') {
      return { foo: 'bar' }
    }
  }
}

~~~