
# ⚙️ 02. REST 

<details>
<summary>1. REST란?</summary> </br>

REST(Representational State Transfer)는 웹에서 자원(Resource)을 효율적으로 주고받기 위한 아키텍처 스타일이다. </br>

즉, API를 설계할 때 지켜야 하는 `설계 원칙`이라고 볼 수 있다. </br>

REST는 `HTTP 프로토콜의 특징을 기반`으로 만들어졌으며, 웹의 기본 구조인 `요청(Request) - 응답(Response)` 방식을 따른다. </br>

</details>

<details>
<summary>2. REST의 기본 개념</summary> </br>

**1) Resource (자원)** </br>

REST는 모든 데이터를 `자원(Resource)`으로 본다. </br>

이 자원은 `URI(또는 URL)`로 표현된다. </br>

예시) </br>

- `/users` </br>
- `/posts` </br>
- `/comments` </br>

URI에는 동사가 아닌 `명사`를 사용해야 한다. </br>

❌ `/getUser` </br>
⭕ `/users` </br>

</br>

**2) Representation (표현)** </br>

클라이언트는 자원의 실제 데이터(DB Entity)가 아니라, 보안과 효율을 위해 가공된 `자원의 표현(Representation, 보통 DTO 사용)`을 전달받는다. </br>

보통 `JSON 형식`을 많이 사용하지만, XML 등 다양한 형식으로도 표현할 수 있다. </br>

</br>

**3) HTTP Method (행위)** </br>

자원에 대한 행위는 `HTTP 메서드`로 구분한다. </br>

- GET : `조회` </br>
- POST : `생성` </br>
- PUT : `전체 수정` </br>
- PATCH : `부분 수정` </br>
- DELETE : `삭제` </br>

예시) </br>

- `GET /users` → 사용자 조회 </br>
- `POST /users` → 사용자 생성 </br>
- `PATCH /users/1` → 사용자 일부 수정 </br>
- `DELETE /users/1` → 사용자 삭제 </br>

</details>

<details>
<summary>3. REST의 원칙</summary> </br>

**1) Client - Server** </br>

클라이언트와 서버의 역할을 분리한다. </br>

따라서 서로 `독립적으로 개발 및 유지보수가 가능하다`. </br>

</br>

**2) Stateless (무상태성)** </br>

서버는 이전 요청 상태를 저장하지 않는다. </br>

각 요청은 `독립적`으로 처리되어야 한다. </br>

</br>

**3) Cacheable (캐시 가능)** </br>

응답은 `캐시`될 수 있어야 한다. </br>

이를 통해 성능을 향상시킬 수 있다. </br>

</br>

**4) Uniform Interface (일관된 인터페이스)** </br>

REST에는 클라이언트와 서버 간에 일관되고 균일한 인터페이스가 필요하다. </br>

- `URI`는 `자원을 식별`한다. </br>
- `HTTP Method`는 `행위를 표현`한다. </br>
- 일관된 방식으로 통신해야 한다. </br>

</br>

**5) Layered System (계층 구조)** </br>

REST API에 연결된 클라이언트는 일반적으로 최종 서버에 직접 연결되어 있는지 아니면 중간에 있는 중개자에 연결되어 있는지 알 수 없다. </br>

따라서 `확장성과 보안성을 높일 수 있다.` </br>

</details>

<details>
<summary>4. RESTful이란?</summary> </br>

REST 원칙을 잘 지켜 설계된 API를 RESTful API라고 한다. </br>

- `REST` = 설계 철학 </br>

- `RESTful` = 그 철학을 충실히 따른 상태 </br>

</details>

<details>
<summary>5. RESTful 설계 원칙</summary> </br>

- URI는 `명사로 작성`한다. </br>

- URI 마지막에 슬래시(/)를 포함하지 않는다. </br>
  또한, 가독성을 위해 **하이픈(-)** 은 사용 가능하지만, **언더바(_)** 는 사용하지 않는다. </br>
  
- `행위는 HTTP Method로 구분한다.` </br>

- 계층 구조를 고려하여 설계한다. </br>

- `HTTP 상태 코드`를 정확히 사용한다. </br>

- 일관된 응답 형식을 유지한다. </br>

예시) </br>

- `GET /users` → 200 OK </br>

- `POST /users` → 201 Created </br>

- `DELETE /users/1` → 204 No Content </br>

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

❶ 확장성 (Scalability) </br>
무상태성 기반 구조로 수평 확장이 용이하다. </br>

❷ 유연성 (Flexibility) </br>
다양한 데이터 표현(JSON 등)을 지원한다. </br>

❸ 분리 구조 (Decoupling) </br>
클라이언트와 서버를 독립적으로 개발할 수 있다. </br>

❹ 경량성 (Lightweight) </br>
HTTP 기반으로 구조가 단순하여 모바일 및 IoT 환경에서도 적합하다. </br>

</details>

<details>
<summary>🔥 핵심 면접 질문 리스트 🔥 </summary></br>

**Q1. REST API란 무엇인가요?** </br>
 
답변: "REST는 HTTP 프로토콜의 장점을 최대한 활용하기 위해 만들어진 아키텍처 스타일(설계 원칙) 입니다. </br>
모든 데이터를 '자원(Resource)' 으로 간주하고, 이를 고유한 URI로 식별하며, </br>
HTTP 메서드(GET, POST, PUT 등)를 통해 해당 자원에 대한 행위를 정의하는 방식입니다." </br>

</br>

**Q2. 'RESTful'하다는 것은 구체적으로 어떤 의미인가요?** </br>

답변: "REST의 설계 원칙을 충실히 지킨 API를 의미합니다. </br>
가장 대표적으로는 URI에 동사가 아닌 명사를 사용하고(예: /getUsers 대신 /users), </br>
행위는 HTTP 메서드로만 표현하며, 상황에 맞는 HTTP 상태 코드를 정확히 반환하는 것을 의미합니다. </br>
이러한 규칙을 지키면 API의 가독성이 좋아지고 누구나 쉽게 이해할 수 있는 인터페이스가 됩니다." </br>

</br>

**Q3. REST의 '무상태성(Stateless)'이 주는 이점이 무엇인가요?** </br>

답변: "서버가 클라이언트의 상태를 저장하지 않기 때문에, 서버의 확장성(Scalability) 이 매우 좋아집니다. </br>
클라이언트의 요청이 어떤 서버로 전달되더라도 독립적으로 처리할 수 있기 때문에, </br>
트래픽이 늘어날 때 서버를 여러 대 늘리는 '스케일 아웃' 환경에서 매우 유리합니다." </br>

</br>

**Q4. URI 설계 시 가장 중요하게 생각하는 원칙이 있다면 무엇인가요?** </br>

답변: "가장 중요한 것은 '직관성' 이라고 생각합니다. </br>
URI만 보고도 어떤 자원을 다루는지 알 수 있도록 명사 위주로 구성해야 하며, </br>
계층 구조를 나타낼 때는 슬래시(/)를 사용하되 가독성을 위해 하이픈(-)을 적절히 활용해야 합니다. </br>
또한 마지막에 슬래시를 넣지 않는 것과 같은 세밀한 규칙을 지켜 일관성을 유지하는 것이 중요합니다." </br>

</br>

**Q5. REST API에서 JSON 형식을 주로 사용하는 이유는 무엇인가요?** </br>

답변: "JSON은 텍스트 기반이라 사람이 읽기 쉽고, XML에 비해 구조가 단순하여 데이터 크기가 작고 가볍기 때문입니다. </br>
또한 대부분의 프로그래밍 언어와 브라우저에서 기본적으로 지원하기 때문에 데이터를 주고받기에 가장 효율적인 형식입니다." </br>

</br>

**Q6. REST API의 단점은 무엇이고, 이를 어떻게 보완할 수 있을까요?** </br>

답변: "정해진 규칙이 엄격하다 보니, 때로는 불필요하게 많은 데이터를 받게 되거나(Over-fetching), </br>
반대로 필요한 데이터를 얻기 위해 여러 번 요청해야 하는 경우(Under-fetching)가 생길 수 있습니다. </br>
이를 보완하기 위해 실무에서는 응답 필드를 제한하거나, 특수한 경우에는 GraphQL 같은 대안을 고려하기도 합니다." </br>

</br>

</details>

---

🔗 참고 </br>
https://cloud.google.com/discover/what-is-rest-api?hl=ko#what-is-rest-api </br>
https://blog.whitemouse.dev/entry/REST-API-완벽-가이드-개념부터-구현까지 </br>
https://blog.postman.com/rest-api-examples/ </br>

🎞️ 이미지 출처 </br>
https://cloud.google.com/discover/what-is-rest-api?hl=ko#what-is-rest-api </br>

