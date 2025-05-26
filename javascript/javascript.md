# 기초 문법
> <span style="color=darkgray">**브라우저 콘솔창에서 JS가 동작하는 방식  
REPEL(Read, Evaluation, Print, Loop)  
: 코드를 입력하면 결과가 바로 출력되는 과정을 반복하는 것**</span>

* 세미콜론을 붙여야 하는 상황
    * statement(문장)이 끝날때
    * 함수를 변수에 할당할때
    * 조건문, 반복문 등이 끝날때
    * 객체 리터럴에서 프로퍼티 정의 후 세미콜론을 붙일 수 있다.(선택)
        * 리터럴 : 프로그래밍에서 고정된 값을 직접 표현하는 방법
    * 함수 표현식

<br/>

## 변수 키워드
: 변수가 영향력을 끼치는 범위가 다름

* var
    * 전역변수처럼 모든 코드에서 사용 가능, 변수 중첩 체크가 잘 안되어 사장됨
* const
    * 현재 사용중인 함수 내부에만 영향을 줌, 고정값(상수)
    * const로 선언된 변수가 객체나 배열을 참조할 경우 내부 속성이나 요소 변경 가능
* let
    * 현재 사용중인 함수 내부에만 영향을 줌, 가변값

<br/>

## 데이터 타입
* 문자열 : "문자열"
* 부울 : true, false(소문자)
* 딕셔너리 : 객체라고 부름
    * 객체 호출 시 obj.key
* str = null  // 메모리에 공간은 확보되었으나 값이 없는 상태
* str = undifond // 메모리에 공간 확보가 되지 않은 상태

<br/>

## 형변환
```JS
let num = 1;
let str = "문자열"
let strNum = "1"

String(num);    // "1"  문자열로 값 리턴
Number(srt);    // NaN  숫자로 값 리턴, NaN은 형변환이 불가능하다는 뜻

parseFloat(num) // "1.0"   float 형식으로 값 리턴
parseInt(strNum) // 1   숫자로 값 리턴

num.toString()  // "1"  문자열로 값 리턴
```

```JS
const elem = document.getElementsByClassName();

const arr_1 = Array.form(elem); // Array.form() 배열로 변환
```

<br/>

### 템플릿 리터럴
```JS
const num = 1
function MyFunction() {
    console.log(`num을 문자열로 출력해보겠습니다.: ${num}`)
}
```

<br/>

## 연산자
* 산술 연산자  
: +, -, *, /, %, **

<br/>

* 비교 연산자  
: ==, ===, !=, !==, >, <

    * 일치 연산자 : ===

        ```js
        1 == "1"    // true
        1 === "1"   // false
        ```

<br/>

* 논리 연산자  
: &&, ||, !

<br/>

* 증감연산자  
: ++  

    ```js
    i++ // 연산 후 증가
    ++i // 연산 전 증가
    ```

<br/>

* spread 연산자  
: 배열을 개별 인자로 펼침, 배열, 객체, 함수 호출시 사용

    ```js
    const arr1 = [1, 2, 3];
    const arr2 = [...arr1, 4, 5]    // [1, 2, 3, 4, 5]

    const arr3 = [10, 11, 12];
    const combined = [...arr1, ...arr3] // [1, 2, 3, 10, 11, 12]

    const obj1 = {a: 1, b: 2};
    const obj2 = {...obj1, c: 3};   // {a: 1, b: 2, c: 3}
    ```

<br/>

* rest 연산자  
: 여러 인자를 하나의 배열로 모음, 매개변수, 구조분해에 사용

    ```js
    function sum (...numbers) { // 변수 여러개를 한번에 받을 수 있다.
        return numbers  // [1, 2, 3]
    }

    sum(1, 2, 3);
    ```

<br/>

* null 병합 연산자 (Nullish Coalescing Operator)  
: nullish일때 예외처리, default값 자리에 return값이 있는 함수가 들어가도 됨(function())

    * nullish 값 : 빈 값
        - null, undefined

    ```js
    const value1 = null;
    const value2 = undefined;
    const value3 = 0;
    const value4 = '';

    console.log(value1 ?? 'default');   // value1이 null이나 undefined라면 'default'를 출력
    console.log(value2 ?? 'default');   // default
    console.log(value3 ?? 'default');   // 0
    console.log(value4 ?? 'default');   // ''
    console.log(value1 ?? value4);  // ''
    ```

<br/>

* 논리합 연산자 (Logical OR Operator)  
: falsy 일때 예외처리, default값 자리에 return값이 있는 함수가 들어가도 됨(function())

    * falsy값 : 거짓의 값을 갖는 값
        - null, undefined, 0, "", false

    ```js
    const value1 = null;
    const value2 = undefined;
    const value3 = 0;
    const value4 = '';
    const value5 = false;

    console.log(value1 || 'default');   // value1이 false면 'default'를 출력
    console.log(value2 || 'default');   // default
    console.log(value3 || 'default');   // default
    console.log(value4 || 'default');   // default
    console.log(value5 || 'default');   // default

    if(!value5) => falsy    // true
    ```
    
<br/>

* Optional Chaining
JSON을 바꾸면 객체 형식으로 변함

```js
const dog = {
    name: "뽀삐"
}

dog.age // error
const age = dog?.age;   // dog 객체의 age 프로퍼티를 호출했는데 오류가 나면 undefined를 반환함
const age = dog?.age || "없네용";   // undefined, "없네용" 반환, 이후 코드 실행됨
```

<br/>

## 함수와 메서드
**함수(Method)**|**메서드(Method)**
|:- |:- |
|호출하는 객체가 없는 경우</br>function();|객체안에있는 함수, 메서드 사용시 호출하는 객체가 있음</br>obj.function()

<br/>

* 메서드 작성 방법

    ```JS
    let object = {
        "property": function(){}
    }
    ```

* 매개변수에 기본 값 넣기
: 마지막 매개변수는 필수값이다.

```js
function temp (age, name = 'kim') {
    return name
}

temp();
```

<br/>

### 함수 선언과 반환
* 기본 함수 선언 방식

    ```js
    x = 1
    function MyFunction(x){
        let temp = 2*x + 3
        return temp
    }
    MyFunction()    // 5
    ```

<br/>

* return에서 여러개 값을 반환하는 법  
: js에서는 여러개 값을 반환하려면 타입을 지정해줘야 함

    ```js
    // 배열 방식
    function temp(){
        a = 1;
        b = 2;
        return [a, b]
    }
    temp()  // [1, 2]
    ```

    ```js
    //객체 방식
    function temp(){
        a = 1;
        b = 2;
        return {a, b}
    }
    temp()  // {a: 1, b: 2}
    ```

* 함수 호출 방법
: 함수를 변수에 담으면, 그 변수 이름으로 호출해야 함

```js
const person = {
  name: "영희",

  sayHello() {
    // 일반 함수 (메서드 축약형)
    console.log("일반 함수의 this.name:", this.name);
  }
};

person.sayHello(); 

const say = person.sayHello;
say();  // 함수 호출
```

<br/>

### 함수 표현식
* 객체 값으로 함수를 설정하는 방식

    ```js
    let myFunction = function() {
        a = 1;
        b = 2;
        return {a, b}
    };
    ```

<br/>

### 함수 사용 방식
* 익명함수
: 함수명 선언 없이 함수를 사용할 수 있다.

    ```js
    // 버전 1 - 일반 익명 함수
    const greet = function(name) {
    return `안녕하세요, ${name}님!`;
    };

    console.log(greet("지민")); // 안녕하세요, 지민님!
    ```

    ```js
    // 버전 2 - 화살표 함수(return 생략)
    const greet = (name) => `안녕하세요, ${name}님!`;
    console.log(greet);
    ```

    ```js
    // 버전 3 - 화살표 함수(return 명시)
    const greet = (name) => {return `안녕하세요, ${name}님!`};
    console.log(greet);
    ```

    ```js
    // 버전 4 - 즉시 실행 함수 표현식 (IIFE, Immediately Invoked Function Expression)
    console.log(
        ((name) => `안녕하세요, ${name}님!`)("지민")
        );
    ```

<br/>

* 함수 중첩
    * 지연함수
    : 다른 곳에서 버그가 있을 수 있다. 스코프 체이닝으로 버그의 영향을 받고싶지 않을 때 지연함수를 사용한다.
    - 스코프 체이닝 : 현재 실행중인 함수에서 변수가 없으면 1depth 위에서 찾는것

    ```js
    x = 1
    function MyFunction(x){
        let temp = 2*x + 3
        return temp
    }
    MyFunction() 

    ```

<br/>

### 구조 분해 할당
: 배열이나 객체에서 값을 꺼내서 변수에 한번에 담는 문법, 할당값이 없으면 undefined 반환

* 배열 구조분해

    ```js
    const fruits = ['apple', 'banana', 'cherry'];

    const [a, b, c] = fruits;

    console.log(a); // 'apple'
    console.log(b); // 'banana'
    console.log(c); // 'cherry'
    ```

<br/>

* 객체 구조분해

    ```js
    const user = { name: '철수', age: 20 };

    const { name, age } = user;

    console.log(name); // '철수'
    console.log(age);  // 20
    ```

<br/>

### Array 함수
* forEach() : 배열에서 index와 value를 추출  
forEach((매개변수1, 매개변수2) => {반환할 내용})

    ```js
    numbers.forEach((value, index) => {
        console.log(`인덱스 : ${index} ${value}`)
    })
    ```

<br/>

* map()
: 리스트나 배열의 각 항목에 어떤 함수를 적용해서 새로운 리스트를 만들때 사용

    ```js
    // 리스트.map(함수)
    const numbers = [1, 2, 3];

    const result = numbers.map(String);
    console.log(result);    // ['1', '2', '3']
    ```

    ```js
    // 리스트.map((매개변수1, 매개변수2) => {return 반환값})
    const triple = numbers.map(number => number *3) // list
    const triple = numbers.map((a, b) => {return a * 3;}); // list
    ```

<br/>

* length : 길이 반환
* push() : 배열 가장 마지막에 삽입
* pop() : 배열 가장 마지막 데이터 제거

* unshift() : 배열 맨 앞에 데이터 삽입
* shift() : 배열 맨 앞의 데이터 제거

* charAt(0) : 인덱스의 문자 추출

### 기타 함수
* Math.floor(10.9) : 내림 함수
* Math.found(10.9) : 반올림 함수
* Math.random() : 랜덤 함수

### async 함수
: Promise를 반환하는 비동기 함수
    * Promise를 반환하기 때문에 내부에서 await 사용 가능
    * Promise를 반환하지 못하는 함수는 wait 불가

```js
// 일반 함수 버전
async function myFunction() {
    // 비동기 작업 가능
    return '결과';
}

// 화살표 함수 버전
const myFunction = async () => {
    // 비동기 작업 가능
    return '결과';
};
```

<br/>

## 제어문
### if문
* 기본 버전

    ```js
    let money = 1000

    if(money > 5000) {
        rideTaxi();
    } else if(money > 2000) {
        rideBus();
    } else {
        walk();
    }
    ```
    
<br/>

* true, null, undifined가 아닌 경우

    ```js
    if(a) {

    }
    ```
    
<br/>

* false, null, undifined인 경우

    ```js
    if(!a) {

    }
    ```
    
<br/>

* 삼항연산식

    ```js
    let money = 1000

    (money === 5000 ? rideTaxi() : (money === 2000 ? rideBus : walk()))
    ```

<br/>

### try catch문
```js
try {
    if() {
        throw new Error('에러 발생')    // Error라는 객체를 '에러 발생'으로 초기화하여 throw(던진다)
    }

} catch (error) {
    에러분류함수_1(error);
    에러분류함수_2(error);
}
```

<br/>

## 반복문
### for
```js
// 기본 버전
for (let i = 0; i < 10; i++) {
    console.log(i)
};
```

```js
// forEach 사용 버전
myArray = [1, 2, 3, 4, 5];

myArray.forEach(element => {
    console.log(element);
});
```

```js
// for of : value값 추출
for (const number of numbers) {
    console.log(number) // 10, 20, 40
}
```

```js
// for in : 키 추출
for (const value in person) {
    console.log(value) // 10, 20, 40
}
```

### while문
while (조건){

}

```js
// 기본 버전
let i = 0;
while (i < 5) {
    console.log(i)
    i++
}
```
do {
    while문이 거짓이어도 무조건 1회 실행
} while () {

}

```js
// do while문
let i = 0;
do {
    console.log(i)
    i++;    // 1 증가
}
while (i < 0) {
    console.log(i)  // while 실행 안됨
}
```

<br/>

## this 바인딩
: 함수가 호출될 때 결정되는 동적 바인딩  
> <span style = "color:darkgray">**this : 사용하는 함수, 형태, 위치에 따라 가르키는 객체가 다름**</span>

* 최상위 this : 전역 window 객체(브라우저 관련 객체)를 가르킴
    * window.document // HTML 문서

* 'use strict'의 this : this가 있는 함수의 객체를 가르킴

* new : new를 하는 함수로 this가 가르키는 객체가 바뀐다.

* 화살표함수 : 화살표함수가 선언된 곳을 this가 가르킨다. 화살표함수에서는 new를 사용할 수 없다.

```js
window.a = 1

function a () {
    this.a  // 1, 전역 window 객체를 가르킴
}

function b () {
    'use strict'    // this가 있는 현재 함수 안의 객체를 가르킴
    let a = 0;
    this.a  // 0
}

new a() // new 바인딩
a.a // new 바인딩을 사용하면 함수 a의 a값 호출
```

<br/>

## 클래스
* 클래스

```js
class ClassName {
    sample() {

    }
}

SomeClass.a()   // 함수 호출
```
  
```js
class Animal {
    constructor(name) { // 생성자 함수, 파이썬의 __init__ 함수와 같은 역할
        this.name = name;   // Animal의 name 객체 생성
    }
    
    // 클래스 내에서 함수 선언 시 함수 키워드 사용 X
    speak() {
        console.log(`${this.name}`) // this.name 은 Animal의 name 객체
    }
}
const dog = new Animal('강아지');
dog.name // 강아지
dog.speak();    // 강아지
```

<br/>

* 상속
    * 파이썬 : class a(상속 클래스):
    * js 상속 : extends 사용

```js
class Dog extends Animal {
    constructor(name, age) {
        this.age = age;
        super(name);    // 상속받은 클래스에 'name 객체를 사용할 것이다' 라고 전달
    }
    speak() {
        console.log(`${this.name} ${this.age}`);    // 멍멍이 12
        super.speak();  // '상속받은 클래스의 speak()를 사용할 것이다'
    }
}

const dog = new Dog('멍멍이', 12);
dog.speak();
```

<br/>

## Promise 객체
### CallBack 지옥
* 발생 배경
    1. JS는 싱글 스레드 방식으로 기능을 동기/비동기적으로 구현할 수 있음
        * 동기 : 현재 작업이 완료되면 다음 작업 진행 가능

        * 비동기 : 현재 작업이 완료될때까지 기다리지 않고 다음 작업 진행 가능, JS에서는 파일 읽고 쓰기, HTTP 등 통신에 사용됨

    2. JS는 이벤트 루프와 콜백 큐를 이용해서 비동기 작업이 완료되면 콜백(Callback)을 실행함  
        * 콜백(Callback): JavaScript의 이벤트 루프를 통해 비동기 작업이 완료된 후, 해당 작업의 결과를 처리하기 위해 호출되는 함수

    3. 이러한 비동기 작업은 실행 순서를 제어하기 위해 아래와 같은 방법을 사용해야 함  
        1. 이벤트 루프를 통해 비동기 함수 작업을 한다.
        2. 비동기 함수 안에 함수를 넣어서 순서대로 작업을 처리하도록 한다.
        3. 위와 같이 함수안에 함수를 넣는것을 반복하여 순차적으로 동작하게 한다.
    
    4. 이러한 제어 방식을 콜백지옥이라고 부름

        ```js
        // 콜백지옥 예시

        const button = document.getElementsByTagName('button');
        button[0].addEventListener('click', function () {
            ajaxCall(function(result)) {    // result가 반환될때까지 대기
                updateUI(result, function () {  // result를 매개변수로 받아 실행
                    hideLoader(function () {
                        ...
                    })
                })
            }
        })
        ```

<br/>

### Promise 객체
: 콜백지옥을 해결하기 위한 객체, 비동기 제어 구문과 return으로 구성됨

* 비동기 결과를 담는 컨테이너
* 세가지 상태와 return값으로 구성됨
    * pending(초기상태), fulfilled(성공), rejected(실패)

```js
// 예시 1. 직접 Promise 객체 생성
const checkAge = (age) => {
    return new Promise((resolve, reject) => {   // new Promise : Promise 객체 생성
        if(age >= 18) {
            resolve('성인입니다.'); // .then()으로 결과 전달
        } else {
            reject('미성년자입니다.');  // .catch()로 결과 전달
        }
    })
}

checkAge(20)
.then(msg => console.log('성공', msg))  // .then(함수)
.catch(err => console.log('실패', err));    // .catch(함수)
```

```js
// 예시 2. fetch 함수를 사용하여 Promise 객체를 반환
const a = fetch('https://jsonplaceholder.typicode.com/posts/1')  // fetch : 비동기 함수, promise 객체를 반환(상태 + 결과)
console.log(a); // Promise { <pending> }
a.then(resolve => resolve.json())   // .then() 안에 있는 함수의 반환값이 없으면 다음 체이닝에서 undefined가 출력됨 
.then(data => console.log('받은 데이터: ', data))
.catch(error => console.error('에러 발생: ', error))
```

```js
// 예시 3. Promise 객체를 return하는 함수
const Hello = () => {
    return Promise.resolve('안녕하세요!');
};

Hello()
.then(msg => console.log(msg))
.catch(err => console.log(err));
```

```js
// 예시 4. Promise 체이닝(Promise chaining)

function fetchData () {
    return new Promise((resolve, reject) => {   // promise 객체 생성, 비동기 실행 선언
    setTimeout(() => {  // setTimeout : 일정시간 대기, 비동기와 유사한 흐름 세팅
        const data = { id: 1, name: "kim"};
        const error = null;

        if (error) {
            reject('실패');
        } else {
            resolve(data);
        }
    }, 1000);
    })    
}

fetchData() // 비동기 실행
.then((results) => {fetchData()})  // 비동기 성공 시 두번째 비동기 실행
.then((result) => {fetchData()})    // 두번째 비동기 성공 시 실행
.then((result) => {fetchData()})
.catch(err => {console.error(err)});
```

```js
// 예시 5. 동기코드인 for문에 비동기 코드를 넣기

function fetchData () {
    return new Promise((resolve, reject) => {   // promise 객체 생성, 비동기 실행 선언
    setTimeout(() => {  // setTimeout : 일정시간 대기, 비동기와 유사한 흐름 세팅
        const data = { id: 1, name: "kim"};
        const error = null;

        if (error) {
            reject('실패');
        } else {
            resolve(data);
        }
    }, 1000);
    })    
}

for(let i = 0; i < 5; i++) {
    console.log("요청 보냄:", i);
    fetchData().then((result) => {
        console.log(result + i);
    })
}

// 요청 보냄: 0
// 요청 보냄: 1
// 요청 보냄: 2
// 요청 보냄: 3
// 요청 보냄: 4
// [object Object]0
// [object Object]1
// [object Object]2
// [object Object]3
// [object Object]4
```

<br/>

#### Promise 병렬처리 함수
: 동시에 여러 함수 실행, 결과를 한번에 반환
```js
// 실행하는 함수 중 하나라도 실패하면 전체 실패로 결과가 나옴
Promise.all([func_1, func_2, func_3]);

// 실행하는 함수 중 하나라도 실패하면 일부 실패로 결과가 나옴
Promise.allSettledl([func_1, func_2, func_3]);  
```

<br/>

### async, await
 : promise를 더 쉽게 사용하고 코드 가독성 향상을 위해 사용
 서버가 DB를 호출한 결과나 웹페이지가 요청한 결과를 기다릴때 사용

* async : 비동기 함수 선언, promise 객체를 반환함
* await : promise의 결과를 변수에 저장

```js
// 예시 1. async()
const Hello = async () => { // promise 객체를 반환
    return '안녕하세요';
};

Hello()
.then(msg => console.log(msg));
```

```js
// 예시 2. async() await()
const getMessage = () => {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve('메시지 도착');
        }, 1000);
    });
};

const showMessaage = async () => {
    const msg = await getMessage();
    console.log(msg);
};

showMessaage();
```

```js
// 예시 3. 순차 실행
function fetchData () {
    return new Promise((resolve, reject) => {   // promise 객체 생성, 비동기 실행 선언
    setTimeout(() => {  // setTimeout : 일정시간 대기, 비동기와 유사한 흐름 세팅
        const data = { id: 1, name: "kim"};
        const error = null;

        if (error) {
            reject('실패');
        } else {
            resolve(data);
        }
    }, 1000);
    })    
}

async function fetchAsync() {
    const resultOne = await fetchData();
    const resultTwo = await fetchData();
    const resultThe = await fetchData();
    const resultFor = await fetchData();
    const resultFor = await fetchData();
    const resultFiv = await fetchData();

    return resultOne + resultTwo + ... + resultFiv;
}
```

```js
// 예시 5. 비동기 이터레이션(yield)
// function*을 사용하면 yield를 사용할 수 있다.
function fetchData () {
    return new Promise((resolve, reject) => {   // promise 객체 생성, 비동기 실행 선언
    setTimeout(() => {  // setTimeout : 일정시간 대기, 비동기와 유사한 흐름 세팅
        const data = { id: 1, name: "kim"};
        const error = null;

        if (error) {
            reject('실패');
        } else {
            resolve(data);
        }
    }, 1000);
    })    
}

async function* asyncFor() {
    for(let i = 0; i < 5; i++) {
        await fetchData();  // await 함수 안에 next() 함수가 있어 실행 > 대기 > 다음으로 넘어감
        yield i;
    }
}

const run = async () => {
    for await (const num of asyncFor()) {
      console.log("값:", num);
    }
  };
  
  run();

// 값: 0
// 값: 1
// 값: 2
// 값: 3
// 값: 4
```
async for문 1
```js
// 예시 6. 비동기 이터레이션(for await of)
function fetchData() {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve({ id: 1, name: "kim" });
      }, 1000);
    });
  }
  
  const fetchAsync = () => {
    return [
      fetchData(),
      fetchData(),
      fetchData(),
      fetchData(),
      fetchData()
    ]; // Promise 객체 배열 반환
  };
  
  async function fetchAsync2() {
    for await (const result of fetchAsync()) {
      console.log(result);
    }
  }
  
  fetchAsync2();
```

<br/>

# 모듈 import
## import export(ES6 최신 문법)
```js
// export_1.js
// 객체 정보 내보내기
export class firstClassName {
    importClass () {
        console.log('클래스 import 성공');
    }
}

// import.js
// 기본 import
import { firstClassName } from "./export_1.js";

const myInstance = new firstClassName();    // 인스턴스 생성
myInstance.importClass()

// 전체 import
import * as test from './export_1.js'   // 전체 import시 별칭 필수

const firstclass = new test.firstClassName();
firstclass.importClass()
```

```js
// export_1.js
// 객체 정보 내보내기
export default class firstClassName {
    importClass () {
        console.log('클래스 import 성공');
    }
}

// import.js
// 별칭으로 import
import ani from "./export_1.js"; // 별칭 ani로 자동 호출됨

const firstclass = new ani();
firstclass.importClass();
```

<br/>

## require exports
```js
// export_1.js
class firstClassName {
    importClass() {
        console.log('클래스 import 성공');
    }
}

module.exports = firstClassName;

// import.js
// package.json에 "type": "module"이 없어야 함
const firstClassName = require('./export_1.js');

const firstclass = new firstClassName();
firstclass.importClass();
```