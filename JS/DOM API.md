[[웹표준#DOM]]

## DOM
문서 객체 모델. HTML을 자바스크립트가 이해할 수 있게 객체로 변환한 것
DOM이 제공하는 DOM에 접근하고 조작할 수 있는 방법

![[Pasted image 20230813230044.png]]

documenyHTML > 요소 > 어트리뷰트 > 텍스트 순서로 접근해야한다.   
어떤 요소에 접근하든 문서document노드를 거쳐야함.

# 요소 찾기/선택

```html
<body>
	<div class="today-info">
		<div class="date" id="date">
		08.13.일요일
		</div>
		<div class="clock" id="clock">
		23:03
		</div>
	<div>
</body>
```

### getElementByID
```js
console.log(docoment.getElementbyID.("date")); // 08.13.일요일
```
문서 노드 접근 > `getElementById`   
`getElementById` : 특정 요소를 id값으로 가져온다는 뜻. 특정 요소 객체를 반환.   
getElementById는 동일한 id를 갖고있는 요소가 여러개 있을 경우, **가장 위에 있는 첫 번째 요소만 반환함**

### querySelector
```js
console.log(document.querySelector("div.date")); // 08.13.일요일
```
ID가 아닌 CSS선택자로 요소를 반환함

### querySelectorAll
```html
<body>
	<div class="today-info">
		<div class="date" id="date">
		08.13.일요일
		</div>
		<div class="date" id="clock">
		23:03
		</div>
	<div>
</body>
```
여러 요소를 반환하는 API

```js
console.log(document.querySelectorAll("div.date"));
```
→NodeList가 출력됨
![[Pasted image 20230813231136.png]]

### getElementByClassName
클래스 이름으로 요소를 찾음
```js
console.log(document.getElementByClassName("date"));
```
→ HTMLCollection 출력
![[Pasted image 20230813231310.png]]

### getElementByTagName
```js
console.log(document.getElementByTagName("div"));
```
![[Pasted image 20230813231710.png]]
div tag를 사용한 모두가 출력됨

## 요소 조작하기

### className
```js
console.log(document.getElementById("date").className); // date
```
도큐먼트에서  Id값이 date인 요소를 가져온 다음 이 요소의 className을 출력함.

### className 변경
```js
const dateElement = documentgetElementByID("date");
dateElement.className = "change";
console.lof(dateElement); // class="change"
```

### id 
```js
console.log(document.querySelector("div.date").id); // date
```
class 이름이 date인 요소를 **하나만 찾기 위해서는 querySelector**를 사용해야합니다.

### id 값 변경
``` js
const dateElement = document.querySelector("div.date");
dateElement.id = "change"

console.log(dateElement);  //id="change"
```

### classList 
``` js
console.log(document.getElementById("date").classList); // 
```
 DOMTokenList 출력.  classList는 class속성에 접근하지만, 여러가지 메서드를 사용할 수 있음
	 add, remove, item, toggle, contains, replace

####  add
```js
const dateElement = document.getElementById("date");
dateElement.classList.add("change")
console.log(dateElement); // class="date change"
``` 
기존 클래스 네임 date에 change가 추가됨

#### remove
```js
const dateElement = document.getElementById("date");
dateElement.classList.add("change");
dateElement.classList.remove("date");
console.log(dateElement); // class = "change"
```
className에 date가 삭제되고 chage만 남음.

## text 노드 변경하기
```html
<body>
	<div class="today-info">
		<div class="date" id="date">
		08.13.일요일
		</div>
		<div class="clock" id="clock">
		23:03
		</div>
	<div>
</body>
```

### textContent
요소에 새로운 텍스트를 할당함

```js
const clockElement = document.getElementById("clock");
clockElement.textContent = "24:00";
const dateElement = document.querySelector("div.date");
dateElement.textContent = "08.13.Mon";
```
→ 뷰포트에 `24:00 08.13.Mon` 출력


# 요소 노드 생성
DOM tree에 추가
## createrElement
새로운 노드 생성

```js
const seasonElement = document.createElement("div"); // 생성할 요소의 태그 이름
seasonElement.classLusta.add("season"); // class이름 추가
seasonElement.textContent = "spring"; // text추가
const seasonText = document.createTextNmode("spring"); // text추가

console.log(document.getElementBuyTagName("div"));
```
JS에서 생성한 요소들이 출력되지 않는다.
요소와 텍스트 노드가 생성만 되었을 뿐 DOM Tree에 추가된 것이 아니기 때문.    
`appendChild`를 통해 DOM Tree에 추가할 수 있음

## appendChild
`appendChild` 메서드는 매개변수로 전달받은 노드를 특정 요소의 마지막 자식요소로 추가함.
```js
const todayInfoElement = document.quertSelector("div.today-info");
todayInfoElement.appenChild(seasonElement);
seasonElement.appendChild(seasonText);

console.log(document.getElementBuyTagName("div")) 
// <div class="season"spring</div>
```
`todayInfo`의 자식요소로 `seasonElement`,    
`seasonElement` 요소의 자식요소로 `seasonText`요소 추가.   

→이제 코드 시행 시, js에서 추가한 요소들이 출력됨

## addEventListener
특정 요소에 이벤트를 추가할 수 있는 API *ex) click , mouseover, scroll

``` js
const buttonElement = document.createElement("div");
buttonElement.classList.add("button");
buttonElement.textContent = "버튼";
const todayInfoElement = document.querySelector("div.today-info");
todayInfoElement.appendChild(buttonElement);
buttonElement.addEventListener("click", () => {
  window.alert("클릭");
});

console.log(document.getElementsByTagName("div"));
```
`window`객체는 현재 사용하고 있는 웹 브라우저의 창 ,  `alert` 객체는 경고창, `confirm` 객체는 확인과 취소 버튼이 있음.

