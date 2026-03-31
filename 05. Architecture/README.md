# 🏗️ 05. Architecture
<details>
<summary>1. 백엔드 아키텍처란?</summary> </br>

백엔드 아키텍처란 클라이언트의 요청을 처리하고, 데이터베이스와 연동하여 응답을 반환하는 전체 구조를 의미한다. </br>
단순히 기능이 동작하는 것이 아니라, **유지보수성과 확장성을 고려한 구조 설계**가 중요하다. </br>
즉, 역할을 나누고 책임을 분리하여 효율적으로 시스템을 구성하는 것이 핵심이다.

</details>

<details>
<summary>2. MVC 패턴</summary> </br>

MVC(Model - View - Controller)는 웹 애플리케이션을 구성하는 대표적인 아키텍처 패턴이다. </br>
각 역할을 분리하여 코드의 재사용성과 유지보수성을 높인다. </br>

❶ Model </br>
- 애플리케이션의 데이터와 비즈니스 로직을 담당한다. </br>
- DB와 직접적으로 연결되며 데이터를 처리하고 관리하는 역할을 한다. </br>

❷ View </br>
- 사용자에게 보여지는 화면(UI)을 담당한다. </br>
- 백엔드에서는 주로 JSON 형태로 데이터를 응답한다. </br>

❸ Controller </br>
- 클라이언트의 요청을 받아 처리 흐름을 제어한다. </br>
- Service 계층을 호출하고 결과를 응답으로 반환한다. </br>

</details>

<details>
<summary>3. 계층형 구조 (Layered Architecture)</summary> </br>

백엔드에서는 MVC를 기반으로 더 세분화된 **계층형 구조**를 사용한다. </br>
일반적인 구조는 다음과 같다. </br>

📦 Controller → Service → DAO(Repository) → DB

</br>

❶ Controller </br>
- 클라이언트의 요청(Request)을 받는다. </br>
- 요청 데이터를 DTO로 변환한다. </br>
- Service 계층에 처리를 위임한다. </br>

❷ Service </br>
- 핵심 비즈니스 로직을 수행한다. </br>
- 여러 DAO를 조합하거나 트랜잭션을 관리한다. </br>
- Controller와 DAO 사이의 중간 역할을 한다. </br>

❸ DAO (Repository) </br>
- 데이터베이스와 직접적으로 통신한다. </br>
- SQL 실행 및 데이터 조회/저장을 담당한다. </br>

❹ Database </br>
- 실제 데이터를 저장하는 공간이다. </br>

</details>

<details>
<summary>4. 요청 처리 흐름</summary> </br>

사용자가 API를 호출했을 때의 전체 흐름은 다음과 같다. </br>

1️⃣ 클라이언트가 HTTP 요청을 보낸다. </br>

</br>

2️⃣ Controller가 요청을 수신한다. </br>

</br>

3️⃣ Controller는 Service 계층에 처리를 위임한다. </br>

</br>

4️⃣ Service는 비즈니스 로직을 수행하고 DAO를 호출한다. </br>

</br>

5️⃣ DAO는 DB에 접근하여 데이터를 조회하거나 저장한다. </br>

</br>

6️⃣ 결과가 Service → Controller로 전달된다. </br>

</br>

7️⃣ Controller가 최종 응답(Response)을 반환한다. </br>

</br>

👉 흐름 요약 </br>

Client → Controller → Service → DAO → DB → Service → Controller → Response

</details>

<details>
<summary>5. 계층을 나누는 이유</summary> </br>

계층형 구조를 사용하는 이유는 다음과 같다. </br>

1️⃣ 유지보수성 향상 </br>
각 계층이 역할별로 분리되어 있어 수정이 쉽다. </br>

</br>

2️⃣ 재사용성 증가 </br>
Service 로직을 여러 Controller에서 재사용할 수 있다. </br>

</br>

3️⃣ 확장성 </br>
기능이 추가되더라도 기존 구조를 유지하면서 확장이 가능하다. </br>

</br>

4️⃣ 책임 분리 (SRP) </br>
각 계층이 하나의 역할만 담당하도록 하여 코드의 가독성과 안정성을 높인다. </br>

</br>

5️⃣ 효율적인 자원 관리 (Singleton) </br>

- 각 계층(Controller, Service, Repository)의 객체는 서버가 시작될 때 딱 하나만 생성되어 모든 요청이 공유하는 **싱글톤(Singleton)** 방식으로 관리된다. </br>

- 이를 통해 수많은 사용자가 동시에 접속해도 매번 객체를 생성하지 않아 메모리 부하를 획기적으로 줄일 수 있다. </br>

- 단, 싱글톤 객체는 여러 명이 공유하므로 내부에 상태를 저장하지 않는 **무상태(Stateless)** 로 설계해야 안전하다. </br>

</details>

<details>
<summary>6. DTO (Data Transfer Object)</summary> </br>

DTO는 계층 간 데이터 전달을 위한 객체이다. </br>

- Controller ↔ Service 간 데이터 전달 </br>

- 클라이언트와 서버 간 데이터 교환 </br>

엔티티(Entity)와 분리하여 사용하는 이유는 다음과 같다. </br>

- API 응답 구조를 자유롭게 설계할 수 있다. </br>

- 민감 정보 노출 방지 (보안) </br>

- 유지보수 용이성 </br>

</details>

<details>
<summary>7. 정리</summary> </br>

백엔드 아키텍처는 단순한 기능 구현이 아니라, **구조를 설계하는 것 자체가 중요한 역할**이다. </br>

MVC 패턴으로 기본 구조를 나누고 Controller → Service → DAO 계층으로 역할을 분리하며 </br>
요청 흐름을 명확하게 관리하는 것이 핵심이다. </br>

</details>

<details>
<summary>🔥 핵심 면접 질문 리스트 🔥 </summary></br>

**Q1. 계층형 아키텍처(Layered Architecture)를 사용하는 이유는 무엇인가요?** </br>

답변: "가장 큰 이유는 '책임의 분리(Separation of Concerns)' 입니다. </br>
각 계층이 자신의 역할에만 집중하게 함으로써 코드의 가독성을 높이고, </br>
특정 기능을 수정할 때 다른 계층에 미치는 영향을 최소화하여 유지보수성을 극대화할 수 있기 때문입니다. </br>
또한, 비즈니스 로직이 담긴 Service 계층을 여러 Controller에서 재사용할 수 있다는 장점도 있습니다." </br>

</br>

**Q2. Controller와 Service의 역할을 명확히 구분해서 설명해 주세요.** </br>

답변: "Controller는 클라이언트의 접점으로, 요청을 받고 응답을 반환하는 '문지기' 역할을 합니다. </br>
주로 요청 데이터의 유효성 검증과 응답 형식 결정을 담당합니다. </br>
반면 Service는 애플리케이션의 핵심인 '비즈니스 로직'을 처리하는 곳입니다. </br>
여러 데이터 저장소(Repository)를 조합하거나 트랜잭션을 관리하며 </br>
실제 서비스가 어떻게 돌아갈지를 결정하는 두뇌 역할을 합니다." </br>

</br>

**Q3. DB에 직접 접근하는 Entity 대신 DTO를 따로 사용하는 이유는 무엇인가요?** </br>

답변: "두 가지 큰 이유가 있습니다. 첫째는 보안입니다. </br>
DB 구조를 그대로 담은 Entity를 노출하면 비밀번호 같은 민감한 정보가 나갈 위험이 있습니다. </br>
둘째는 결합도 낮추기입니다. 화면에 보여줄 데이터 형식은 자주 변하는데, </br>
그때마다 DB 테이블 구조인 Entity를 수정할 수는 없습니다. </br>
DTO를 두어 API 스펙이 변해도 DB 구조는 안정적으로 유지할 수 있게 설계하는 것이 정석입니다." </br>

</br>

**Q4. 서비스 계층(Service)에서 트랜잭션을 관리해야 하는 이유는 무엇인가요?** </br>

답변: "비즈니스 로직의 '원자성' 을 보장하기 위해서입니다. </br>
예를 들어 '송금' 기능은 내 계좌에서 돈을 빼는 작업과 상대 계좌에 돈을 넣는 작업이 모두 성공해야 합니다. </br>
만약 하나만 성공하고 서버가 꺼지면 큰 문제가 생깁니다. </br>
따라서 여러 DB 작업이 묶인 비즈니스 단위인 Service 계층에서 트랜잭션을 걸어, </br>
하나라도 실패하면 전체를 취소(Rollback)할 수 있도록 관리해야 합니다." </br>

</br>

**Q5. 싱글톤(Singleton) 패턴으로 객체를 관리할 때 주의할 점은 무엇인가요?** </br>

답변: "싱글톤 객체는 서버 내에 딱 하나만 존재하고 모든 사용자가 공유하기 때문에, </br>
내부적으로 상태를 가지지 않는 '무상태(Stateless)' 로 설계해야 합니다. </br>
만약 객체 안에 특정 사용자의 데이터를 변수로 저장하게 되면, </br>
다른 사용자의 요청 처리 중에 데이터가 꼬이는 심각한 동시성 문제가 발생할 수 있습니다. </br>
따라서 공유되는 필드 변수 없이 메서드 파라미터나 지역 변수만 사용하는 것이 안전합니다." </br>

</br>

**Q6. 백엔드 요청 처리 흐름을 '로그인' 기능에 빗대어 설명해 보세요.** </br>

답변: "사용자가 아이디/비번을 치면 </br>
1. Controller가 요청을 받아 데이터 형식을 확인하고, </br>
2. Service에 로그인을 시도하라고 시킵니다. </br>
3. Service는 4. Repository(DAO) 에 해당 아이디의 유저 정보를 찾아달라고 요청하고, </br>
5. DB에서 가져온 암호화된 비번과 입력된 비번을 비교합니다. </br>
비교 결과가 맞다면 Service는 로그인 성공 결과를 Controller에 돌려주고, </br>
마지막으로 6. Controller가 성공 메시지나 토큰을 담아 클라이언트에게 응답합니다." </br>

</br>

</details>

---

🔗 참고 </br>
Google Gemini_ 아키텍쳐 </br>

