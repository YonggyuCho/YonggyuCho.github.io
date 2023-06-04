---
layout: post
title: "JavaScript 비동기 처리"
subtitle: "JavaScript 비동기 처리 공부."
date: 2023-06-03
background: ''
categories:
  - JavaScript
tags:
  - JavaScript
  - asynchronous

---

# JavaScript의 비동기처리  

자바스크립트의 비동기처리란 특정 코드의 연산이 끝날까지 기다리지않고 다음코드를 먼저 실행하는 자바스크립트의 특성이다.

## 비동기 처리의 예시

```Javascipt
console.log('hello')

setTimeout(function() {
  console.log('Good')
}, 3000)

console.log('Bye')
```
이런 코드가 존재할때
보통 비동기처리를 모르는사람은 콘솔에 hello 3초후 Good, Bye 이렇게 로그가 찍힐거라 예상하지만
실제는 hello, Bye 3초후 Good 이렇게 찍힌다
  
**그 이유는 setTimeout이 3초를 기다리는동안에 Bye를 출력해버리는 자바스크립트의 비동기특성 때문이다. **

 이러한 문제점을 바로잡기위한 함수가
 **Callback(콜백)**
 함수이다. 
  
 콜백함수를 사용하면 특정 로직이 끝났을 때 원하는 동작을 실행시킬 수 있습니다.
 
 
 
 
 
 
 
 

