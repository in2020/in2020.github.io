---
layout: post
title:  "Vue.js - Dynamic Components"
date:   2019-02-21 13:00:00 +0900
categories: vue
---

[vuejs.org Dynamic & Async Components](https://vuejs.org/v2/guide/components-dynamic-async.html#keep-alive-with-Dynamic-Components)

컨퍼넌트 변경 방법

~~~ html 
 
<component v-bind:is="currentTabComponent"></component>
 
~~~

컨퍼넌트 변경 전 변경전 컨포넌트 변경사항을 유지하는 방법

~~~ html

<!-- Inactive components will be cached! -->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>

~~~