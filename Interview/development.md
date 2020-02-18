# Interview

## <span id="questions">Questions</span>

- <a href="#ans1">CORS에 대해 설명해주세요 또는 CORS는 브라우저와 관련이 있나요</a>
- <a href="#ans2">PUT, PATCH, OPTIONS에 대해 간략히 설명해주세요.</a>
- <a href="#ans3">Content-Type 에는 어떤 종류가 있나요</a>
- <a href="#ans4">application/x-www-form-urlencoded와 multipart/form-data의 차이점은</a>
- <a href="#ans4">엥귤러에서 양방향 바인딩이란 무엇인가요, 단방향 바인딩은 무엇인가요</a>
- <a href="#ans4">현재 서버에 접속중인 사용자는 어떻게 확인하나요</a>
- <a href="#ans4">서버 10대를 관리한다고 가정했을 때 로그 수집은 어떻게 하나요</a>
- <a href="#ans4">Meteor를 사용한 이유는 무엇인가요</a>
- <a href="#ans4">PHP에서 Node로 변경한 이유는 또는 차이점은</a>
- <a href="#ans4">동영상 스트리밍은 어떤 방식을 사용했나요</a>
- <a href="#ans4">람다의 Connection pool 방식에 대해서 설명해주세요</a>
- <a href="#ans4">람다에서 3rd party를 호출해보신적이 있으신가요</a>
- <a href="#ans4">람다는 일반적으로 외부에서 호출할 수 없는데 어떻게 사용할 수 있나요</a>
- <a href="#ans4">DB Pool의 초기 설정은 어떻게 하셨고, 어떤 방식으로 사용하셨나요</a>
- <a href="#ans4">오픈 소스에 기여하신 경험이 있으신가요</a>
- <a href="#ans4">리덕스를 사용하신적이 있나요</a>
- <a href="#ans4">리엑트에서 비동기 호출에 대한 렌더링은 어떤 방식으로 하나요</a>
- <a href="#ans4">DynamoDB는 어떤 경우에 사용하셨나요</a>

## Answers

<span id="anc1">1. CORS에 대해 설명해주세요.</span> [[목차](#questions)]

- 아래의 HTTP 요청은 기본적으로 cross-site HTTP 요청이 가능하다.
  - `<img>`태그로 다른 도메인의 이미지 파일을 가져오거나
  - `<link>`태그로 다른 도메인의 CSS를 가져오거나
  - `<script>`태그로 다른 도메인의 Javascript 라이브러리를 가져오거나  
- `<script></script>`로 둘러싸여 있는 스크립트에서 생성된 XMLHttpRequest cross-site HTTP 요청은 보안상 브라우저의 제한으로 **same-origin policy**의 적용을 받기 때문에 cross-site HTTP요청이 불가하다. (프로토콜,호스트명,포트가 같은 경우에는 가능)
- `<script></script>`에서 생성되는 XMLHttpRequest에 대해서도 cross-site HTTP 요청이 가능해야 한다는 요구가 늘어나자 W3C에서 CORS(Cross-Origin Resource Sharing)라는 이름의 권고안이 나옴.
- CORS 요청은 Simple/Preflight, Credential/Non-Credential의 조합으로 4가지가 가능
- 브라우저가 요청 내용을 분석하여 위의 4가지 방식중 하나로 서버에 요청을 전송하기 때문에 개발자는 목적에 맞는 방식을 선택하여 개발해야 함.
- Simple Request
  - GET, POST, HEAD 중 하나여야 함
  - POST 방식일 경우 Content-Type이 아래 셋 중에 하나여야 함
    - application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain
  - 커스텀 헤더를 전송하지 말아야 함.
- Simple Request 조건에 해당하지 않으면 브라우저는 Preflight Request 방식으로 요청함.
- Preflight Request는 예비요청(Preflight)과 본요청(Actual)로 진행됨
- Actual Request는 서버에서 반환한 `Access-Control-Allow-Methods`에 대해서만 진행 가능.
- Request with Credential
  - 클라이언트는 요청 시 xhr 요청시 `xhr.withCredential: true`와 같이 지정해 쿠키를 전달해야 함.
  - 서버는 Response Header에 반드시 `Access-Control-Allow-Credentials: true`를 포함해야 함.
  - 서버에서 `Access-Control-Allow-Origin: *`이 오면 안되며 `http://foo.origin`과 같은 구체적 도메인이 와야 함.
  - Simple Request에 `xhr.withCredential: true`가 지정되어 있으나 Response Header에 `Access-Control-Allow-Credentials: true`가 명시되어 있지 않으면, 해당 Response는 브라우저에 의해 무시됨
  - 예비 요청에 대한 응답에 `Access-Control-Allow-Credentials: false`를 포함하면, 본 요청은 Request with Credentials을 보낼 수 없음.
- 서버측에서의 CORS 요청 처리
  - `Access-Control-Allow-Origin`
    - 모든 도메인으로부터 서버 리소스 접근 허용하려면: *
    - 1개 이상의 도메인을 적으면 오류 발생
  - `Access-Control-Expose-Headers`: 브라우저에서 기본적으로 접근 불가한 헤더(Content-Length) 및 커스텀 헤더를 
  확인할 수 있음
  - `Access-Control-Max-Age`: Preflight Request의 결과가 캐시에 얼마나 남아 있는지를 보여줌.
  - `Access-Control-Allow-Headers`: 예비 요청에 대한 Response Header에 사용되며, 본 요청에서 사용할 수 있는 HTTP Header를 지정.
    - 사용 가능한 헤더 예시: Content-Type, Accept-Encoding, X-CSRF-Token, Authorization
 
[MDN - HTTP 접근제어(CORS)](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
[CORS](https://brownbears.tistory.com/336)
