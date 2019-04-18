---
layout: post
title:  "Vue.js - Router 지연된 로딩"
date:   2019-04-18 00:00:00 +0900
tags: [vue, vue-router]
---

참고 : [Vue Router - Lazy loading](https://router.vuejs.org/kr/guide/advanced/lazy-loading.html)

코드가 늘면 js파일이 커져서 한번에 다운받기 부담스럽다.

Router 지연된 로딩을 사용하면 파일을 쪼개어 기능이 필요할때 로드되도록 할수 있다.

아래와 같이 선언하고 vue cli를 이용하여 빌드하면 해당 컴포넌트 관련 파일이 분할되어 생성된다.

~~~ javascript

const AsyncItem = () => import('./components/AsyncItem.vue');

~~~

라우터에서 사용 방법은 같다. 컴포넌트 정의만 다를 뿐이다.

~~~ javascript

const AsyncItem = () => import('./components/AsyncItem.vue');
const routes = [
  { path: '/async',
    component: App,
    children: [
      {
        path: '',
        component: AsyncItem
      }
    ]
  },
];

~~~






