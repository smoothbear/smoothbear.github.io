---
layout: "post"
title: "특정 요청에 대한 CORS 비허용"
subtitle: "스프링에서 CORS가 허용되지 않는 문제"
categories: 문제 해결
tags: [spring, cors]
---



api 연동을 하는데, 특정 경로에서만 CORS(교차 출처 리소스 공유)가 허용되지 않는 오류가 떴다.

분명히 WebMvcConfigurer를 상속받아 모든 경로와 Origin에 대해서 모두 허용하였지만, 오류가 났었다.



### 해결 방법

* curl로 OPTIONS 메소드로 요청을 날려보자.

  -> 이때 401 에러가 뜬다면, SecurityConfig에서 OPTIONS 또한 permitAll을 해주어야 한다.



### 원인

POST 메소드에 대해서만 permitAll을 하였더니, OPTIONS는 권한이 부족해 접근하지 못하는 문제가 생겼다.

이로 인해, OPTIONS 요청으로 Cross-Origin 허가를 받지 못하였고, 이 때문에 에러가 발생한 것이다.

