---
layout: post
title:  "TDD By Example 1부 화폐 예제"
date:   2019-07-20 01:00:00 +0900
tags: [TDD]
---

참고 도서: Test-Driven Development: By Example (켄트 벡)

TDD 리듬

1. 테스트 추가
2. 테스트 실행, 실패 확인
3. 테스트를 성공하도록 수정
4. 테스트 실행. 성공 확인
5. 리팩토링 

4단계까지는 어떤 죄를 저지르던지 빨리 진행해야 한다.

이를 통한 변화 포인트: 수없이 작은 단계를 통한 리팩토링.

우리의 목적은 작동하는 깔끔한 코드다.

어떤 구현이 올바른가에 대한 우리 추측이 완벽하지 못한 것과 마찬가지로 올바른 인터페이스에 대한 추측 역시 절대 완벽하지 못하다.

올바른 보폭이라는 것은 존재하지 않는다. 상황에 따라 속도를 조절할 줄 알아야한다.