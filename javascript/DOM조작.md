# window 객체 프로퍼티 및 메서드
https://developer.mozilla.org/en-US/docs/Web/API/Window

* Window.document() : 창이 포함하는 문서로의 참조를 반환
* Window.frames() : 현재 창의 하위 프레임을 배열로 반환
* Window.history() : History 객체 참조를 반환해서 과거 방문한 페이지로 이동 가능
* Window.location() : 현재 url을 가져오거나 설정함
* Window.localStorage() : 키값만 알면 토큰값을 가져올 수 있음
* Window.scrollx() : 좌표를 사용하여 스크롤

* Window.alert(): 경고 메시지 표시
* Window.confirm(): 확인 또는 취소를 묻는 대화 상자를 표시
* Window.prompt(): 사용자에게 텍스트를 입력받을 수 있는 대화 상자를 표시

* Window.setTimeout(): 특정 시간 후에 함수를 한 번 실행하도록 예약하는 메서드
* Window.setInterval(): 특정 시간 간격으로 함수를 반복해서 실행하도록 예약하는 메서드

<br/>

# Document 메서드
* DOM : HTML을 조작 가능한 객체 형태로 만든 것  
    * XML DOM : XML 요소에 접근 가능

* 노드의 종류
    * 요소 노드 : 노드를 가져올 떄 HTML 태그 요소만 가져옴
    * 텍스트 노드
    * 주석 노드

<br/>

## HTML 요소 선택

```js
document.getElementById('id');  // 단일 태그 전체 반환
document.getElementsByClassName('className');   // HTMLCollection(3) [button.tab-button, button.tab-button, button.tab-button]
document.getElementsByTagName('tagName');   // HTMLCollection(2) [li.grandchild, li.grandchild]
document.getElementsByName('name'); // HTMLCollection 반환

document.querySelector('.className');   // 단일 태그 전체 반환
document.querySelectorAll('#id');   // NodeList(3) [button.tab-button, button.tab-button, button.tab-button]

child.parentElement;    // 부모 요소 찾기
parent.firstElementChild;   // 첫번째 자식 요소 선택
parent.lastElementChild;   // 마지막 자식 요소 선택

elem.previousElementSibling;    // 현재 요소의 이전 형제 요소 반환
elem.nextElementSibling;    // 현재 요소의 다음 형제 요소 반환
```

<br/>

* HTML Collection vs NodeList
    * HTML Collection
        * DOM을 바라보고 있는 참조 목록, DOM이 바뀔때마다 브라우저 엔진이 자동으로 참조 업데이트됨(동적)
        * ForEach() 사용 불가, array 메서드 사용 불가(map, filter..)

    * NodeList
        * DOM을 바라보고 있는 참조 목록, 갱신이 안되기 때문에 요소 상태가 변경되면 새로고침해야 함(정적)  
          (마치 셀레니움의 Stale Element Reference Exception이 발생하는것처럼)
        * 유사배열이므로 Array 메서드 사용 불가(map, filter..)
        * ForEach()만 사용 가능
        
    * HTML Collection, NodeList를 배열로 변환하는 방법
    ```js
    const elem = document.getElementsByClassName();

    const arr_1 = Array.form(elem); // Array.form()
    const arr_2 = [...elem];    // 스프레드 문법 : 유사 배열을 펼쳐서 진짜 배열로 만들어줌
    ```

<br/>

## HTML 요소 생성

```js
document.createElement('li')    // 메모리에 지정된 HTML 요소 생성
document.body.appendChild(element)  // 메모리에 생성한 요소를 DOM에 보이도록 body에 추가
document.write()    // HTML에 텍스트 출력
```

<br/>

### HTML 노드 수정
### HTML 노드의 프로퍼티
* .nodeName : 노드의 이름
* .nodeValue : 노드 값
* .nodeType : 노드 타입

### text 노드 수정
```js
element.innerHTML = '내용이 변경됐습니다.'    // 요소에 포함된 내용에 직접 접근
element.innerText = '내용이 변경됐습니다.'    // 화면에 보이는 텍스트에 접근 가능
element.textContext = '내용이 변경됐습니다.'    // 숨겨진 텍스트에 접근 가능
element.style.backgroundColor = 'red';  // 색상 변경
```

<br/>

## HTML 이벤트 핸들러
: 이벤트가 발생했을 때 처리를 담당하는 코드

* HTML 태그 안에 직접 작성(인라인 방식)  
: HTML 태그의 onclick 속성에 자바스크립트 작성, 유지보수 어려움
    ```js
    <button onclick="alert('클릭')">클릭하면 얼럿이 뜹니다.</button>
    ```

<br/>

* JS에서 요소에 연결
    ```html
    <button id="myBtn">클릭</button>
    ```
    ```js
    const btn = document.getElementById('myBtn');

    btn.onclick = function () {
    alert('버튼 클릭됨!');
    };
    ```

<br/>

* addEventListener 사용
    ```js
    // 요소.addEventListener('이벤트', () => {액션})

    const btn = document.getElementById('myBtn');

    btn.addEventListener('click', () => {
        alert('버튼 클릭됨!')
    })
    ```

* 마우스 이벤트 만들기
```js
const clickEvent = new MouseEvent('click', {

})
```
<br/>

* 자주 쓰이는 이벤트
    - click
    - mouseover
    - mouseout
    - keydown
    - keyup
    - submit

<br/>