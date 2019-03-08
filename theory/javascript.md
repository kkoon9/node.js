JavaScript
-----------------------
- - -
## JavaScript란?
- 객체 기반의 스크립트 프로그래밍 언어이다.
- 웹 브라우저 내에서 주로 사용하며, 다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가지고 있다.
- Node.js와 같은 런타임 환경과 같이 서버 사이트 네트워크 프로그래밍에도 사용되고 있다.

## JavaScript의 핵심 개념
### 1. 객체
- boolean, number, string, null, undefined을 제외한 모든 것이 객체이다.
- 함수도 객체로 간주한다.
### 2. 프로토타입
- 프로토타입 기반 언어라고 불린다.
- 자바도 OOP이다.
- JavaScript에는 클래스대신 프로토타입이라는 것이 존재한다.
- 클래스가 없으니 상속 기능도 없다.
- Prototype Link + Prototype Object
### 3. 실행 컨덱스과 클로저
- 자신만의 독특한 과정을 실행 컨텍스트로 만들고 그 안에서 실행이 진행된다.
- 이 실행은 자신만의 유효범위를 갖는데 이 때, 클로저를 구현할 수 있다.

## Javascript의 특징
### 1. 스크립트 언어이다.
- 웹페이지를 동작을 다이나믹하게 구현할 수 있다.
- 코딩이 간결하다.
### 2. 프로그래밍 언어이다.
- 웹에서 벗어나 독립적으로 프로그램 구현이 가능하다.
### 3. 동적 바인딩, 동적 언어이다.
- 컴파일 시 자료형, this, 변수, scope 등이 정해지는 것이 아니라 실행 중에 정해지고 변경된다.
### 4. 표준이 있지만 브라우저마다 지원하는 범위가 다르다.
- ECMAScript라는 표준 자바스크립트가 있지만 브라우저의 자바스크립트 엔진마다 지원범위에 차이가 있다.

## Javascript 문법
### 1. const, let
- var 대신 const와 let으로 대체한다.
- const와 let은 블록 스코프를 가진다.
- 그러므로 블록 안에서 선언된 const 혹은 let은 블록 밖에서 접근할 수 없다.
- const : 한번 값을 대입하면 다른 값을 대입할 수 없다. 또한 초기화 시 값을 대입하지 않으면 에러가 발생한다.
- let : 한 번 초기화했던 변수에 다른 값을 대입할 수 있다.
### 2. 템플릿 문자열
- 백틱(`)으로 감싼다. 백틱으로 감싸면 문자열 안에 변수를 넣을 수 있다.
~~~javascript
// ES5 문법 : 가독성이 떨어진다.
var num1 = 1;
var num2 = 2;
var result = 3;
var string1 = num1 + ' 더하기 ' + num2 + '는 \'' + result + '\''; // "1 더하기 2는 '3'"

// ES2015 : ES5에 비해 훨씬 깔끔하고 가독성이 좋다.
const num3 = 1;
const num4 = 2;
const result2 = 3;
const string2 = `${num3} 더하기 ${num4} 는 '${result2}'`; // "1 더하기 2는 '3'"
~~~
### 3. 객체 리터럴
- 객체의 매서드에 함수를 연결할 때 콜론(:)과 function을 부이지 않아도 된다.
- 속성명과 변수명이 겹치는 겨웅에는 한 번만 쓰면 된다.
- 객체의 속성명을 동적으로 생성할 수 있다.
### 4. 화살표 함수
~~~javascript
function add1(x,y) {
    return x + y;
}
function add2 = (x, y) => {
    return x + y;
}
const add3 = (x, y) => x + y;
const add4 = (x,y) => (x+y); // add3과 차이 없음!

function not1(x) {
    return !x;
}
const not2 = x => !x;
~~~
- function 선언 대신 =>(화살표) 기호로 함수를 선언한다.
- 화살표 함수를 통해 return문을 줄일 수 있다.
- 기존의 function과 다른 점은 this 바인드 방식이다.  
### 5. 비구조화 할당
- 객체와 배열로부터 속성이나 요소를 쉽게 꺼낼 수 있다. 
~~~javascript
var array = ['nodejs', {}, 10, true];
var node = array[0];
var obj = array[1];
var bool = array[array.length-1];

const array = ['nodejs', {}, 10, true];
const [node, obj, , bool] = array;
~~~
### 6. 프로미스(Promise)
- 자바스크립트와 노드의 API들이 콜백 대신 프로미스 기반으로 재구성된다.
- 콜백 헬을 극복했다는 평가를 받는다.
[[Tip]]
콜백 헬 : 콜백 함수로 인해 코드의 복잡성이 증가하고 가독성이 떨어지는 경우
Callback 함수가 그 결과 값을 가지고 Callback을 다시 호출하고, 그 결과 값으로 또 다시 Callback을 호출하게 될 때 발생한다.
[[/Tip]]
1. 프로미스 객체를 생성
~~~javascript
const condition = true; // true면 resolve, false면 reject
const promise = new Promise((resolve, reject) => {
    if(condition) {
        resolve('성공');
    } else {
        reject('실패');
    }
});

promise
    .then((message) => {
        console.log(message); // 성공(resolve)한 경우 실행
    })
    .catch((error) => {
        console.error(error); // 실패(reject)한 경우 실행
    });
~~~
- new Promise로 프로미스를 생성할 수 있고, 안에 resolve와 reject를 매개변수로 갖는 콜백 함수를 넣어준다.
- then이나 catch에서 다시 다른 then이나 catch를 붙일 수 있다.
- 이전 then의 return 값을 다음 then의 매개변수로 넘긴다.
- 콜백을 프로미스로 바꾸는 방법
~~~javascript
function findAndSaveUser(Users) {
    Users.findOne({}, (err, user) => { // 첫 번째 콜백
    if (err) {
        return console.error(err);
    }
    user.name = 'zero';
    user.save((err) => { // 두 번째 콜백
        if (err) {
            return console.error(err);
        }
        User.findOne({ gender: 'm' }, (err, user) => { // 세번째 콜백
            //생략        
        });
    });
    });
}
~~~
- 콜백 함수가 세 번 중첩되어 있다. 콜백 함수가 나올 때마다 코드의 깊이가 깊어진다.
- 그렇게 되면 각 콜백 함수마다 에러도 따로 처리해줘야 한다.
~~~javascript
function findAndSaveUser(Users) {
    Users.findOne({})
        .then((user) => {
            user.name = 'zero';
            return user.save();
        })
        .then((user) => {
            return Users.findOne({ gender: 'm'});
        })
        .then((user) => {
            //생략
        })
        .catch(err => {
            conole.error(err);
        });
}
~~~
- 하지만 모든 콜백 함수를 위 코드와 같이 바꿀 수 있는 것은 아니다.
- 메서드가 프로미스 방식을 지원해야 한다.
- 위의 코드는 findOne과 save 메서드가 내부적으로 프로미스 객체를 가지고 있어서 가능하다.

### 7. async/await
- 