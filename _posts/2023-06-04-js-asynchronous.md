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

```html
<pre style="background-color: #f2f2f2;">
<code>
console.log('hello')

setTimeout(function() {
  console.log('Good')
}, 3000)
</code>
</pre>

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
 콜백함수는 특정한 이름이 존재하는 함수가 아니라 함수에 인자를 함수로넣고 사용하여 특정 로직이 끝나고나서 함수를 다시 호출하는것이다.
 
 예시코드를 보자
 ```Javascipt
 function getData(callbackFunc) {
	$.get('https://domain.com/products/1', function(response) {
		callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
	});
}

getData(function(tableData) {
	console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
 ```
getData의함수의 인자에 콜백함수가 들어간다. 
$.get은 URL서버에서 데이터를 받아오는것인데 그 값을 response에 저장한다. 
콜백함수를 사용하지않으면 response에 값을 넣기도전에 끝나버린다. 하지만 콜백함수를 사용하여 $.get이 끝나고나서 callbackFunc함수를 다시호출하여 response에 그 데이터를 넣어준다.

## 콜백지옥

콜백지옥은 비동기 처리를 위해 콜백 함수를 연속해서 사용할떄 발생하는 문제이다.
```Javascript
$.get('url', function(response){
	callback1(response, function(id){
		callback2(id, function(rs){
			callback3(rs, function(data){
				console.log(data)
			})
		})
	})

})
 ```
 
 이처럼 연속적으로 콜백함수를 호출하였을시 코드의 가독성은 떨어지고 로직을 변경하기도 까다로워진다.

## 해결방법

 만약 코딩 패턴으로만 콜백 지옥을 해결하려면 밑의 방식으로 콜백 함수를 분리해주면된다.
 ```Javascript
function callback1(response, function(id){
	callback1Data(id, callback2)
})
function callback2(response, function(rs){
	callback2Data(rs, callback3)
})
function callback3(response, function(data){
	console.log(data)
})
 $.get('url', function(response){
 	callbackData(respones, callback1);
})
```
 일반적으로 콜백지옥을 해결하기위한 방법은 
 **Promise**
 와 
**Async**
 가 존재한다
 
 ## Promise란
 
 자바스크립트 비동기처리에 사용되는 객체이다. 
 Promise는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용한다. 일반적으로 웹 어플리케이션을 구현할 때 서버에서 데이터를 요청하고 받아오기 위해 사용된다. 
 
 ### Promise 상태

Promise를 사용할 떄 알아야 할 점은 바로 상태(status) 입니다. 여기서 말하는 상태란 프로미스의 처리 과정을 의미합니다.
`New Promise()`
로 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖는다.
- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은상태
- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태
 
#### Peding(대기)
먼저 `New Promise()` 메서드를 호출하면 대기상태가 된다.
`New Promise()`를 호출할때 콜백함수를 선언할수도 있고, 콜백함수의 인자는 `resolve`, `reject` 이다.
```javascript
new Promise(function(resolve, reject){
})
```

#### Fulfilled(이행)
여기서 콜백 함수의 인자 `resolve`를 실행하면 이행 상태가 된다.
```javascript
new Promise(function(resolve, reject){
	resolve()
})
```
그리고 이행 상태가 되면 아래와 같이 `then()`을 이용하여 처리 결과 값을 받을 수 있습니다.
```javascript
new Promise(function(resolve, reject){
	var data = 100
	resolve(data)
})
getData().then(function(resolvedData){   //resolve의 결과 값을 then을통해 resolveData로 받았다.
	console.log(resolvedData)   //100
})
```

#### Rejected(실패)
반대로 여기서 콜백 함수의 인자 `reject`를 실행하면 실패 상태가 된다.
```javascript
new Promise(function(resolve, reject){
	reject()
})
```

그리고 실패 상태가 되면 아래와 같이 `catch()`을 이용하여 실패처리 결과 값을 받을 수 있습니다.
```javascript
new Promise(function(resolve, reject){
	reject(new Error("Is Error"))
})
getData().then().catch(function(err){   //Is Error를 err에 받았다
	console.log(err)   // Error : Is Error
})

```
### 예시코드

밑코드는 Promise를 사용하지않는 callback함수로의 비동기 처리이다.
```javascript
function getData(callbackFunc) {
	$.get('https://domain.com/products/1', function(response) {
		callbackFunc(response) // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
	})
}

getData(function(tableData) {
	console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
})
```
 
 위코드에 Promise를 적용하면 아래와 같은 코드가 된다.
 
```javascript
 function getData(callback){
 	return new Promise(function(resolve, reject) {  // Promise를 사용할때에는 return을 사용해줘야한다.
		$.get('url 주소', function(response){
		resolve(response)   //데이터를 받으면 resolve 호출
		})
	})
}
getData().then(function(tableData){ //resolve의 결과값이 여기로 전달된다.
	console.log(tableData) //response의 값이 tableData로 전달된다.
 })
  ```

 이제는 `Promise()`,`resolve()`,`then()` 과 같은 함수의 역할이 보인다.
 
 
