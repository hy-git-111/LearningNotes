# Web
## 정적 웹, 동적 웹
* 브라우저  
: HTML 문서나 파일을 출력하는 SW

* 정적 웹  
: html 변동시 서버에서 html 업데이트 필요(새로고침)  
사용자 정보 초기화됨

* 동적 웹  
: html 변동이 있을때 Javascript로 변동된 부분에 대한 데이터만 업데이트(랜더링, 새로고침 불필요)    
사용자 정보 유지됨

* AJAX, Asynchronyze Javascript And XML
    * 전체 페이지를 새로고침하지 않고도 자주 업데이트해야 하는 웹사이트의 특정 기능이나 섹션에 사용
    * 서비스 지속성 유지 및 트래픽 감소
    * XML HTTP Request, Fetch API로 구현함

* XHR(XMLHttpRequest) 객체
: 웹 브라우저와 서버가 데이터를 교환할 때 사용됨

    MVC 단점 : 디바이스에 따라 각각 다르게 개발해야함
    웹페이지에 변화가 았는 경우 전체 사이트 리로드
    > ajax로 개선

* SPA, Single Page Application
    * 필요한 데이터만 비동기로 받아와 현재 화면에 랜더링하여 다수의 페이지를 하나의 페이지인 것처럼 처리하는 프레임워크
        > <span style="color:darkgray">**SPA가 동적 웹을 만들어줌 > JS로 html을 구현함**</span>

        > <span style="color:darkgray">**Library vs Framework  
        Library : 사용자가 필요시 import(e.g. jQuery)
        framework : 프레임워크 규칙 준수 필요(e.g. Django)**</span>

    * 브라우저와 서버를 분리하여 개발, 브라우저에 렌더링하는 방식을 FE에서 관리함
    * SEO(Search Engine Optimization)이 어려움

    > <span style="color:darkgray">**검색엔진은 HTML 방식으로 진행됨  
    SEO는 JS가 랜더링될때까지 기다려야 함  
    따라서 SEO를 할 떄 SPA프레임워크를 사용한 부분은 포함시키지 않음**</span>


<br/>

## 웹 주소
* URI(Uniform Resource Identifier, 통합 자원 식별자)  
    * URL의 상위 버전  
    * 서버에서 특정 리소스를 구별하기 위한 식별자

* URN(Uniform Resource Name)
    * 이름으로 리소스를 특정하는 URI

* URL(Uniform Resource Locator)
    * 웹 페이지를 고유하게 식별할 수 있는 주소
    * 구조 : 프로토콜 + 도메인 + url 경로 + 쿼리 
     
[URI/URL/URN 참고자료] https://velog.io/@younoah/uri-url-urn

<br/>

### 웹 프로토콜(Protocol, 통신 규약)
* Json : 데이터 전송 시 주로 사용
    * 경량 데이터 교환 포맷(csv < json < xml)
    * 중첩 가능하여 확장이 용이
    * 검색 및 조회 속도가 빨라 데이터 저장에 많이 사용됨

* XML : 데이터 저장, 전달, 교환 시 사용
    * 복잡한 데이터 표현에 적합
    * 태그로 작성되어 계층적, 확장 용이
    * 데이터 조회 시, DOM 탐색이 필요함(느림)

* HTML : HTTP에 응답하는 방식, 웹 프로토콜

* HTTP : 클라이언트, 서버 간 데이터가 교환되는 방식에 대한 규약
    * http(Hyper Text Transform Protocol)
        * http 1.1 : 1요청 1응답의 원칙을 가진다.
        * http 메서드(행위)
            * GET : 페이지 정보, 데이터 조회 요청
            * POST : 저장할 정보 전달 > 정보 "생성" 요청, 보안사항이 있는 데이터의 전달
            * PUT, PATCH : 기존에 저장된 정보 수정 요청
            * DELETE : 저장된 정보 삭제  

* https(Hyper Text Transform Protocol Secure)
    * 기기, 운영체제, 브라우저에 상관없이 통신할 수 있는 방식

        > <span style="color:darkgray">**http를 꼭 알아야 하는 이유!  
    통신방식을 알면 응답값에 대한 파악 가능(4xx, 5xx..)  
    개발자 도구를 통해 http 통신 기록 확인 가능  
    결함 공유 시 오류코드 전달 가능**</span>

    [HTTP 메서드 참고] https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/CONNECT

<br/>

#### htttp 메시지 구조
* Request Message
    * Start Line : 요청 작업의 내용으로 구성
        * HTTP 메서드 / 요청 타겟 / HTTP 버전

    * Header : 요청에 대한 추가 정보 제공
        * Host, User-Agent, Body에 전달되는 Content 정보 등

    * Blank Line

    * Body : HTTP 메서드 작업을 위해 서버에 전달되는 데이터, 주로 POST나 PUT요청에 사용됨

<br/>

* Response Message
    * Status Line : 요청 작업의 결과로 구성
        * HTTP 버전 / 상태코드

            > <span style="color:darkgray">**1xx : Information  
            2xx : Successful  
            3xx : Redirection(사용자가 요청한 url이 아닌 다른 url로 우회)  
            4xx : Clinet Error  
            5xx : Server Error**</span>

    * Header
    * Blank Line
    * Body

<br/>

## Web 통신 구조
: Client - FE - Web 서버 - BE 서버{ WAS(Web Container) - DB 서버 }

* 클라이언트 : 브라우저

* Frontend : 서버 기능과 무관하게 단독적인 기능들의 집합
    * UI/UX 구성
    * 서버에 요청하기 위한 통신 기능 탑재

* Web 서버

* Backend 서버 : 동작코드, 기능의 동작인 비즈니스 로직을 처리하는 부분, WAS와 DB를 포함하며 WAS에는 Web Container가 포함되어 있음

    * 비즈니스 로직 : 입력된 데이터를 저장하기 위해 가공하는 것

* WAS, Web Application Server : 클라이언트와 BE 사이에서 통신을 돕는 서버

* Database 서버 : 데이터베이스 처리를 위한 서버

<br/>

### Frontend
* 구성요소
    * view : UI
    * controller : 데이터 처리, 로직 실행
    * State Management : 애플리케이션 데이터의 상태 관리
    
* 설계 원칙
    * 직관성
    * 일관성
    * 접근성
    * 응답성

<br/>

### Backend
* 구성 요소
    * 애플리케이션 서버
    * DB
    * API

* 개발 언어
    * python : 연구자료가 많음
    * Java : 안정적이고 확장 가능
    * Node.js : 비동기 처리에 강점(Web 개발에 주로 사용됨)
    * Ruby

* 사용 툴  
    * ORM : SQL이 아닌 개발 언어로 어플리케이션과 데이터베이스를 연결 가능하도록 해주는 툴  
        * SQLAlchemy, Django ORM

* Backend 주요 보안 기술
    * SSL/TLS : 데이터 암호화
    * 방화벽 : 네트워크 보안
    * 입력 검증 : SQL Injection 방지

* 성능최적화 방법
    * 인덱스 설정
    * 쿼리 최적화
    * 캐싱
    * 파티셔닝(데이터 분할 관리)

<br/>

### Data Base
* 기본 기능
    * 저장(Insert) : 데이터를 저장하기 위한 규칙을 만듬 > Database Table 생성됨
    * 검색(Select, find)
    * 수정(Update)
    * 삭제(Delete)  
        * Soft Delete : 실제 데이터는 유지하고 삭제 여부에 True 표시를 함  
        * Hard Delete : 데이터 자체를 삭제

    > <span style="color:darkgray">**트랜젝션 : 개발에서는 수정, 삭제, 저장을 뜻함(검색은 미포함)  
    트랜젝션 건다 : 개발에서 롤백을 뜻함**</span>

<br/>

* DB의 구성요소
    * 테이블 : 데이터를 표 형식으로 구성(Row + Column)
    * 스키마(Schema) : DB의 구조 정의
    * 쿼리(Query) : DB에 요청을 하기 위한 명령어, 데이터베이스 정렬 가능

    > <span style="color:darkgray">**데이터 처리 방식  
    클라이언트에서 서버로 요청 > 서버가 DB로 쿼리를 날림 > DB에서 서버로 데이터 전송 > 서버가 클라이언트로 데이터 전송**</span>

<br/>

### DBMS  
: 데이터베이스 관리 소프트웨어  

* 종류   
    * 관계형 데이터베이스  
    : SQL DB라고도 함
    스키마를 지정하여 테이블 간의 관계를 기반으로 데이터 관리  
    Primary key를 활용해 데이터 테이블 연결  
    일관성 유지에 좋음  
    보안/금융 데이터 관리에 사용
        * 데이터 모델링
        : 관계형 db에서 데이터베이스 구조를 어떻게 연결할 것인지 설계하는 과정
        데이터 중복 최소화, 명확한 관계 정의, 확장성 확보가 핵심 원칙

        * 정규화
        : 테이블간 데이터를 분리하여 중복 최소화

        * 비정규화
        : 성능 향상을 위해 데이터 중복을 허용, 정규화 데이터를 일부 통합

    * 비 관계형 데이터베이스  
    : NoSQL이라고도 함  
    정형화되지 않아 확장성이 좋음  
    AI나 비정형 데이터(가공되지 않은 데이터) 처리에 유리
        * key-value DB : 속도 빠름  
        * document DB : json의 확장 버전  
        * Graph DB : 노드의 속성별로 데이터 저장, 추천광고 등에 사용

<br/>

## Web 데이터 통신 방법  
: Client - FE - Web 서버 - BE 서버{ WAS(Web Container) - DB 서버 } 

1. 클라이언트의 데이터 요청(정적 + 동적)
2. Web 서버 : 정적 리소스 처리(애플리케이션 서버에 요청 없이 데이터 처리)
3. WAS : 웹서버로부터 동적 요청을 전달 받아 Web Container가 동적 리소스 처리
4. Backend 서버 : 로직 처리
5. DB 서버 : Backend에서 요청받은 데이터 전달

<br/>

## Web 구성
* HTML, HyperText Markup Language  
    * 웹페이지의 구조화를 위한 마크업 언어(텍스트를 붙이는 언어)
    * 태그를 이용하여 요소를 표시하고 구성함

        > <span style="color:darkgray">**http : html 전송을 위한 프로토콜  
        HyperText : 웹사이트에서 링크를 통해 다른 사이트로 즉시 이동하는 기능  
        Markup : 태그를 사용해 문서에 의미를 표시하는 것**
        </span>

* CSS, Cascading Style Sheet  
: 웹 페이지 디자인을 위한 언어  
    > <span style="color:darkgray">**Selenium에서 요소를 식별할 떄 CSS Selector 사용**</span>

    * Bootstrap  
    : CSS 라이브러리

* JS, JavaScript
: 웹페이지의 동적 요소 추가를 위한 언어

<br/>

# HTML
## HTML 구조
* DOCTYPE
* html
* head
* body

예시 코드
```html
<!DOCTYPE html> // html5 문서임을 선언
<html lang="en">
    <head>
        <meta charset="UTF-8">  // 인코딩 형식
        <title>Document</title> // 웹페이지 제목
    </head>
    <body>
    // 웹 페이지의 실제 내용 작성
    </body>
</html>
```

<br/>

## HTML 태그
### 기본 문법
```html  
<태그 속성="속성값">콘텐츠</태그>
```

* self-closing tags  
: 닫는 태그가 필요하지 않은 태그

    self-closing tags 예시
    ````html
    <br/> : 줄바꿈
    <input/> : 입력창
    <img/> : 이미지 삽입
    ````
    <!-- img태그 사용 예시
    ```html
    <img src="url또는 파일 경로" alt="대체텍스트"/>
    ``` -->

* 컨테이너  
: 요소를 묶어서 레이아웃 구조화

    * Block 수준의 컨테이너 요소  
    : 줄바꿈을 통해 행 단위로 스타일 적용 가능  

        Block element 예시  
        ````html
        <div></div> : 행바꿈
        ````

    * Inline 수준의 컨테이너 요소  
    : 줄바꿈 없이 일부 텍스트만 스타일 적용 가능  

        Inline element 예시 
        ````html
        <span></span>
        ````    

<br/>

### 자주 사용하는 태그
* h 태그  
    ````html
    <h1></h1>
    ````
    예제
    ````
    <h1>제목 태그</h1>
    <h2>제목 태그</h2>
    <h3>제목 태그</h3>
    <h4>제목 태그</h4>
    <h5>제목 태그</h5>
    <h6>제목 태그</h6>
    ````
    출력
    <h1>제목 태그</h1>
    <h2>제목 태그</h2>
    <h3>제목 태그</h3>
    <h4>제목 태그</h4>
    <h5>제목 태그</h5>
    <h6>제목 태그</h6>

<br/>

* p 태그  
    ````html
    <p></p>
    ````
    예제
    ````html
    <p>내용1</p>
    <p>내용2</p>
    ````
    출력  
    <p>내용1</p>
    <p>내용2</p>

<br/>

* a 태그  
    ````html
    <a href="url" target="속성값에 따라 현재 탭/새 탭에서 실행">텍스트</a>
    ````
    * target 속성값  
    _blank : 새로운 탭에서 열기  
    _self : 현재 탭에서 열기(default)

    예제
    ````html
    <a href="https://www.naver.com/" target="">현재 탭에서 네이버 열기</a>  
    <a href="https://www.naver.com/" target="_blank_">새 탭에서 네이버 열기</a>
    ````
    출력  
    <a href="https://www.naver.com/" target="">현재 탭에서 네이버 열기</a>  
    <a href="https://www.naver.com/" target="_blank_">새 탭에서 네이버 열기</a>

<br/>

* 목록 태그와 요소  
    ````html
    <ul></ul> : Unoldered List
    <ol></ol> : Oldered List
    <li></li> : List
    ````
    예제
    ````html
    <ul>
    <li>item</li>
    <li>item</li>
    </ul>

    <ol>
    <li>item</li>
    <li>item</li>
    </ol>

    ````
    출력
    <ul>
    <li>item</li>
    <li>item</li>
    </ul>
    
    <ol>
    <li>item</li>
    <li>item</li>
    </ol>

<br/>

* table 태그와 요소
    ````
    <table></table> : Table 생성
        * 속성
        border : 테두리 선 굵기

    <tr></tr> : Table Row
    <th></th> : Table Header
    <td></td> : Table Data
    ````
    > <span style="color:darkgray">**테이블 생성 : CSS를 이용하는 것보다 간단함  
    테두리 등 속성 설정 : 주로 CSS 이용**</span>

    예제
    ````html
    <table border="1">
        <tr>
            <th>속성1</th>
            <th>속성2</th>
        </tr>
        <tr>
            <td>값1</td>
            <td>값2</td>
        </tr>
    </table>
    ````
    출력
    <table border="1">
        <tr>
            <th>속성1</th>
            <th>속성2</th>
        </tr>
        <tr>
            <td>값1</td>
            <td>값2</td>
        </tr>
    </table>

<br/>

* form 태그와 요소
    ````html
    <form></form> : form 생성
        * 속성
            method : 서버로 데이터를 전송하기 위한 메서드, (default : GET)
                GET : 주소 표시줄에 사용자 입력한 데이터 포함
                    동적 웹서비스에서 특정한 페이지를 식별하는 고유 주소로 사용
                POST : 주소 표시줄에 사용자 입력 데이터 비노출

            name : 한 문서 내에 form 태그가 여러개 사용될 수 있음.
                이를 위해 form 구분을 위한 키(key)로 사용됨.

            action : 데이터를 전송할 서버와 연결되는 주소(URL, script 파일명 등)
                form 태그에서 입력받은 값을 전달할 경로는 action 속성에 입력한다. 

    <label></label> : 요소에 레이블(라벨) 지정
        * 속성
        for : 입력 요소의 id값

    <input/> : 한 줄 입력 가능한 입력필드
        * 속성
            type : text, url, radio, submit 등

            name : input 구분을 위한 Key
                   input 태그에서 입력받은 값을 서버로 받아오면 name 속성에 저장된다.

            placeholder : 입력값 예시            

    <textarea></textarea> : 여러 줄 입력 가능한 입력필드
        * 속성
        name : textarea 구분을 위한 Key
        placeholder : 입력값 예시
        clos : 행 크기 제어
        rows : 열 크기 제어
    ````

    > <span style="color:darkgray">**form 태그는 다른 언어와 연동하여 사용(js, React SPL)  
    label 태그가 입력 요소와 연결될 경우 입력 요소 활성화됨**</span>

    예제
    ````html
    <form>
        <label for="inputId">input:</label>
        <input
        type="text"
        id="inputId"
        name="text1"
        placeholder="텍스트를 입력해 주세요."
        />
        <br/><br/>
        <label>textarea:</label>
        <textarea
            name="content"
            placeholder="텍스트를 입력해 주세요."
            cols="20"
            rows="5"
        ></textarea>
    </form>
    ````
    출력
    <form>
        <label for="inputId">input:</label>
        <input
        type="text"
        id="inputId"
        name="text1"
        placeholder="텍스트를 입력해 주세요."
        />
        <br/><br/>
        <label>textarea:</label>
        <textarea
            name="content"
            placeholder="텍스트를 입력해 주세요."
            cols="20"
            rows="5"
        ></textarea>
    </form>

<br/>

* Semantic 태그  
: 컨테이너 태그이지만 각 요소의 역할과 의미를 예측 가능하도록 하는 태그  
SW 완성도와 관련됨  
검색엔진 최적화(SEO, Search Engine Potimization)를 위해 사용

    ````html
    <header></header>
    <nav></nav> : 내비게이션 링크
    <section></section> : 구역 분할
    <main></main>
    <aside></aside>
    <article></article> : 문서 내 독립적인 콘텐츠
    <footer></footer>
    ````

    > <span style="color:darkgray">**semantic을 사용하지 않으면 div 태그로 레이아웃 구현 가능**</span>

<br/>

## 선택자(Selector)
* 전역 속성   
: 모든 html에서 사용할 수 있는 공통 속성

* 선택자  
: CSS로 속성을 부여할 대상을 뜻함
    * id
    : 고유 식별자로 요소 식별을 위해 사용

    * class
    : 여러 요소에 동일한 스타일 적용을 위해 동일한 클래스 할당  
    다중 할당 시 공백으로 구분 

* 선택자 이름 입력 규칙
    * 대소문자 구분
    * 공백, 특수문자 포함 불가
    * 숫자나 문자로 시작, 숫자로만 이루어질 수 없음 

    사용 예시
    ```html
    <head>
        <style>
            /* class 선택자 */
            .class1{    

            }
            /* class 선택자 */
            .class2{

            }
            /* id 선택자 */
            #id1{

            }
        </style>
    </head>
    <body>
        <div class="class1 class2">요소 1</div>
        <div class="class1">요소 2</div>
        <div id="id1">요소 3</div>
    </body>
    ```

<br/>

# SW 아키텍처
: 시스템의 구성 요소와 각 요소간의 관계/상호작용을 정의하는 구조

## 유형
* 모놀리식 아키텍처  
: 모든 기능이 하나의 단일 시스템으로 구성  
테스트 진행 시 타깃은 하나

* 마이크로서비스 아키텍처  
: 각 서비스가 독립적인 기능으로 나누어진 구조  
테스트 진행 시 타깃은 여러개

## 주요 구성 요소
* Frontend
    * 사용자 인터페이스 제공
    * 사용자 입력 처리 및 시각적인 콘텐츠 출력
    * API 호출을 통해 BE와 데이터 통신
    
* API
    * 외부에서 만들어둔 기능
    * 네트워크, 통신을 통해 기능 제공
    * 코드 집합으로 재사용 가능

* Backend
    * 비즈니스 로직 처리 및 데이터 연산
    * 인증, 보안 관리
    * API 응답 생성

* Network
    * 데이터가 클라이언트와 서버 간에 이동하는 경로 관리    
    * 데이터 전송 프로토콜 : TCP/IP, UDT, HTTP/HTTPS

* Database
    * 데이터 저장
    * 중복 데이터 방지 및 일관성 유지
    
    > <span style="color:darkgray">**DB 설계 원칙  
    1.정규화 : 중복 데이터를 최소화하여 데이터 무결성 확보  
    2.인덱스 최적화 : 색인 속도를 높이기 위한 인덱스 설정  
    3.보안 : 암호화 및 접근 권환 관리**</span>

<br/>

### API(Application Programming Interface)
: SW간 상호작용을 가능하게 하는 인터페이스

* 특징  
    * 시스템 간 통신 및 데이터 교환 간소화  
    * 개발 효율 및 재사용성 향상

* 종류
    * REST API
    : url을 통해 통신하는 API

    * SOAP API(Simple Object Access Protocol)  
        * 마이크로서비스 아키텍처(분산 환경)에서 xml 데이터를 기준으로 통신하는 API 구조
        * 명확한 계약(WSDL)을 통한 명세 정의
        * 금융 시스템, ERP등 높은 보안 및 신뢰성을 요구하는 시스템에 사용됨

    * GraphQL API  
        * 클라이언트가 GrahpQA 쿼리로 원하는 데이터를 요청하고, 서버는 json 형식의 데이터를 반환하는 API 구조(클라이언트 중심)
        * 주로 HTTP / HTTPS 프로토콜 사용
        * 모바일 앱, 실시간 데이터 업데이트 등 데이터 효율이 중요한 시스템에 사용됨

<br/>

#### REST API(REpresentational State Transfer API)
: 대표 상태 전달, 리소스를 URL로 표현하고, HTTP 메서드를 이용해 리소스를 조작하는 방식

* REST : 분산 하이퍼미디어 시스템을 위한 아키텍쳐 스타일(제약조건의 집합)

* REST 핵심 원칙(제약조건) 6가지
    1. 클라이언트-서버 구조(Client-Server)  
    : 클라이언트와 서버의 명확한 역할 구분(Client - 사용자 인터페이스, Server - 데이터 로직)

    2. Stateless(무상태성)
    : 클라이언트의 각 요청을 독립적으로 처리, 이전 요청의 상태(세션)를 서버에 저장하지 않음

    3. Cacheable  
    : 응답에 캐시 가능 여부를 명시하여 클라이언트나 중간서버에 캐싱할 수 있어야 함
        e.g.
        ```
        Cache-Control: max-age=3600 // 3600초(1시간)동안 캐시 가능
        Cache-Control: no-store // 캐시 불가능
        ```

    4. Layered System  
    : 중간 서버의 구조 계층화로 역할을 명확하게 분리, 클라이언트는 계층의 존재를 모른채 동작 가능해야 함
    
    5. Uniform Interface : 효율적인 아키텍처를 위해 일관된 인터페이스를 가지고 있음  
        * 자원의 식별(Resource Identification) : URI를 통해 자원을 고유하게 식별 가능해야 함
            * URI를 통해 요청의 "위치"만 포함되어야 함, 작업의 형태는 http 메서드로 전달
            * URI는 명사 위주로 사용  
            e.g.
            ````
            URI : https://qatrack.elice.io/courses/724447/lectures/6460513/lecturepages/52977675
            courses id : 724447
            lectures no. : 6460513
            lecturepages : 52977675
            ````

        * 자원의 표현(Representation) : 자원의 상태를 JSON, XML 등으로 전달
            e.g.
            ```
            // API Response
            {       
            "id": 123,
            "name": "kim",
            "email": "kim@example.com",
            "created_at": "2024-06-10T15:30:00Z",
            "links": {
                "self": "/users/123",
                "orders": "/users/123/orders"
                }
            }
            ```

        * 메시지의 자기 설명성(Self-descriptive Messages) : 
            e.g.
            ```
            // API Response
            HTTP/1.1 200 OK
            Content-Type: application/json  << type이 있어야 데이터 파싱 가능
            Cache-Control: max-age=600
            ```

        * HATEOAS : 클라이언트가 API를 탐색할 수 있도록 API 응답 시 사용 가능한 기능들의 링크를 함께 제공, 메세지를 통한 상태 전이가 가능해야 함

    6. Code-On-Demand  
    : 클라이언트에서 실행할 수 있는 코드를 서버가 전송할 수 있어야 함(js)

* REST API
: REST 원칙을 기반으로 만들어졌으나, 부분적으로 REST 원칙이 적용된 api

* RESTful API(REST API, Representational State Transfer)
: 상태 정보 전송의 원칙을 잘 준수하는 API, End Point를 기준으로 통신을 함

> <span style="color:darkgray">**Endpoint : 웹서버의 주소를 가르키는 문자  
REST API는 HTTP 메서드, End Point 세팅을 통해 테스트 가능**</span>

<!-- * 특징
    * HTTP 프로토콜을 기반으로 설계, HTTP 메서드 사용
    * Stateless : 클라이언트의 요청을 저장하지 않음(무상태성, 상태 저장 X)
    * Idempotent : 클라이언트가 동일한 요청 시 동일한 응답 전송(멱등성)
    * Cacheability : 클라이언트가 응답을 캐싱할 수 있음 -->

> <span style="color:darkgray">**API vs REST API  
    API : 통신 규약  
    RESTful API : 요청과 응답 형식까지 지정한 통신 규약  
    <br/>
    .xsd  
    : .xml 파일의 규칙을 정리한 파일 형식  
    코드 검증 시 xsd 파일 사용 가능  
    웹에서 'xml, xsd'로 검색하면 xml을 xsd로 변환하는 사이트가 나온다.**</span>

* RESTful API의 구성
: HTTP Method + Endpoint(어떠한 기능을 만드는지에 대한 정의가 있는 부분)

    * http 메서드
        * POST : Create
        * PUT : Update(전체)
        * PATCH : Update(부분)
        * DELETE
        * GET : Read

    * Endpoint
    : /DataTable의 이름/DataTable의 ID값
        * ID값은 숫자 외에도 랜덤문자일수도 있음

* RESTfun API에서 사용되는 엔트포인트의 구성 방식
    * Base Endpoint(기본 엔드포인트, Collection Resource URI)  
    : 특정 리소스의 전체 목록에 접근할 때 사용

        ```
        /example
        ```

    * Path Parameter(경로 매개변수) 사용 엔드포인트
    : 개별 리소스 접근용 엔드포인트

        ```
        /products/1
        -> 1 : DataTable의 ID값(파라미터값)
        ```

    * Query Parameter(쿼리 매개변수) 사용 엔드포인트
    : URL의 ? 뒤에 오는 key=value 형태의 파라미터, body값이 아닌 url로 데이터를 제공할때 사용
    데이터 필터링, 정렬, 페이지네이션 등에 주로 사용됨

        ```
        /example?sort="created"&order="DESC"
        해석 : example?생성 날짜 기준 정렬&최신순 정렬
        ```

<br/>

#### API 인증 방식
* API Key : 단순 문자열로 인증
* Basic 인증 : 사용자 이름과 비밀번호로 인증
* JWT(Jwon Web Tocken) : 클라이언트와 서버가 통신할 때 토큰을 통해 인증상태 유지
* Oauth 2.0 : 액세스 토큰을 통해 인증과 권한 분리

> <span style="color:darkgray">**로그인 상태를 유지하는 것이 중요함  
따라서 인증/인가 방식을 잘 정하는 것이 중요**</span>

<br/>

#### 세션 인증 방식
1. 웹 브라우저에서 로그인 성공
2. 서버에서 세션을 생성한 후 일부를 웹 브라우저, 나머지는 서버의 Memory/HDD/DB에 저장
3. 웹 브라우저는 전달받는 세션의 일부를 쿠키에 Session ID로 저장
4. 이후 웹 브라우저가 로그인 상태를 유지한 채로 다른 동작 요청(Request)시, Session ID를 함께 전송
5. 서버는 Session ID를 비교하여 로그인 상태 확인

> <span style="color:darkgray">**쿠키  
: 클라이언트에 저장되는 사용자 데이터  
-세션 쿠키 : 브라우저 종료 시 데이터 삭제(임시 로그인)  
-영구 쿠키 : 만료기간 설정, 브라우저 종료 후에도 데이터 유지(자동 로그인)  
<br/>
세션  
브라우저에서의 세션 : 세션 스토리지, 브라우저 종료 시 데이터 삭제
서버에서의 세션 : 서버가 사용자의 상태를 저장하는 임시 공간**</span>

> <span style="color:darkgray">**쿠키가 만료되면,  
Application > Storage > Cookies에서 세션 쿠키가 사라진다.**</span>
<br/>

#### 토큰 인증 방식
1. 웹 브라우저에서 로그인 성공
2. 서버에서 header, payload, verify signature를 암호화하여 토큰 생성한 후 웹 브라우저로 전송
3. 웹 브라우저는 토큰을 저장하고, 서버는 토큰 정보가 없는 상태가 됨
4. 이후 웹 브라우저의 데이터 요청 시, 서버로 토큰 정보 전송
5. 서버는 서버에 저장되어 있는 비밀키를 사용하여 header, payload 복호화 및 verify signature과 일치하는지 확인
6. verify signature와 일치하고 유효기간이 남아있으면 서버가 데이터 전송

<br/>

* 헤더 : Type + alg을 담고 있음
    * Type : JWT(고정값)
    * alg : verify signature을 만들기 위한 암호화 알고리즘 저장

* 페이로드 : 토큰에서 사용할 정보의 조각들인 클레임(Claim)을 담고 있음

* verify signature : 암호화 알고리즘값을 담고 있음

<br/>

> <span style="color:darkgray">**세션 인증 vs 토큰 인증  
세션 인증 : stateful, 시간에 따라 바뀌는 상태값 존재  
토큰 인증 : stateless, 시간에 따라 바뀌는 상태값이 없음**</span>

> <span style="color:darkgray">**Access 토큰 : 만료 시간을 짧게 설정, 매번 인가를 받기 위해 사용  
Refresh 토큰 : 만료 시간을 길게 설정, 액세스 토큰이 유효한지 확인을 위한 토큰**</span>

<br/>

## SW 아키텍처 패턴
### 클라이언트-서버
: 서버가 중앙에서 데이터를 관리, 클라이언트는 요청하는 구조

* 클라이언트  
    * 서버에 요청을 보내고 응답을 받아 사용자와 상호작용하는 장치 또는 애플리케이션  
    (서버에 접근하는 모든 장치 또는 애플리케이션)  
        e.g.  
        ````
        게임 구동 프로그램
        웹 브라우저
        모바일 클라이언트
        ````
    * REST API 또는 GraphQL로 서버와 통신  

    * 클라이언트는 서버에 의존적이며, 처리 능력이 제한됨

    * 웹 클라이언트와 모바일 클라이언트로 구분  
        * 웹 클라이언트 : HTML, CSS, JavaScript로 구성된 브라우저 기반의 애플리케이션
        * 모바일 클라이언트 : Android, iOS 기반의 네이티브 앱

    * 기술 스택 : React, Angular, Vue.js

<br/>

* 서버  
: 웹 서버, 애플리케이션 서버, 데이터베이스 서버로 구성
    * Web 서버
        * 정적 리소스 처리
        * 리버스 프록시(보안)
        * 로드밸런싱
        * Apache, NGINX, IIS(windows)로 구현

            > <span style="color:darkgray">**프록시 서버(Proxy Server)  
            : 포트 스캐닝(port scanning)을 방지하기 위해 현재 활성화된 노드 번호를 숨기고 서버와 클라이언트 사이를 중계  
            <br/>
            로드밸런싱(Load Balancing)  
            : 여러 요청이 있을 때 끊김 없는 서비스 제공(지속성)을 위해 was를 여러개 배치함.  
            이때 사용 가능한 WAS를 Web Server에 매칭해주는 스위치(트래픽 분배 도구)**</span>

    * WAS(Web Application Server)
        * 웹 애플리케이션을 실행시켜 필요한 기능을 수행하고 결과를 웹 서버에게 전달하는 일종의 미들웨어
        * 로직이나 데이터베이스와의 연동을 하기 위한 일련의 처리 업무 담당
        * nodeJS, django로 구현

    * DB 서버
        * 데이터를 저장하고 조회
        * mongoDB, MySQL로 구현

    * Backend 서버
        * 클라이언트의 요청을 처리하고 데이터 연산 및 DB에 데이터를 저장하는 중앙 컴퓨터 또는 시스템
        * WAS와 DB를 포함함

    > <span style="color:darkgray">**웹 통신 방법  
    Client - FE - Web 서버 - BE 서버{ WAS(Web Container) - DB 서버 }**</span>

<br/>

* 클라이언트-서버 모델의 확장성
    * 수직 확장 : 서버 HW 성능 업그레이드
    * 수평 확장 : 서버를 추가하여 부하 분산

    
* 클라이언트-서버 모델의 통신 방식
    * 동기(Synchronous) : 요청 시 응답이 와야 다음 요청 진행
    * 비동기(Asynchronous) : 요청 후 응답을 기다리지 않고 다음 작업 수행

* 클라이언트-서버 모델의 데이터 통신 보안
    * SSL/TLS를 사용한 데이터 암호화
    * 인증토큰(JWT, OAuth)

* 클라이언트-서버 모델의 데이터 통신 최적화
    * 데이터 압축(GZIP)으로 네트워크 패킷 감소
    * CDBN으로 데이터 전송 속도 향상
    * 캐싱을 통해 반복 요청 최소화
        * Redis : 데이터 캐싱 및 세션 관리에 최적화 된 고성능 키-값 저장소
<br/>

## 소프트웨어 아키텍처 계층
: SW를 구성하는 계층적인 구조

* 프레젠테이션 계층(Presentation Layer)  
: UI와 관련된 계층 (Vue, React, HTML, API Controller 등)  
사용자 입력을 받고 비즈니스 로직 계층으로 전달

* 비즈니스 로직 계층(Business Logic Layer)  
: 애플리케이션의 핵심 로직을 처리  
데이터 처리 규칙을 정의

* 리포지토리 계층(Repository Layer)  
: 데이터베이스와의 상호작용을 담당