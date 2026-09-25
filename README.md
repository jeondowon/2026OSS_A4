# 오픈소스 스튜디오 01분반

22300650 / 전도원

## Assignment 4. HTML Form & Validation

## Key Learning

1. Form 구조 - form 안에서 label과 입력 요소를 for / id로 연결하고, fieldset과 legend로 Form의 구조를 만드는 방법을 배웠습니다.
2. Form CSS - :hover, :focus, :checked 등으로 사용자 동작에 반응하는 UI를 만들 수 있다는 것을 배웠습니다.
3. Validation - required, type="email", minlength 같은 HTML 속성으로 검사 조건을 선언하고, JavaScript의 checkValidity()로 그 조건들을 검사해서 제출내용이 유효한지 확인하는 방법을 배웠습니다.

## Form Elements

Bootstrap Checkout 예제(https://getbootstrap.com/docs/5.2/examples/checkout/)를 HTML 구조 중심으로 참고하여 form1.html을 만들었습니다.

1. input type="text": 이름, Username, 주소, 우편번호, 카드 정보 입력
2. input type="email": 이메일 입력
3. input type="password": 비밀번호 입력
4. input type="radio": 결제 방식(Credit card / Debit card / PayPal) 중 하나 선택
5. input type="checkbox": 배송지 동일 여부, 정보 저장 여부 선택
6. input type="date": 배송 날짜 선택
7. input type="color": 선물 포장 색상 선택
8. select + optgroup: 국가 선택, 대륙(Asia / America / Europe)별로 옵션을 묶음
9. datalist: State / City를 직접 입력하거나 추천 목록에서 선택
10. textarea: 배송 요청사항 입력
11. fieldset + legend: Billing address / Options / Payment 세 영역으로 항목을 묶고 제목 표시

## HTML vs CSS

form1.html은 아무 스타일을 적용하지 않은 기본 상태입니다. form1_css.html은 같은 Form에 CSS를 적용해 입력 요소와 버튼의 모양을 통일하고, 넓은 화면에서는 항목을 나란히 배치하며 좁은 화면에서는 세로로 정렬되도록 구성했습니다. hover와 focus 상태도 추가해 조작 중인 요소를 쉽게 알아볼 수 있습니다.

## Validation & JS

form1_js.html에 HTML Validation 속성을 적용했습니다.

1. required - First name, Last name, Username, Email, Password, Address, Country, Zip 8개 항목
2. type="email" - Email 입력
3. minlength - Password 6자 이상, Username 3자 이상

JavaScript에서는 form의 submit 이벤트를 addEventListener()로 처리했습니다. event.preventDefault()로 기본 제출 동작을 막고, 필수 항목을 위에서부터 차례로 checkValidity()로 검사합니다. 유효하지 않은 항목이 나오면 빨간 테두리를 표시하고 alert()로 오류 메시지를 띄운 뒤, focus()로 해당 항목에 커서를 옮기고 return으로 함수를 종료합니다. 모든 항목이 조건을 충족하면 alert("등록이 완료되었습니다.")가 표시됩니다. 값을 고치거나 Reset을 누르면 오류 표시가 사라지도록 input, reset 이벤트도 만들었습니다.

## Problem & Solution

문제
required나 minlength 조건에 맞지 않는 값으로 제출하면 브라우저 기본 말풍선만 뜨고, JavaScript의 checkValidity() -> alert() -> focus() -> return 코드는 전혀 실행되지 않았습니다. 브라우저의 기본 검사가 submit 이벤트보다 먼저 실행되어서, 값이 유효하지 않으면 submit 이벤트 자체가 발생하지 않기 때문이었습니다.

해결
form 태그에 novalidate 속성을 추가해서 브라우저 기본 검사를 끄고 JavaScript가 검사를 맡도록 했습니다. required, type="email", minlength 속성은 그대로 두었기 때문에 checkValidity()는 이 조건들을 기준으로 정상적으로 검사합니다.

## Reflection

HTML 속성만으로도 필수 입력, 이메일 형식, 글자 수 같은 검사를 할 수 있지만, 오류 메시지와 이후 동작을 직접 정하려면 JavaScript가 필요하다는 걸 알게 됐습니다. 실제 서비스에서는 브라우저와 JavaScript 검사 외에 서버에서도 다시 검사해야 한다고 하는데, 서버 쪽 검사는 어떻게 구현하는지 알아보고 싶습니다.
