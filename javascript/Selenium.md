# 기본 명령어
* driver.findElement(locator)
    * locator와 일치하는 첫 번째 WebElement 객체 반환
* driver.findElements(locator)
    * 요소를 찾으면 WebElement 객체를 담은 Array 반환
    * 요소를 찾지 못하면 [] 반환

<br/>

# Locator
* ID : 가장 빠르고 안정적인 고유값
* NAME : ID 다음으로 많이 사용됨
* CSS Selector(Cascading Style Sheets Selector)  
: 웹 페이지의 디자인 정의를 위해 사용되는 CSS를 locator로 사용하여 대부분의 요소를 쉽게 선택 할 수 있고 브라우저 네이티브 기능 사용 가능함

    * DOM의 역방향 탐색 불가(형제 ~ 자손만 탐색 가능)
    * 개발자 도구 > 콘솔에서 selector가 유효한지 확인 가능 : $$("css_selector")

* XPATH
: XML/HTML 문서의 특정 노드를 찾는 경로 언어, 절대경로(/)와 상대경로(//)가 있음

    * DOM의 양방향 탐색 가능(조상 ~ 자손 탐색 가능)
    * 텍스트 콘텐츠 기반으로 요소 탐색 가능
    * 개발자 도구 > 콘솔에서 xpath가 유효한지 확인 가능 : $x("your_xpath")

* XPATH, CSS Selector의 사용법은 파이선 셀레니움과 동일

```js
const { By } = requirement('selenium-webdriver');

const elemById = await driver.findElement(By.id('ID')); // 가장 빠르고 안정적
const elemByName = await driver.findElement(By.name('name'));   // form 요소에서 사용됨
const elemByClassName = await driver.findElement(By.name('className')); // 복합 클래스는 selector 사용
const elemByTagName = await driver.findElement(By.tagName('tagName'));

const elemByLink = await driver.findElement(By.linkText('linkText'));   // <a>태그 전용
const elemByPartialLink = await driver.findElement(By.partialLinkText('partialLinkText'));  // 텍스트가 동적으로 변하거나 너무 길때 사용

const elemBySelector = await driver.findElements(By.css('button.class'));
const elemByXpath = await driver.findElement(By.xpath('xpath'));
```

> <span style="color:darkgray">**브라우저 콘솔에서 요소 확인하는 법  
CSS : $$("선택자")  
XPATH : $x("선택자")**</span>

<br/>

# 요소 다루기
element.sendKeys("text");
element.clear();
element.click();

* 상태 확인
element.isDisplayed()   // 요소가 화면에 있는지 확인, true, false 반환
element.isEnabled() // 요소가 활성화 되었는지 확인
element.isSelected()

* 속성값 추출
element.getText()   // 렌더링된 텍스트 콘텐츠 추출
element.getAttribute("attribute")    //

* 드롭다운
: python과 다르게 Select 객체가 없으므로 ```<option>옵션</option>``` 을 직접 클릭해야함

* 체크박스, 라디오 버튼
: 클릭으로 처리

<br/>

# 대기
* 무조건 대기
```js
await driver.sleep(ms);
```

* 암시적 대기 (Implicit Wait)
: 요소를 즉시 찾지 못하면 지정된 시간동안 DOM을 주기적으로 재탐색, 
명시적 대기와 혼용시 예상치 못한 동작 발생 가능  
<u>**한번 설정하면 모든 findElement에 적용됨**</u>

```js
await driver.manage().setTimeouts({implicit: 10000});   // 10초
```

* 명시적 대기 (Explicit Wait)
: 특정 조건이 충족될때까지 대기

```js
// 예시 1. 명시적으로 작성하는 방법
driver = await new Builder().forBrowser('chrome').build();

const wait = new WebDriverWait(driver, 10000); // timeout 10초
await wait.until(until.elementLocated(By.id('ID')));    // until.elementLocated() : ExpectedConditions
```

```js
// 예시 2. 일반적으로 작성하는 방법
driver = await new Builder().forBrowser('chrome').build();
await driver.wait(until.elementLocated(By.id('ID')), 10000);
```
* Expected Conditions
: until 객체 사용  
<a href="https://docs.newrelic.com/kr/docs/synthetics/synthetic-monitoring/scripting-monitors/synthetics-scripted-browser-reference-monitor-versions-050/">참고 링크</a>

    * until.elementIsEnabled(WebElement) : 요소가 활성화(클릭/입력 가능)될 때까지 대기
    * until.elementIsDisabled(WebElement) : 요소가 비활성화될 때까지 대기
    * until.elementIsSelected(WebElement) : 요소가 선택될 때까지 대기
    * until.elementIsNotSelected(WebElement) 요소가 선택 해제될 때까지 대기
    * until.stalenessOf(WebElement) : 요소가 DOM에서 사라질 때까지 대기 (페이지 이동/갱신 후)

    * until.alertIsPresent() : 얼럿(Alert) 창이 나타날 때까지 대기

    * until.titleIs(string) : 페이지 제목이 특정 문자열과 같거나 포함할 때까지 대기
    * until.titleContains(string) : 페이지 제목이 특정 문자열과 같거나 포함할 때까지 대기
    * until.urlIs(string) : 페이지 URL이 특정 문자열과 같거나 포함할 때까지 대기
    * until.urlContains(string)  : 페이지 URL이 특정 문자열과 같거나 포함할 때까지 대기

* Custom Expected Conditions
```js
const waitForText = () => {
    return async function(driver) { // async function : 비동기 함수, Promise 반환
        const elem = await driver.findElement(By.id('ID')); // 비동기 작업
        const text = await elem.getText();  // 비동기 작업
        return text === '시작' ? elem : false;
    };
};
```
* Fluent Wait
    * withTimeout : 전체 최대 대기 시간
    * pollingEvery : 조건 확인 주기 설정
    * ignoring : 대기중 발생하는 exception을 무시하고 계속 시도

<br/>

# 팝업, 얼럿 처리
: alert와 같이 브라우저 기본 기능인 것은 포커스 이동을 통해 객체를 가져올 수 있다.

```js
// 1. 대기
await wait(until.alertsPresent());

// 2. 포커스 전환
const alert = await driver.switchTo().alert();

// 3. 상호작용
await alert.accept();
await alert.dismiss();
const alertText = await alert.getText();
await alert.sendKeys('text');   // 프롬프트에 텍스트 입력
```

<br/>

# 프레임 내부 요소 접근
: ```<frame>``` 또는 ```<iframe>``` 태그 내부에 있는 요소는 별도의 HTML 문서로 취급됨
따라서 프레임 내부 요소에 접근하려면 해당 프레임으로 포커스 전환을 해야함

```js
// 1. 포커스 전환
await driver.switchTo().frame(identifier);

// 2. 프레임 내부 요소 조작

// 3. 포커스 복귀
await driver.switchTo().parentFrame();  // 부모 프레임으로 이동
await driver.switchTo().defaultContent();   // 최상위 HTML로 이동
```
* identifier 종류
    * index값
    * 프레임의 name 또는 id 속성 값
    * frameElement(프레임 요소 찾아서 넣기)

<br/>

# 브라우저 창/탭 전환
: 새 창이나 새 탭이 열렸을 때 포커스 전환이 필요함. 각 창/탭은 고유한 Window Handle(문다열 ID)을 가짐

```js
//1. 현재 창 핸들 저장
const originalHandle = await driver.getWindowHandle()

// 2. 새 창/탭 여는 동작 수행

// 3. 모든 창 핸들 가져오기
const allHandles = await driver.getWindowHandles()

// 4. 새 창 핸들 찾기 (기존 핸들과 다른 핸들)
const newHandle = ~

// 5. 새 창으로 전환
await driver.switchTo().window(newHandle);

// 6. 원래 창으로 복귀
await driver.switchTo().window(originalHandle)
```

<br/>

# Actions class
* .perform() : 액션 실행을 위한 명령어

```js
const actions = driver.actions({bridge:true});  // action API 객체 생성, {bridge:true} : 구버전 사용 선언

await actions.move({origin: element}).perform();  // 특정 WebElement 객체 위로 마우스 오버
await actions.move({ origin: element, x: 50, y: 10 }).perform();    // 특정 WebElement 객체 기준으로 좌표만큼 떨어진 곳에 마우스 오버

await actions.dragAndDrop(sourceElement, targetElement).perform();  // 드래그 앤 드롭, sourceElem을 클릭해서 targetElem으로 이동
await actions.clickAndHold(source).move({origin: target}).release().perform();  // 드래그 앤 드롭, 마우스 클릭 유지, 이동, 클릭해제 동작을 나누어 작성한 방식

await actions.doubleClick(element).perform();   // 마우스 더블 클릭
await actions.contextClick(element).perform();  // 마우스 우클릭

await actions.keyDown(Keys.SHIFT).sendKeys('abc').keyUp(Keys.SHIFT).perform();  // 특수키 누른 상태로 키보드 이벤트 조합 입력

await actions.move({origin: el1}).click().sendKeys('text').perform();   // 동작 체이닝

```

<br/>

# 파일 업로드
: 실제 업로드를 하는것처럼 경로를 서버로 넘겨 서버에서 이미지 업로드 받아야 함
button 요소의 숨겨진 ```<input type="file">```에 파일의 절대 경로를 send_keys()로 입력

```js
import path from 'path';
import { fileURLToPath } from 'url';
import { Builder, By } from 'selenium-webdriver';

// 현재 파일 경로 계산 (__dirname 대체)
const __filename = fileURLToPath(import.meta.url);

// 이미지 파일 경로 설정
const imgSource = path.resolve(__dirname, '../resources/testdata/review_photo.jpg');

// WebDriver 시작
const driver = await new Builder().forBrowser('chrome').build();

const uploadInput = await driver.findElement(By.css('input.hidden'));
await uploadInput.sendKeys(imgSource);  // 파일 업로드
```

<br/>

# JavaScript 직접 실행
* executeScript()  
: 강제 이벤트 발생, 숨겨진 요소 제어, 브라우저 정보 추출, 스크롤 제어 등 WebDriver API만으로 수행하기 어려운 작업 수행

```
driver.executeScript("js code", [arguments])
```

* executeAsyncScript()  
: AJAX 요청, setTimeout등 브라우저 컨텍스트에서 비동기 작업을 실행하고 완료 시 결과 반환