# 단위테스트 절차
1. 환경 설정
2. 테스트 코드 작성
3. 테스트 실행

</br>

## 환경 설정 - 가상 환경
* 가상환경
    * 가상환경은 OS 호환이 되지 않는다.
    * Python에서는 버전에 따라 lib/pkg 충돌이 있을 수 있다. 따라서 가상환경을 통해 컨테이너화 하면, 프로젝트마다 충돌을 방지할 수 있다.

    > <span style="color:darkgray">**Python 이외의 다른 언어는 src > package.json을 활용해 일정한 환경을 유지할 수 있다.**</span>

</br>

* 가상환경 생성 : python -m venv venv

</br>

* 가상환경 활성화
    * Windows : venv\Scripts\activate
    * Mac/Linux : source venv/bin/activate

</br>

## 단위테스트 프레임워크
* unittest
    * 내장 라이브러리
    * 클래스 기반 테스트
    * 정형화된 메서드명 사용

</br>

* pytest  
: 확장성이 좋음, unittest 치환 가능
    * 외부 라이브러리
    * 함수 기반 테스트
    * 모듈명, 클래스명, 함수명이 'test_'로 시작
    * Fixture 기능 제공
    : DB Set 등 테스트를 위해 필요한 자원을 미리 준비 가능


</br>

### unittest
* Unittest 실행 기본 패턴  
: setUp() - 테스트 메서드 실행 - tearDown()

</br>

* Unittest 기본 구성 요소
    * Test Suit : 테스트 파일
    * Test Case : Class
    * Test Step : Method
    * Test Runner : 테스트 실행 및 결과 출력 도구
    * Assertions : 테스트 검증을 위한 명령

</br>

* Unittest 클래스의 주요 메서드
    * setUp() : 각 테스트 메서드 실행 전 사전작업 수행(셀레니움 url, 쿠키 정보 등)
    * tearDown() : 테스트 후 정리 작업, setUp()에서 불러왔던 데이터가 자동으로 삭제됨
    * setUpClass() : 클래스 시작 시 1회 실행
    * tearDownClass() : 클래스 시작 시 1회 실행

</br>

* assert 메서드
    * assertEqual() : 값이 같은지 확인
        ```python
        self.assertEqual(a, b)
        ```
    * assertNotEqual()
    * assertTrue() : 조건이 참인지 확인
    * assertIsNone() : 값이 None인지 확인
    * assertRaises() : 특정 예외 상황이 동작하는지 확인
        ```python
        # add.py
        def add(a, b):
            if a < 0 or b < 0:
                raise ValueError
            return a + b

        # test_01.py
        with self.assertRaises(ValueError): # 예상되는 예외 입력
            add(1, b)   # 에러를 유발하는 코드

        # test_01.py
        self.assertRaises(ValueError)
        ```
    * assertRaisesRegex(): 특정 예외 상황과 예외 메세지 검증
        ```python
        # add.py
        def add(a, b):
            if a < 0 or b < 0:
                raise ValueError("양수만 입력 가능합니다.")
            return a + b

        # test_01.py
        with self.assertRaises(ValueError, "양수만 입력 가능합니다."): # 예상되는 예외 입력, 예의 메세지
            add(1, b)   # 에러를 유발하는 코드
        ```

</br>

* Unittest 데코레이터  
: 특정 클래스나 함수에 추가적인 기능을 부여(기능 확장)하기 위해 사용
    * skip
        ```python
        @unittest.skip('이 테스트 스텝은 넘어갑니다.') # 결과 출력 's'
        @unittest.skipif(condition, 특정 조건)    # 특정 조건일 때 skip
        @unittest.skipUnless(condition, 특정 조건)  # 특정 조건일 때 run
        @unittest.expectedFailure # 결과 출력 'x'
        ```
    * TextTestRunner : 테스트 결과 커스터마이징
<br>

* 실행 명령어  
    ```
    python -m unittest discover 차상위디렉터리**<span>
    ```
</br>

* 리포트 생성
    * xml 리포트용 라이브러리 설치 : pip install unittest -xml -reporting
        ```python
        from xmlrunner import XMLTestRunner

        unittest.main(testRunner=XMLTestRunner(output=output))
        ```
    
        ```python
        from HtmlTestrunner import XMLTestRunner

        unittest.main(testRunner=HtmlTestRunner(output=output))
        ```

<br/>

### pytest
* 파일 구성
    * conftest.py : fixture, Hook 함수등을 작성한 파일, 다른 모듈에서 별도의 import 없이 사용 가능

    * __init__.py : 파일을 패키지로 인식하도록 함, pytest 실행 시 참조하는 테스트 환경 설정 파일

        ```python
        markers = api # 사용할 마크 지정
        addopts = -v -s   # 기본 실행 옵션 설정
        testpaths = tests # 기본 테스트 경로 지정
        filterwarnings = ImportWarning    # 경고 필터링 설정
        log_cli = f"%Y-%m-%d %h:%m:%s - {message}"    # 로그 출력 설정
        ```

    * pytest.ini : 테스트 경로, 마커설정(이름과 설명) 등 Warning 메세지 방지를 위해 pytest 실행 시 적용할 옵션 정의
    
    * requirements.txt : Pytest 관련 설치 파일을 작성한 파일(의존성 패키지 목록)

</br>

* pytest 실행 기본 패턴
: fixture(setUp)/Mocking - 테스트 메서드 실행 - fixture(tearDown)

    > <span style="color:darkgray">**float 형식 숫자 계산 검증 시, pytest.approx()를 사용한다.**</span>

</br>

#### pytest 데코레이터
* @pytest.fixture() : 여러 테스트 파일에서 공통으로 사용하는 데이터나 환경 설정 코드 작성
    ```python
    #conftest.py
    @pytest.fixture(scope="function", autouse=True)
    # scope : 실행 범위(주기)
    # autouse : 테스트 함수에서 호출하지 않아도 fixture 자동 실행

    def name():
        setUp 코드  # fixture 코드 실행
        yield   # fixture 실행 정지, 객체를 테스트 함수에 전달
        tearDown 코드   # 테스트 코드 실행 후 이어서 실행됨

    def base_url():
        return "https://..."

    def driver():
        ...

    def hook():
        ...
    ```
    
    * scope 종류
        * function : 기본값, 각 테스트케이스마다 실행
        * class : 테스트 클래스(Test suit)마다 실행
        * module : 모듈단위로 실행
        * session : 전체 데스트 실행 중 한번만 실행

* @pytest.skip(reason="미완성 기능") : 결과 출력 's'
* @pytest.skipif(condition=True, reason="미완성 기능") : 특정 조건일 때 skip

* @pytest.mark.name : 특정 테스트만 실행
    ```python
    # test_01.py
    @pytest.mark.slow
    def test_losw_tesk():
        pass

    @pytest.mark.smoke
    def test_smoke_tesk():
        pass
    ...
    ```
    ```
    pytest -m slow : 오래 걸리는 성능테스트만 실행
    pytest -m smoke : 기본 기능 확인용 빠른 테스트
    pytest -m api : api 호출 관련 테스트
    pytest -m db : db연동 테스트
    pytest -m regression : 리그레션 테스트
    ```
        
* @pytest.mark.parametrize("인자 문자열", 리스트) : 테스트 함수에 여러 개의 입력값을 제공하여 동일한 테스트를 반복 실행
    ```python
    params = [(1, 1), (2, 1), ("땡", ValueError)]

    @pytest.mark.parameterize("a, expected", params)
    def test_name(a):
        assert a == expected
    ```
* @pytest.mark.xfail(reason="버그 수정 전") : 예상대로 실패시 Pass(XFAIL), 성공시 fail(XPASS)
* @pytest.mark.xfail(condition=True, reason="버그 수정 전") : condition 값이 True일 때만 xfail 적용됨

</br>

#### 로그 설정
* basic config  
: 한 번에 기본적인 로깅 설정 가능

    ```py
    # log_handler.py
    import logging

    @pytest.fixture(scope="session", autouse=True)
    def configure_logging():
        logging.basicConfig(
            filename="test_result.log",  # 로그 파일 경로
            level=logging.INFO,  # 로그 레벨 설정
            format="%(asctime)s - %(levelname) - %(message)s",  # 로그 포맷 지정
            encoding="utf-8"  # ✅ UTF-8 인코딩 적용
        )
    ```

    ```py
    # test.py
    import logging

    class Test():
        logger = logging.getLogger()

        def test_example(self):
            self.logger.info("테스트 시작")

            try:
                ...
                
            except Exception:
                self.logger.warning("UI 요소 변경됨")
                self.logger.error("오류 발생", exc_info=True)   # exc_info : stateless 사용 여부(stateless : 에러가 나면 터미널에 어떤 에러가 떴는지 파이썬 자체 메세지 출력)
                self.logger.exception("예외상황 발생")

            finally:
                self.logger.info("테스트 종료")
    ```

* log handler  
: 여러 개의 핸들러(콘솔, 파일, 네트워크 등)를 원하는 대로 추가/제어할 수 있음

    ```py
    import logging
    from logging.handlers import RotatingFileHandler
    from logging.handlers import TimedRotatingFileHandler

    @pytest.fixture(scope="session", autouse=True)
    def configure_logging():
        # 기본 로거 설정
        logger = logging.getLogger()    # 로거 객체 생성
        logger.setLevel(logging.DEBUG)  # 로거 자체의 최소 레벨 지정
        formatter = logging.Formatter("%(asctime)s - %(levelname)s - %(message)s")

        # 스트림 핸들러 설정
        stream_handler = logging.StreamHandler()    # 로그 메시지를 스트림(콘솔, 터미널 등)에 출력하는 스트림 핸들러 객체 생성
        stream_handler.setLevel(logging.INFO)       # 스트림에 INFO 이상 메세지 출력
        stream_handler.setFormatter(formatter)      # 출력할 메세지의 포멧 지정
        logger.addHandler(stream_handler)           # 로거에 스트림 핸들러 연결
        
        # 파일 핸들러 설정
        file_handler = logging.FileHandler("test.log", mode="a")    # 파일 핸들러 객체 생성
        file_handler.setLevel(logging.DEBUG)    # test.log 파일에 DEBUG 이상 메세지 출력 
        file_handler.setFormatter(formatter)    # 출력할 메세지의 포멧 지정
        logger.addHandler(file_handler)         # 로거에 파일 핸들러 연결

        # 용량 기반 로테이팅 핸들러 설정
        rotating_handler = RotatingFileHandler(
            "logfile.log",                  # 기본 파일명
            maxBytes=1024 * 1024 * 5,       # 5MB 넘으면 새 파일로 교체
            backupCount=3                   # 최대 3개까지 백업 (logfile.log.1, logfile.log.2, ...)
        )
        rotating_handler.setFormatter(formatter)    # 출력할 메세지의 포멧 지정
        logger.addHandler(rotating_handler)         # 로거에 로테이팅 핸들러 연결

        # 시간 기반 로테이팅 핸들러 설정
        timed_handler = TimedRotatingFileHandler(
            "timed_logfile.log",    # 기본 파일명
            when="midnight",        # 변경 주기 ("S", "M", "H", "D", "midnight", "W0~W6")
            interval=1,             # 1일마다 회전
            backupCount=7,          # 최근 7일치만 유지
            encoding="utf-8"
        )
        timed_handler.setFormatter(formatter)   # 출력할 메세지의 포멧 지정
        logger.addHandler(timed_handler)        # 로거에 로테이팅 핸들러 연결
    ```

    ```py
    # test.py
    import logging

    class Test():
        logger = logging.getLogger()

        def test_example(self):
            self.logger.info("테스트 시작")

            try:
                ...

            except Exception:
                self.logger.warning("UI 요소 변경됨")
                self.logger.error("오류 발생", exc_info=True)   # exc_info : stateless 사용 여부(stateless : 에러가 나면 터미널에 어떤 에러가 떴는지 파이썬 자체 메세지 출력)
                self.logger.exception("예외상황 발생")
                
            finally:
                self.logger.info("테스트 종료")
    ```

</br>

* assert 메서드
    ```python
    # add.py
    def add(a, b):
        if a < 0 or b < 0:
            raise ValueError("양수만 입력 가능합니다.")
        return a + b

    # test_01.py
    with pytest.raises(ValueError, match="양수만 입력 가능합니다."): # 예상되는 예외 입력, 예dhl 메세지
        add(1, b)   # 에러를 유발하는 코드
    ```

</br>

* 실행 명령어  
```
pytest 차상위디렉터리/파일명.py::특정함수 옵션/플러그인
```

</br>

* 실행 옵션('pytest --help'로 조회 가능)
    * -v : verbose, 자세한 결과 출력
    * -m 마커명: mark, 특정 마크(@pytest.mark) 지정 테스트만 실행
    * -q : quiet, 간략한 결과 출력
    * -x : 첫 번째 실패 시 즉시 종료
    * --html=파일명 : html 리포트 저장(pytest-html 필요)
    * --maxfail=N : N개 실패 시 실행 종료
    * -k "키워드" : keyword, '@pytest.mark'가 붙은 테스트만 실행
    * -s : print()도 터미널에 출력

</br>

* 플러그인
    * pytest-html : 결과를 html 리포트로 저장
        * --self-contained-html : css, js 등을 html 파일 하나에 포함시켜 단일 파일로 생성
        * --title="Report Title" : 리포트 제목 변경
        ```
        pip install pytest-html

        pytest tests/unit/ -v --html=report.html --self-contained-html
        ```
    * pytest-cov : 코드 커버리지 분석 및 리포트 생성
        ```
        pip install pytest-cov
        
        pytest tests/unit/ --cov=src    # src 디렉터리의 코드 커버리지 측정
        pytest tests/unit/ --cov=src --cov-report=html  # src 디렉터리의 코드 커버리지 측정 후 html로 리포트 생성
        ```
    * pytest-xdist : 테스트 병렬 실행(--headless 모드 필요)
        * --dist=loadscope : 모듈/클래스 단위로 병렬 테스트, 테스트간 공유 자원이나 공용 fixture등이 있는 경우 사용
        * --dist=each : 개별 테스트 함수 단위로 병렬 테스트, 테스트가 완전히 독립적인 경우 사용
        ```
        pip install pytest-xdist

        pytest -n 코어수 --dist=loadscope
        pytest -n auto  # 코어수 자동 감지
        ```
    * pytest-rerunfailures : 테스트 실패 시 자동 재실행
        ```
        pip install pytest-rerunfailures

        pytest tests/unit/ --reruns 3   # 실패한 테스트를 최대 3번까지 재시도
        ```
    * pytest-mock : mock 객체 생성 및 관리, 외부 API 호출에 대한 의존성 제거

    * pytest-asyncio : 테스트 대상이 되는 API가 FastAPI, Starlette 등 비동기 방식으로 구현되었거나, API를 호출하는 클라이언트 코드가 aiohttp, httpx 등의 비동기 방식으로 작성되었을 때 pytest 실행 지원

</br>

## API 테스트
### API 검증 항목
* status code
* header
* elapsed time(응답 시간)
* body값 검증
    * 값의 타입
    * 특정 키 존재 여부
    * 빈 문자열인지
* schema validation(스키마 검증) : body의 타입 검증

### HTTP 메서드 요청
* response 객체
    ```python
    response.status_code    # return type int
    response.text   # return type str, Body값 반환
    response.json()   # API 서버의 응답에 따라 dict or list 형태로 Body값 반환
    response.headers    # return type dict
    response.elapsed    # return type timedelta(시/분/초, 0:00:00.120301)
    response.elapsed.total_seconds()    # return type timedelta(초, 0.120301)
    ```

    ![Ipython_res 객체가 가지고 있는 속성과 메서드 목록](./img/image-5.png)

* GET
    ```python
    import requests

    url = "htte://example.com"
    header = {"Content-Type": "application/json"}
    response = requests.get(url, headers = header)
    response.raise_for_status   # 상태코드가 4xx 이상이면 예외를 발생시킴
    ```

* POST
    ```python
    import requests

    url = "htte://example.com"
    form_data = {"form": "data"}
    response = requests.post(url, data=form_data)
    response.raise_for_status   # 상태코드가 4xx 이상이면 예외를 발생시킴
    ```

    ```python
    import requests

    url = "htte://example.com"
    body_data = {"userId": 1}
    response = requests.post(url, json=body_data)
    # json= 사용 시, 자동으로 헤더 추가(Content-Type: application/json)
    response.raise_for_status   # 상태코드가 4xx 이상이면 예외를 발생시킴
    ```

* PUT
    ```python
    import requests

    url = "htte://example.com"
    update_data = {
        "id": 1,
        "title": "수정된 제목"
        "body": "기존 body"}
    response = requests.post(url, json=update_data)
    response.raise_for_status   # 상태코드가 4xx 이상이면 예외를 발생시킴
    ```

* DELETE
    ```python
    import requests

    url = "htte://example.com"
    response = requests.delete(url)
    response.raise_for_status   # 상태코드가 4xx 이상이면 예외를 발생시킴
    ```

### 스키마 검증
* JSON Schema를 사용한 pytest 검증 예시  
    API response

    ```json
    {
    "userId": 1,
    "username": "kim",
    "isAdmin": false
    }
    ```

    schema.json
    
    ```json
    {
    "type": "object",
    "properties": {
        "userId": { "type": "integer" },
        "username": { "type": "string" },
        "isAdmin": { "type": "boolean" }
    },
    "required": ["userId", "username", "isAdmin"]
    }
    ```   
    test_schema.py

    ```python
    import requests
    import pytest
    from jsonschema import validate, ValidationError

    # JSON 스키마를 Python dict로 변환
    with open("schema.json", "r") as f:
        user_schema = json.load(f)

    # 테스트 함수
    def test_user_response_schema():
        response = requests.get("https://example.com/api/user/1")
        data = response.json()

        try:
            validate(instance=data, schema=user_schema) 
            # validate() : jsonschema 라이브러리 함수, 필드 누락, 타입 오류 등도 모두 검출
            # instance = 실제 응답 JSON 데이터
            # schema = JSON Schema

        except ValidationError as e:
            pytest.fail(f"❌ 스키마 검증 실패: {e.message}")
            # pytest.fail() : assert대신 실패 선언
    ```

</br>

# 코드 작성 시 참고사항
* FIRST 원칙
    * Fast : 테스트는 빠르게 실행되어야 함
    * Independent : 각 테스트가 독립적이어야 함
    * Repeatable : 환경에 무관하게 항상 동일한 결과 보장
    * Self-validating : 테스트 결과가 성공/실패로 명확하게 나타나야 함
    * Timely : 코드를 작성한 직후에 테스트 작성

* AAA 패턴
: 테스트 코드를 3단계로 나누는 패턴
    * Arrange : 테스트 준비
    * Act : 실제 동작 수행
    * Assert : 결과 검증

* 유지보수를 위한 테스트 코드 5대 원칙
    * 명확한 테스트명 사용
    * 단일 책임의 원칙
    * 반복 코드 최소화
    * 실패 원인 명확화
    * 변경에 강한 구조

<!-- 
프로세스 : 프로그램의 단위
다른 프로그램과 메모리 정보 공유 불가능

스레드 : 프로그램 내에서 일을 처리할 수 있는 단위
다른 프로그램과 메모리 정보 공유 가능 -->

> <span style="color:darkgray">**파이썬은 다른 프로그램과 메모리 정보 공유가 불가능한 언어이므로, 네트워크로 메세지를 메모리 DB에 저장하여 다른 프로그램과 정보 공유**</span>

# 테스트 데이터
* 종류
    * 고정 데이터
    * Mock 데이터
    * 동적 데이터

## ORM(Object Relational Mapping)
: 객체와 DB모델을 이어주는 역할

* 구성 요소
    * Schema Object(모델 객체)
    : DB 테이블에 1대1 대응이 되도록 DB User table에 매핑되는 "객체 선언"

    ```SQL
    CREAT TABLE User(
        id INTEGER NOT NULL,
        name VARCHAR9100
    );
    ```

    * Query Builder
    : js로 쿼리를 만들면 "실제 DB에서 실행할 SQL로 변환"해주는 기능
    ```SQL
        SELECT id, name FROM User
        WHERE id 123;
    ```

    * Migration Tool
    : DB Schema 변경사항을 기록하고 관리하기 위한 마이그레이션 툴

# Mocking
* 라이브러리
    * unittest.mock (Python 내장)
    * pytest-mock (pytest 플러그인)  
        - **HTTP 요청이 발생하지 않도록** 내부 로직을 통째로 대체함  
        - 플러그인 설치를 통해 @pytest.fixture 정의 없이 mocker를 fixture로 사용 가능
        - API 호출, 함수, 메서드, 클래스 mocking 가능(독립적인 테스트 가능)

        ```python
        # app.py
        # 사용자의 정보를 받아오는 함수

        import requests

        # 예외동작 지정 등 기능 확장을 위해 get_user() 사용
        def get_user(user_id):
            response = requests.get("https://api.example.com/user")
            return {
                "status_code": response.status_code,
                "data": response.json()
            }
        ```

        ```python
        # test_app.py

        import pytest
        from app import get_user

        # 매개변수로 mock을 받아와 @fixture 선언 없이도 mocker 사용 가능
        def test_get_user_with_mocker(mocker):    
            mock_response = mocker.Mock()   # Mock 객체 생성

            # 가짜 응답 등록
            mock_response.status_code = 200
            mock_response.json.return_value = {"name": "Kim"}

            # mocker.path() : app 모듈의 requests.get 함수를 mock.requests.get 함수로 대체
            mocker.path("app.requests.get", return_value=mock_response)
            
            # 대체된 get_user() 내부의 requests.get이 mock 함수로 호출되어 결과 반환
            user = get_user()

            assert user["status_code"] == 200
            assert user["data"]["name"] == "Kim"
        ```

    * responses (requests 전용)
        - 실제 API URL로 **요청을 보내지만 네트워크 없이 응답을 직접 지정**  
        - requests 라이브러리 호출을 가로채 가짜 응답 반환
        - 명세 기반 테스트 가능

        ```python
        # test_app.py

        @responses.activate # responses 활성화
        def test_get_user_with_response():
            # 가짜 응답 등록
            responses.add(
                responses.GET,
                "https://api.example.com/user",
                json={"name": "Kim"},
                status=200
            )

            # GET 호출 시 API는 호출되지만 가짜 응답이 반환됨 
            response = requests.get("https://api.example.com/user")
            data = response.json()

            assert response.status_code == 200
            assert data["name"] == "Kim"
        ```