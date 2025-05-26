# JEST
: JavaScript 테스트 프레임워크
    * 테스트 프레임워크 : 데이터 기반 테스트 등을 통해 테스트 로직과 데이터를 분리하여 유지보수성을 높이기 위한 것

* helper 함수
: 반복적으로 사용되는 로직을 별도 함수/클래스로 분리하여 작성
    * 포멧 변환 함수, 랜덤 데이터 생성 함수, 커스텀 wait 함수, API 호출 함수 등
<br/>

## 코드 구조
```js
import { Builder, By, until } from "selenium-webdriver";

describe('TestSuite 설명', () => {
    let driver; // 전역변수처럼 사용되어 테스트 코드 밖에 선언

    beforeEach(async () => {    
        // 각각의 it 실행 전 실행할 내용, Pytest의 Fixture와 같은 역할
        driver = await new Builder().forBrowser('chrome').build();  // driver 변수에 내용 저장
    });
    
    afterEach(async () => {
        // 각각의 it 실행 후 실행할 내용
    });

    beforeAll(async () => {
        // 모든 it 실행 전 딱 한번 실행하는 내용, Setup
    });

    afterAll(async () => {
        // 모든 it 실행 후 딱 한번 실행하는 내용, TearDown
    });

    it('각 TestCase 설명', async () => {

    });

    expect(await actualResult).Matcher(expectedResult);
});
```

* Matcher
    * .toBe(value) : 값과 타입이 정확히 일치하는지 확인(===)
    * .toEqual(value) : 객체 또는 배열의 내부 속성값이 일치하는지 확인
    * .toContain(item) : 배열이나 문자열에 특정 내용을 포함하는지 확인
    * .toHaveLength(number) : 배열이나 문자열의 길이 확인
    * .toMatch(regexp) : 정규 표현식과 일치하는지 확인
    * .toBeGreaterThan(number) : number보다 큰 숫자인지 확인
    * .toBeLessThan(number) : number보다 작은 숫자인지 확인
    
    * .toBeTruthy() : 값이 true인지
    * .toBeFalsy() : 값이 false 인지
    
    * .toBeNull() : 값이 null인지
    * .toBeUndefined() : 값이 undefined인지
    * .toBeDefined() : 값이 정의되어 있는지

<br/>

### DDT(Data Driven Test)
: 동일한 테스트 로직에 데이터만 변경하여 반복 테스트하는 경우를 위해 테스트 로직과 테스트 데이터를 분리하여 관리
it.each(), test.each() 모두 사용 가능함

```js
// 예제 1. 배열 데이터, test.each() 버전
const data = ['A', 'B', 'C'];

describe('배열 데이터', () => {
    test.each(data)('실행 성공 시 출력 문구', async (매개변수) => {
        // 테스트 로직
        // 검증 로직
        expect(actualResult).Matcher(expectedResult);
    })
})
```

```js
// 예제 2. 객체 배열 데이터, it.each() 버전
const data = [
    {'key_1': 'A', 'key_2': 'a'},
    {'key_1': 'B', 'key_2': 'b'},
    {'key_1': 'C', 'key_2': 'c'}
    ];

describe('배열 데이터', () => {
    it.each(data)('실행 성공 시 출력 문구', async ({key_1, key_2}) => { // 키값이 여러개라 구조 분해 사용
        // 테스트 로직
        // 검증 로직
        expect(actualResult).Matcher(expectedResult);
    })
})
```

<br/>

## 테스트 실행
* 특정 테스트 파일 실행
```
npx jest path/test.js
```

* 특정 패턴을 가진 테스트 이름 실행
```
npx jest -t "테스트 이름 포함 문자열" 
```

* 특정 폴더 실행
```
npx jest path/folder
```

* tagging 테스트 코드 실행
```js
describe('[ @smoke ] 로그인 기능', () => {
  test('올바른 계정으로 로그인', () => {
    // 테스트 코드
  });
});

test('[ @regression ] 비밀번호 오류 테스트', () => {
  // 테스트 코드
});
```

```
// 방법 1.
npx jest -t '@smoke'
```

```
// 방법 2.
npx jest --testNamePattern='@regression'
```

## HTML 리포터
* 설치
```
npm install --save-dev jest-html-reporter
```

* 설정 코드
```js
//jest.config.js

module.exports = {
  reporters: [
    "default",
    ["jest-html-reporter", {
      pageTitle: "Test Report",
      outputPath: "test-report.html"
      includeFailureMsg: true,
      includeConsoleLog: true,
      theme: "defaultTheme"
    }]
  ]
}
```