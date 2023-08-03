### [웹 프론트엔드를 위한 자바스크립트 첫걸음](https://www.inflearn.com/course/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%B2%AB%EA%B1%B8%EC%9D%8C/dashboard)
강의를 듣고 개념을 정리한 필기 노트입니다.
마크다운 기반의 애플리케이션 Obsidian으로 작성되었습니다.

### [웹 프론트엔드를 위한 자바스크립트 첫걸음](https://www.inflearn.com/course/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%B2%AB%EA%B1%B8%EC%9D%8C/dashboard)
강의를 듣고 개념을 정리한 필기 노트입니다.


[[1. 변수와 상수]]
[[2. 자료형과 형변환]]
[[3. 연산자]]
[[4. 조건문]]
[[5. 함수]]
[[5.1 지역변수 전역변수]]
[[6. 스코프]]
[[7. 호이스팅]]
[[8. 함수 표현식]]
[[9. 객체]]
[[10. 배열]]

# 자바 스크립트의 표기법
1. Dash-case
	1. HTML 과 CSS에서 주로 사용되는, 하이픈 기호로 단어 사이를 연결하는 방법
2. Snake_case
	1. 언더바 기호로 단어 사이를 연결.
3. camelCase
	1. 기호 대신 단어의 첫 글자를 대문자로 작성함. 단, 첫번째 단어의 첫 글자는 소문자로 작성함. JS에서 주로 사용됨.
4. PascalCase
	1. camelCase와 유사하지만, 첫번째 단어 첫 글자 역시 대문자로 표기. JS 생성자 함수의 이름을 표시할 때 사용됨.


# 자바 스크립트의 넘버링 

 ```javaScript
 const furits ['apple', 'plum', 'pare']
 console.log(fruits(0)) //'apple'
```
숫자 0부터 시작됨

# JS기초 
1. 자바스크립트는  HTML 컨텐츠를 수정하는 것이 가능하다 ex. `getElementByID()`
	```Javascript
	documnet.getElementID('id이름').innerHTML = "바꿀 value"
	```
2. 자바스크립트는 HTML attribute를 바꾸는 것이 가능하다
3. 자바스크립트는 style(css)를 바꿀 수 있다. 
4. 자바스크립트는 HTML 요소들을 hide, show할 수 있다.
5. 자바스크립트는 외부 스크립트를 연결할 수 있다.


# 프로토타입
JS는 프로토타입 기반 언어라 불린다.
모든 객체들이 메서드와 속성들을 상속받기 위한 템플릿으로서, 프로토타입 객체를 가진다는 의미이다.
모든 객체는 자신의 부모 역할을 하는 프로토타입의 링크를 갖고 있으며,
이 링크를 통해 프로토타입으로부터 프로퍼티나 메서드를 상속받을 수 있다.


# 이벤트란?
HTML요소에서 발생하는 것들.
```
ex. 웹페이지가 로딩을 마쳤다.
ex. 입력창이 바뀌었다.
ex. 버튼이 클릭되었다.
```
HTML은 이벤트 핸들러 어트리뷰트로, 자바스크립트 코드가 HTML요소에 추가될 수 있도록 허용한다.

자주 사용되는 HTML 이벤트
- Event
- ohchange: HTML element chage
- onclick: 유저가 HTML 요소를 클릭함
- onmouseover: user moves the mouse over an element
- onmouseout: user moves the mouse out from an element
- onkeydown: user pushes keyboard key
- onload: 브라우저가 웹페이지 로딩을 끝냄
