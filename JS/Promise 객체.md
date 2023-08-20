[[동기와 비동기#비동기]]처리

비동기처리 예제
``` javascript
const workA = (value, callback) => {
  setTimeout(() => {
    callback(value);
  }, 5000);
};
const workB = (value, callback) => {
  setTimeout(() => {
    callback(value);
  }, 3000);
};
const workC = (value, callback) => {
  setTimeout(() => {
    callback(value);
  }, 10000);
};
const workD = (value, callback) => {
    callback(value);
};

workA("workA", (res) => {
  console.log(res);
});
workB("workB", (res) => {
  console.log(res);
});
workC("workC", (res) => {
  console.log(res);
});
workD("workD", (res) => {
  console.log(res);
});
```
1. 먼저 동기 함수 workD가 출력되고, 
2.  workB는 함수 "workB"란 단어 출력과(3초 후) cosnoel.log로 매개변수로 받은 값을 출력하는 함수를 인수로 전달한다.
3. workB함수에서 valuer값으로 workB를 받고,
4. workA(2초 후), workC(5초 후)도 동일한 방식으로 실행


# Promise객체
자바스크립트의 내장 객체.(예약어)
비동기 작업을 편리하게 처리하며 콜백지옥에서 구제한다.

```javascript
const promise = new Promise
```
`new` 키워드와 생성자를 사용해 생성함


### 실행함수
프로미스 객체를 만들 때엔, 인수로 executor(집행자)라는 실행함수를 전달함.
```javascript
const executor = (resolve, reject) => {
    //코드
};
const promise = new Promise(executor);
```
실행함수란? 생성자에 반드시 들어가야하는 함수이며, 작업을 비동기로 처리하는 함수.

3초 후 실행되는 비동기 함수를 프로미스 객체를 이용해 구현한다면
```javascript
const executor = (reslove, reject) => {
setTimeut (() => {
console.log('3초 후 출력됩니다.')
}, 3000)
};
const promise = Promise(executor);
```
→ 3초 후 코드가 실행된다. 
executor 함수는 프로미스 객체를 생성함과 동시에 실행되는 실행함수.


# reslove, reject
자바 스크립트 내에서 자체적으로 제공하는 콜백함수, 
executor는 비동기처리
성공→ resolve를
실패→ reject를 호출합니다.


## Promise 내부 프로퍼티
프로미스=객체이기 때문에 프로퍼티[[9. 객체#객체 프로퍼티]]를 갖고있음.
바로 `state`와 `result`
맨 처음 state: pending 상태와 result: undefined 상태를 갖고 있다가 executor(집행자) 함수가 호출하는 콜백 함수에 따라 state와 result가 변경된다.
![[Pasted image 20230802205752.png]]
이 과정에서 resolve와 reject로 나뉘어짐
resolve → fulfilled
reject → rejected


[[9. 객체#메서드]] = 내장함수
###  `.then` 메서드
executor 함수에서 비동기 처리된 결과 값을 반환할 때에는, 매개변수로 받은 resolve 콜백함수에 결과값을 전달.
→ 이 resolve 콜백 함수에 전달된 값은 프로미스 객체의 `.then()`메서드를 이용해 사용함.
→ `.then()`메서드에서는 executor 함수에서 전달한 값이 매개변수로 전달됨.

### resolve
```javascript
const executor = (resolve, reject) => {
    setTimeout(() => {
        resolve("성공");
    }, 3000);
};

const promise = new Promise(executor);
promise.then((결과) => {
    console.log(결과); // 성공
});
```
`state` → `pending`에서 `fulfilled`(이행)로 변경
`result` → `undefined`에서 '성공'으로 변경
`.then()`메서드를 통해 프로미스 객체의 값을 **매개변수**로 받아 콘솔에 출력함

### reject
```javascript
const executor = (resolve, reject) => {
    setTimeout(() => {
        reject("실패");
    }, 3000);
};

const promise = new Promise(executor);
promise.then((결과) => {
    console.log(결과); 
});
```
`state` → `pending`에서 `rejected`로 변경
`result` → `undefined`에서 `실패`로 변경
`.then` 메서드를 이용해 프로미스 객체의 결과 값을 콘솔에 출력하지만, 아무것도 출력되지 않음.

`.then`메서드는 **작업이 성공했을 때만 사용**되는 메서드이다.
`reject`되면 결과값이 출력되지 않음 


## `.catch` 메서드
`reject` 되었을 때의 결과값을 사용하기 위한 메서드
```javascript
const executor = (resolve, reject) => {
    setTimeout(() => {
        reject("실패");
    }, 3000);
};

const promise = new Promise(executor);
promise
  .then((res) => {
    console.log(res);
  })
  .catch((error) => {
    console.log(error);
  });
```
작업이 실패하면 `.then()` 메서드는 실행되지 않고, 
`.catch()` 메서드만 실행됨.