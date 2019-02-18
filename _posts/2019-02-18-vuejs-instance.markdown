---
layout: post
title:  "Vue.js - 인스턴스"
date:   2019-02-18 11:00:00 +0900
categories: vue
---

[참고 페이지 kr.vuejs.org](https://kr.vuejs.org/v2/guide/instance.html)

[Vue 전체 옵션](https://kr.vuejs.org/v2/api/)

# Vue 인스턴스 특성

- data에 있는 속성들은 인스턴스가 생성될 때 존재한 것들만 반응형
- 어떤 속성이 나중에 필요하다는 것을 알고 있으며, 빈 값이거나 존재하지 않은 상태로 시작한다면 초기값을 지정할 필요가 있습니다.
- 유일한 예외는 Object.freeze ()를 사용하는 경우입니다. 이는 기존 속성이 변경되는 것을 막아 반응성 시스템이 추적할 수 없다는 것을 의미합니다.
- 다른 사용자 정의 속성과 구분하기 위해 $ 접두어를 붙였습니다.

~~~ javascript

var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 는 인스턴스 메소드 입니다.
vm.$watch('a', function (newVal, oldVal) {
  // `vm.a`가 변경되면 호출 됩니다.
})

~~~

- 라이프사이클

![라이프사이클](https://kr.vuejs.org/images/lifecycle.png)