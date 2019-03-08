Prototype
------------------------------------
- 객체는 언제나 함수로 생성된다.
~~~javascript
function Person() {
  this.eyes = 2;
  this.nose = 1;
}
var kim  = new Person();
var park = new Person();
console.log(kim.eyes);  // => 2
console.log(kim.nose);  // => 1
console.log(park.eyes); // => 2
console.log(park.nose); // => 1
// kim과 park은 eyes와 nose를 공통적으로 가지고 있는데
// 메모리에는 eyes와 noes가 두 개씩 총 4개가 할당됩니다. ( kim, park 각각 2개 )
// 이러한 메모리 낭비를 protoype으로 해결할 수 있다.
function Person() {}
Person.prototype.eyes = 2;
Person.prototype.nose = 1;
var kim  = new Person();
var park = new Person():
console.log(kim.eyes); // => 2

function Person() {} // => 함수
var personObject = new Person(); // 함수로 객체를 생성
var obj = {}; // [1]
var obj = new Object(); // [2]
~~~
- [1]과 [2]는 같은 코드이다.
- Object는 JavaScript에서 기본적으로 제공되는 함수이다.
- Object뿐만 아니라 Function, Array도 모두 함수로 정의되어 있다.
- 함수가 정의 될 때에는 2가지 일이 이루어진다.
1. 해당 함수에 Constructor(생성자) 자격 부여
- 생성자 자격이 부여되면 new를 통해 객체를 만들어 낼 수 있게 된다.
2. 해당 함수의 Prototype Object 생성 및 연결
- 함수를 정의하게 되면 함수만 생성되는 것이 아니라 Prototype Object도 같이 생성이 된다.  
![함수 정의](https://github.com/kkoon9/node.js/blob/master/img/javascript_prototype.PNG)  
- 생성된 함수는 protoype이라는 속성을 통해 Prototype Object에 접근할 수 있다.
- Prototype Object는 일반적인 객체와 같으며 기본적인 속성으로 constructor와 _proto_를 가지고 있다.
- constructor는 Prototype Object와 같이 생성되었던 함수를 가리키고 있다.
- _proto_는 Prototype Link이다.
## Prototype Object
- 일반적인 객체이므로 속성을 마음대로 추가/삭제 할 수 있다.  
![Prototype Object](https://github.com/kkoon9/node.js/blob/master/img/prototypeObject.PNG) 
## Prototype Link  
~~~javascript
function Person() {}
Person.prototype.eyes = 2; // 2
Person.prototype.nose = 1; // 1
var kim = new Person();
var park = new Person();
kim.eyes //2
~~~
- 위 코드처럼 kim에는 eyes라는 속성이 없는데도 kim.eyes를 실행하면 2라는 값을 참조한다.
- 바로 _proto_ 속성이 가능하게 해준다.
- _proto_는 객체가 생성될 때 조상이었던 함수의 Prototype Object를 가리킨다.
- kim 객체가 eyes를 직접 가지고 있지 않기 때문에 eyes 속성을 찾을 때까지 상위 프로토타입을 탐색한다.
- 최상위까지 도달했는데도 못찾을 경우 undefined를 리턴한다.
- _proto_속성을 통해 프로토타입과 연결되어 있는 형태를 __프로토타입 체인__ 이라고 한다.