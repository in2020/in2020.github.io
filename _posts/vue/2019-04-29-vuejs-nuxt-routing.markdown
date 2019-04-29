---
layout: post
title:  "Vue.js - NUXT 라우팅"
date:   2019-04-29 00:00:00 +0900
tags: [vue, nuxt]
---

참고: [NUXT JS - 라우팅](https://ko.nuxtjs.org/guide/routing)

pages 디렉토리 내의 Vue 파일 구조를 기반으로 vue-router 설정을 자동으로 생성합니다.

- 동적 라우트

vue 파일에 언더바(_)를 접두사로 붙여 표현

- 중첩 라우트

폴더와 같은 이름 으로 Vue 파일을 생성. `<nuxt-child/>` 사용

- 미들웨어

middleware/ 디렉토리 파일 이름은 곧 미들웨어의 이름

미들웨어는 아래의 세가지에서 순차적으로 실행됩니다:

- nuxt.config.js
- 매칭된 레이아웃
- 매칭된 페이지

미들웨어 첫번째 인자는 context

~~~ javascript

export default function (context) {
  context.userAgent = process.server ? context.req.headers['user-agent'] : navigator.userAgent
}

~~~

nuxt.config.js 미들웨어 호출

~~~ javascript

export default {
  router: {
    middleware: 'stats'
  }
}

~~~

매칭 레이아웃, 페이지 미들웨어 호출

~~~ javascript

export default {
  middleware: 'stats'
}

~~~