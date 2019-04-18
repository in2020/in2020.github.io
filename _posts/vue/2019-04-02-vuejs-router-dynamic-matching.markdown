---
layout: post
title:  "Vue.js - Router 동적 라우트 매칭"
date:   2019-04-02 13:00:00 +0900
tags: [vue, vue-router]
---

[Vue Router 동적 라우트 매칭](https://router.vuejs.org/kr/guide/essentials/dynamic-matching.html)

path에 동적 세그먼트를 콜론으로 선언하고

~~~ javascript

const router = new VueRouter({
  routes: [
    // 동적 세그먼트는 콜론으로 시작합니다.
    { path: '/user/:id', component: User }
  ]
})

~~~

$route.params.id로 호출 

~~~ html

<div>User {{ $route.params.id }}</div>

~~~


$route.params 외에도 $route 객체는 $route.query (URL에 쿼리가 있는 경우), $route.hash 등의 유용한 정보를 제공합니다

매개 변수와 함께 라우트를 사용할 때 주의 해야할 점은 사용자가 /user/foo에서 /user/bar로 이동할 때 동일한 컴포넌트 인스턴스가 재사용된다는 것입니다. 

두 라우트 모두 동일한 컴포넌트를 렌더링하므로 이전 인스턴스를 삭제 한 다음 새 인스턴스를 만드는 것보다 효율적입니다. 

그러나 이는 또한 컴포넌트의 라이프 사이클 훅이 호출되지 않음을 의미합니다.