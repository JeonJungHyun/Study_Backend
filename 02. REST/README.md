# ⚙️ 02. REST 

<details>
<summary>1. REST란?</summary> </br>

REST(Representational State Transfer)는  
웹에서 자원(Resource)을 효율적으로 주고받기 위한 아키텍처 스타일이다. </br>

즉, API를 설계할 때 지켜야 하는 `설계 원칙`이라고 볼 수 있다. </br>

REST는 HTTP 프로토콜의 특징을 기반으로 만들어졌으며, </br>
웹의 기본 구조인 `요청(Request) - 응답(Response)` 방식을 따른다. </br>

</details>

<details>
<summary>2. REST의 기본 개념</summary> </br>

**1) Resource (자원)** </br>

REST는 모든 데이터를 자원(Resource)으로 본다. </br>
이 자원은 `URI(또는 URL)`로 표현된다. </br>

예시) </br>

`/users` </br>
`/posts` </br>
`/comments` </br>

URI에는 동사가 아닌 `명사`를 사용해야 한다. </br>

❌ `/getUser` </br>
⭕ `/users` </br>

**2) Representation (표현)** </br>

클라이언트는 자원의 실제 데이터가 아니라, </br>
자원의 표현(Representation)을 전달받는다. </br>

보통 `JSON 형식`을 많이 사용하지만, </br>
XML 등 다양한 형식으로도 표현할 수 있다. </br>

**3) HTTP Method (행위)** </br>

자원에 대한 행위는 HTTP 메서드로 구분한다. </br>

- GET : 조회 </br>
- POST : 생성 </br>
- PUT : 전체 수정 </br>
- PATCH : 부분 수정 </br>
- DELETE : 삭제 </br>

예시) </br>

`GET /users` → 사용자 조회 </br>
`POST /users` → 사용자 생성 </br>
`PATCH /users/1` → 사용자 일부 수정 </br>
`DELETE /users/1` → 사용자 삭제 </br>

</details>

<details>
<summary>3. REST의 원칙</summary> </br>

**1) Client - Server** </br>

클라이언트와 서버의 역할을 분리한다. </br>

따라서 서로 독립적으로 개발 및 유지보수가 가능하다. </br>

**2) Stateless (무상태성)** </br>

서버는 이전 요청 상태를 저장하지 않는다. </br>

각 요청은 `독립적`으로 처리되어야 한다. </br>

**3) Cacheable (캐시 가능)** </br>

응답은 캐시될 수 있어야 한다. </br>

이를 통해 성능을 향상시킬 수 있다. </br>

**4) Uniform Interface (일관된 인터페이스)** </br>

REST에는 클라이언트와 서버 간에 일관되고 균일한 인터페이스가 필요하다. </br>

- URI는 자원을 식별한다. </br>
- HTTP Method는 행위를 표현한다. </br>
- 일관된 방식으로 통신해야 한다. </br>

**5) Layered System (계층 구조)** </br>

REST API에 연결된 클라이언트는 일반적으로 최종 서버에 직접 연결되어 있는지 아니면 중간에 있는 중개자에 연결되어 있는지 알 수 없다. </br>

따라서 확장성과 보안성을 높일 수 있다. </br>

</details>

<details>
<summary>4. RESTful이란?</summary> </br>

REST 원칙을 잘 지켜 설계된 API를 RESTful API라고 한다. </br>

`REST` = 설계 철학 </br>
`RESTful` = 그 철학을 충실히 따른 상태 </br>

</details>

<details>
<summary>5. RESTful 설계 원칙</summary> </br>

- URI는 명사로 작성한다. </br>
- 행위는 HTTP Method로 구분한다. </br>
- 계층 구조를 고려하여 설계한다. </br>
- HTTP 상태 코드를 정확히 사용한다. </br>
- 일관된 응답 형식을 유지한다. </br>

예시) </br>

`GET /users` → 200 OK </br>
`POST /users` → 201 Created </br>
`DELETE /users/1` → 204 No Content </br>

응답 예시) </br>

성공 </br>
{
  "status": 200,
  "data": { ... }
}

실패 </br>
{
  "status": 400,
  "message": "Bad Request"
}

</details>


<details>
<summary>6. REST의 장점</summary> </br>

1) 확장성 (Scalability) </br>
무상태성 기반 구조로 수평 확장이 용이하다. </br>

2) 유연성 (Flexibility) </br>
다양한 데이터 표현(JSON 등)을 지원한다. </br>

3) 분리 구조 (Decoupling) </br>
클라이언트와 서버를 독립적으로 개발할 수 있다. </br>

4) 경량성 (Lightweight) </br>
HTTP 기반으로 구조가 단순하여 모바일 및 IoT 환경에서도 적합하다. </br>

</details>

---

🔗 참고 </br>
https://cloud.google.com/discover/what-is-rest-api?hl=ko#what-is-rest-api </br>
https://blog.whitemouse.dev/entry/REST-API-완벽-가이드-개념부터-구현까지 </br>
https://blog.postman.com/rest-api-examples/ </br>

🎞️ 이미지 출처 </br>
https://cloud.google.com/discover/what-is-rest-api?hl=ko#what-is-rest-api </br>

