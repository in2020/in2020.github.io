---
layout: post
title:  "Vue.js - jest unit test with phpstorm"
date:   2019-02-27 13:00:00 +0900
tags: [vue]
categories: vue
---

[github @vue/cli-plugin-unit-jest](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-unit-jest)
[Vue Test Utils](https://vue-test-utils.vuejs.org/)
unit test를 하기 위한 준비

- @vue/unit-jest 모듈 추가

~~~ 

vue add @vue/unit-jest

~~~

- package.json script 추가

~~~

"test:unit": "vue-cli-service test:unit"

~~~

- test lib으로 chai 추가

~~~

npm i chai -D

~~~

-----------

test 코드 작성

[wrapper 참고](https://vue-test-utils.vuejs.org/api/wrapper/#properties)
[chai 참고](https://www.chaijs.com/api/bdd/)

~~~ javascript

import { expect } from 'chai'
import { shallowMount } from '@vue/test-utils'
import About from '@/components/About.vue'

describe('About.vue', () => {
  it('renders props.msg when passed', () => {
    const msg = 'new message'
    const wrapper = shallowMount(About, {
      propsData: { msg }
    })
    expect(wrapper.html()).contain('Loremh ipsum')
  })
})


~~~

phpstorm 설정

- run > edit configuration
- add > npm 
  - package.json 경로 설정
  - scripts 항목 test:unit 선택
- run!