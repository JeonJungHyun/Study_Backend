

# 🛡️ 06. Validation & Exception

<details>
<summary>1. 데이터 검증(Validation)과 예외 처리(Exception)의 필요성</summary> </br>

만약 사용자가 실수로, 혹은 나쁜 의도로 이상한 데이터를 보내면 어떻게 될까? </br>

예를 들어, 나이를 입력하는 칸에 "스무살"이라는 글자를 넣거나, 회원가입인데 비밀번호를 빈칸으로 보낸다면 </br>
서버는 계산을 하려다 툭 하고 멈춰버릴(에러가 날) 수 있다. </br>

`Validation(검증)`은 "우리 서버에 들어오기 전에 데이터가 올바른지 입구에서 미리 검사하는 것". </br>

`Exception Handling(예외 처리)`은 "만약 내부에서 예상치 못한 사고가 터졌을 때, </br>
서버가 완전히 죽지 않게 수습하고 사용자에게 상황을 설명해 주는 것". </br>

이 두 가지가 잘 되어 있어야 서버가 24시간 안정적으로 돌아갈 수 있다.

</details>

<details>
<summary>2. Bean Validation : 데이터 검문소</summary> </br>

옛날에는 사용자가 보낸 데이터를 검사할 때 하나하나 if(age < 0) ... 같은 코드를 직접 짰다. </br>

하지만 데이터가 많아지면 코드가 너무 지저분해진다. 그래서 스프링에서는 Bean Validation이라는 도구를 쓴다. </br>

이 방식은 DTO(데이터 전달 객체)의 필드 위에 어노테이션(@) 하나만 붙여주면 자동으로 검사를 해준다. </br>

- @NotBlank: "야, 너 여기 아무것도 안 쓰거나 공백만 치고 넘어가면 안 돼!" (가장 많이 씀) </br>

- @Size(min=8, max=16): "비밀번호는 최소 8자에서 16자 사이로만 적어줘." </br>

- @Email: "이메일 형식이 골뱅이(@)도 있고 점(.)도 찍힌 정상적인 형식인지 확인해 봐." </br>

</br>

🌟 핵심 포인트: Controller에서 데이터를 받을 때 파라미터 앞에 **@Valid**라는 도장을 찍어줘야 한다. </br>

그래야 스프링이 "아, 이 DTO는 검문소(Validation)를 거쳐야 하는구나!"라고 알고 검사를 시작한다.

</details>

<details>
<summary>3. 사용자 정의 예외 (Custom Exception) </summary> </br>

자바 언어 자체에는 기본적으로 NullPointerException(데이터가 비어있음) 같은 에러들이 이미 있다. </br>

하지만 이건 너무 포괄적이라서 어디서 왜 에러가 났는지 알기 어렵다. </br>

개발을 하다 보면 "아이디가 이미 있을 때", "로그인 비밀번호가 틀렸을 때"처럼 우리 서비스에만 있는 특별한 상황이 생긴다. </br>

이때 자바가 주는 기본 에러 대신 우리가 직접 이름을 붙인 에러(Custom Exception)를 만들어서 쓰는 것. </br>

</br>

🤔 왜 만들어? </br>

에러 이름만 봐도 UserNotFoundException이라고 되어 있으면 "아, 유저를 못 찾아서 에러가 났구나!" 하고 바로 알 수 있다. </br>

🤔 어떻게 써? </br>

RuntimeException이라는 조상 클래스를 상속받아서 나만의 클래스를 만들고, 코드 중간에 문제가 생기면 </br>

throw new UserNotFoundException();이라고 던져주면 된다.

</details>

<details>
<summary>4. @RestControllerAdvice </summary> </br>

서버 이곳저곳(Controller, Service, Repository)에서 에러가 터질 때마다 모든 곳에 try-catch 같은 응급 처치 코드를 도배하면 어떻게 될까? </br>

코드가 너무 지저분해져서 읽기 힘들어진다. </br>

그래서 스프링은 **@RestControllerAdvice**라는 '중앙 응급실'을 딱 하나 만들었다. </br>

</br>

✏️ 하는 일: 프로젝트 어디에서든 에러가 터져서 밖으로 튀어나오면, 이 응급실이 그걸 낚아챈다. </br>

✏️ 장점: 개발자는 "에러가 나면 여기서 처리할게!"라고 한곳에만 정의해 두면 된다. </br>

그럼 코드가 아주 깔끔해지고, 에러 관리도 한눈에 들어오게 된다. </br>

이 응급실 안에서 **@ExceptionHandler**라는 전담 의사들을 배치해서, "로그인 에러는 이 의사가 처리하고, DB 에러는 저 의사가 처리해!"라고 정해둘 수 있다.

</details>

<details>
<summary>5. 에러 응답 규격 (Error Response) : 친절한 사고 안내문</summary> </br>

에러가 났을 때 클라이언트(프론트엔드)에게 그냥 "에러 났어!"라고만 하면 프론트엔드 개발자는 당황한다. 정확히 어떤 에러가, 왜 났는지 알려줘야 한다. </br>

그래서 우리만의 **에러 안내문 양식(JSON)**을 미리 약속해 둔다. </br>

- 상태 코드(Status): HTTP 표준 번호 (예: 400은 잘못된 요청, 404는 못 찾음) </br>

- 에러 코드(Code): 우리가 만든 고유 번호 (예: USER_001) </br>

- 메시지(Message): 사용자 화면에 띄워줄 친절한 설명 (예: "이미 사용 중인 아이디입니다.") </br>

이렇게 일정한 양식을 보내주면, 프론트엔드 개발자는 그 양식을 보고 사용자 화면에 경고창을 띄워주기만 하면 되니까 협업이 훨씬 쉬워진다.

</details>

<details>
<summary>6. 최종 요청 처리 흐름 (에러가 날 때)</summary> </br>

1️⃣ 입구: 사용자가 데이터를 보낸다. </br>

2️⃣ 검문: Controller의 @Valid가 DTO를 검사한다. (잘못되면 여기서 바로 에러 발생!) </br>

3️⃣ 실행: Service에서 로직을 수행하다가 문제가 생기면 Custom Exception을 던진다. </br>

4️⃣ 구조: 밖으로 던져진 에러를 @RestControllerAdvice 응급실이 낚아챈다. </br>

5️⃣ 처방: 미리 정해둔 Error Response 양식에 에러 내용을 담는다. </br>

6️⃣ 응답: 클라이언트에게 친절한 에러 JSON을 반환한다. </br>

이 과정을 통해 사용자는 "아, 내가 뭘 잘못 입력했구나"를 알게 되고, 서버는 죽지 않고 다음 요청을 받을 준비를 한다.

</details>

<details>
<summary>7. 정리</summary> </br>

Validation & Exception은 백엔드 구조에 '안전장치'를 다는 과정. </br>

Validation으로 잘못된 데이터가 들어오는 걸 입구에서 컷(Cut)하고, </br>

Exception Handling으로 발생한 사고를 우아하게 수습한다. </br>

</details>

---

🔗 참고 </br>
Google Gemini_ 데이터 처리와 예외검증 </br>

