---
layout: post
title:  "Vue.js - NUXT View"
date:   2019-04-29 02:00:00 +0900
tags: [vue, nuxt]
---

참고: [NUXT JS - Views](https://ko.nuxtjs.org/guide/views)

프로젝트 루트 경로에 `app.html` 파일을 생성하여 html 확장 가능하다

- Layouts

페이지 컴포넌트를 레이아웃에 렌더링하기 위해서 꼭 `<nuxt/>` 태그를 작성하세요.

~~~ javascript

<template>
  <nuxt/>
</template>

~~~

Layout 사용

 ~~~ javascript
 
 export default {
  layout: 'blog'
}
 
 ~~~

 - Pages

개발에 용이하도록 Pages에 존재하는 컴포넌트는 추가 속성을 제공한다.

  - asyncData:	가장 중요한 속성이며 비동기적으로 만들 수 있고, 첫 번째 인자로 전달 받을 수도 있습니다.
  - fetch:	페이지가 렌더링되기 전에 스토어를 채우기위해 사용되며, 구성 요소 데이터를 설정하지 않는다는 점을 제외하면 데이터 메소드와 같습니다.
  - head:	현재 페이지에 대한 특정 메타 태그를 설정하려면 이곳에서 확인합니다.
  - layout:	layouts 폴더에 정의된 레이아웃을 지정할 수 있습니다.
  - transition:	페이지에 대한 특정 트랜지션을 설정합니다.
  - scrollToTop:	기본값은 false 입니다. 페이지를 렌더링하기 전에 페이지를 맨 위로 스크롤할 것인지를 나타내며, 중첩 라우트를 위해 사용됩니다.
  - validate:	동적 라우트에 대한 유효성을 검사합니다.
  - middleware:	이 페이지에 대한 미들웨어를 설정하면, 미들웨어는 페이지를 렌더링하기 전에 호출.

- HTML Head

Nuxt.js는 headers 와 html attributes 를 갱신하기 위해서 vue-meta를 사용합니다.

~~~ javascript

export default { 
  head: {
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' }
    ],
    link: [
      { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css?family=Roboto' }
    ]
  }
}

~~~

