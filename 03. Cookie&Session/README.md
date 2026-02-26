# 🍪 03. Cookie & Session 

<details>
<summary>1. 쿠키와 세션은 왜 필요한가?</summary> </br>

웹 브라우저와 웹 서버가 데이터를 주고 받을 때 HTTP 통신을 이용하는데, HTTP는 `Stateless(무상태성)` 프로토콜이다. </br>

즉, 서버는 이전 요청의 상태를 저장하지 않는다는 것이다. </br>

따라서 한 번 작성하거나 사용한 뒤에는 반복적으로 작업하지 않도록 저장해 두는 것이 필요한데, </br>

이때 등장하는 개념이 바로 쿠키와 세션이다. </br>

</details>

<details>
<summary>2. Cookie</summary> </br>

**1) Cookie란?** </br>

쿠키란 사용자가 어떤 웹 사이트에 들어갔을 때 사용자 브라우저에 저장되는 작은 데이터이며, `키와 값(key, value)` 형태로 구성되어 있다. </br>

서버는 응답 시 `Set-Cookie` 헤더를 통해 쿠키를 생성한다. </br>

브라우저는 쿠키를 저장해 놓았다가, 사용자가 요청하면 해당 정보를 함께 보내서 서버가 사용자를 식별할 수 있게 해준다. </br>

**2) 전송 방식** </br>

쿠키를 사용하여 로그인하는 과정을 살펴보면, 아래와 같다. </br>

<img width="820" height="396" alt="image" src="https://github.com/user-attachments/assets/8ec91fbc-f814-46e8-9130-b32c2098c508" />

1) 클라이언트가 서버에 요청을 보낸다. </br>
2) 서버가 응답과 함께 쿠키를 생성한다. </br>
3) 브라우저가 쿠키를 저장한다. </br>
4) 이후 요청마다 쿠키가 자동 전송된다. </br>

**3) 주로 사용되는 곳** </br>

- 로그인 상태 유지 (아이디 기억하기, 자동 로그인) </br>
- 장바구니 (로그인하지 않아도 상품 유지) </br>
- 사용자 설정 저장 (다크모드 여부, 팝업 "오늘 하루 보지 않기" 등) </br>

**4) 쿠키의 한계** </br>

- 보안 취약성: 클라이언트에 저장되므로 사용자가 임의로 수정하거나 탈취하기 쉽다. </br>

- 용량 제한: 하나의 쿠키는 4KB로 크기가 제한되어 있다. </br>

- 성능 저하: 매 요청마다 서버로 전송되기 때문에 쿠키가 많아지면 네트워크 부하가 커진다. </br>

</details>

<details>
<summary>3. Session</summary> </br>

**1) Session이란?** </br>

세션은 서버에 저장되는 정보이며, 사용자의 민감한 정보는 서버 측에서 관리하고 </br>
클라이언트에게는 그 정보를 찾을 수 있는 '열쇠'인 **세션 ID(Session ID)**만 발급해 주는 방식이다. </br>

**2) 동작 방식** </br>
1) 클라이언트가 서버에 로그인(인증) 요청을 보낸다. </br>

2) 서버는 계정 정보를 확인 후, 서버의 세션 저장소(메모리 또는 DB)에 정보를 저장하고 고유한 Session ID를 발급한다. </br>

<img width="4590" height="1247" alt="image" src="https://github.com/user-attachments/assets/435e56b7-575e-4066-89b3-a6cb1c15c4e4" />

3) 서버는 응답 헤더의 Set-Cookie에 Session ID를 담아 보낸다. </br>

4) 클라이언트는 이후 요청마다 이 Session ID가 담긴 쿠키를 함께 전송한다. </br>

5) 서버는 전달받은 ID로 세션 저장소에서 사용자 정보를 확인하여 응답한다. </br>

<img width="4590" height="1247" alt="image" src="https://github.com/user-attachments/assets/a9691ae0-95b6-4cb7-8d37-efe3894c06db" />


**3) 장단점** </br>

- 장점: 실제 데이터가 서버에 있으므로 쿠키보다 훨씬 안전하다. </br>

- 단점: 사용자가 많아질수록 서버 메모리(RAM) 사용량이 늘어나 서버 부하가 발생할 수 있다. </br>

</details>


---

🔗 참고 </br>
https://gdsc-university-of-seoul.github.io/Login-using-cookie-and-session/ </br>
https://hongong.hanbit.co.kr/완벽-정리-쿠키-세션-토큰-캐시-그리고-cdn/ </br>
https://velog.io/@ysy3285/쿠키-VS-세션 </br>


🎞️ 이미지 출처 </br>
https://velog.io/@ysy3285/쿠키-VS-세션 </br>
https://velog.io/@dev_jiwon/Security-쿠키Cookie와-세션Session </br>
