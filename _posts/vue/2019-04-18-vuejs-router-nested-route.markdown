---
layout: post
title:  "Vue.js - Router 중첩된 라우트"
date:   2019-04-18 00:00:00 +0900
tags: [vue, vue-router]
---

참고: [Vue Router - Nested routes](https://router.vuejs.org/kr/guide/essentials/nested-routes.html)

위 참고 사이트에서는 중첩이라는 단어를 사용했는데 와닿지가 않는다.

URI의 Path 세그먼트의 세부 설정 정도로 이해된다.

아래 두 URI가 있을때

~~~

/user/foo/profile
/user/foo/posts

~~~

라우터 설정 방법은 아래와 같다. 

~~~ javascript

const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // /user/:id/profile 과 일치 할 때
          // UserProfile은 User의 <router-view> 내에 렌더링 됩니다.
          path: 'profile',
          component: UserProfile
        },
        {
          // /user/:id/posts 과 일치 할 때
          // UserPosts가 User의 <router-view> 내에 렌더링 됩니다.
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})

~~~






