# ☕ 09. Java 심화 (JVM & GC)

<details>
<summary>1. JVM(Java Virtual Machine)의 탄생 배경과 역할 </summary> </br>

❶ 탄생 배경 </br>

"한 번 쓰고, 어디서든 실행한다 (Write Once, Run Anywhere)" </br>
과거의 언어(C, C++)는 윈도우에서 짠 프로그램을 리눅스에서 돌리려면 코드를 수정하고 다시 컴파일해야 했다. </br>
하지만 자바는 JVM이라는 가상 머신을 중간에 두어 이 문제를 해결했다. </br>
개발자는 OS에 상관없이 자바 코드만 짜면, 각 운영체제에 설치된 JVM이 이를 해석해서 실행한다. </br>

</br>

❷ JVM의 핵심 기능 </br>

- 바이트코드 실행: 자바 컴파일러가 만든 .class 파일을 읽어 기계어로 번역하고 실행한다. </br>

- 메모리 관리 (중요): 프로그램이 사용하는 메모리를 할당하고, 더 이상 안 쓰는 메모리를 알아서 수거한다. </br>

- 보안: 실행 중에 코드의 안전성을 검사하여 시스템에 해를 끼치지 않도록 방어막 역할을 한다.

</details>

<details>
<summary>2. Runtime Data Areas: JVM 메모리 구조 분석 </summary> </br>

자바 프로그램이 실행될 때 JVM이 OS로부터 할당받는 메모리 영역이다. 크게 공유 영역과 개별 영역으로 나뉜다. </br>

</br>

❶ Method Area (공유): </br>

모든 스레드가 공유하는 공간. </br>

클래스 정보(이름, 필드, 메서드), 전역 변수(Static), 상수(Literal)가 저장된다. 프로그램 시작부터 끝까지 유지된다. </br>

</br>

❷ Heap Area (공유): ⭐ 핵심 영역 </br>

new 키워드로 생성된 모든 **객체(인스턴스)** 와 배열이 저장되는 곳이다. </br>

가비지 컬렉터(GC)의 주요 청소 대상이다. 싱글톤 빈도 여기에 저장되어 공유된다. </br>

</br>

❸ Stack Area (개별): </br>

각 스레드(사용자)마다 하나씩 생성된다. </br>

메서드가 호출될 때마다 '프레임'이 쌓이며, 그 안에는 지역 변수와 매개변수가 들어있다. </br>

메서드가 종료되면 즉시 사라지기 때문에 다른 사용자(스레드)와 섞일 일이 없어 안전하다. </br>

</br>

❹ PC Register & Native Method Stack (개별): </br>

PC Register는 현재 실행 중인 JVM 명령의 주소를 기록한다. </br>

Native Method Stack은 자바가 아닌 C/C++ 등으로 작성된 코드를 실행할 때 사용한다.

</details>

<details>
<summary>3. 가비지 컬렉션 (Garbage Collection, GC) 원리 </summary> </br>

❶ 자동 메모리 관리 시스템 </br>
자바는 개발자가 직접 메모리를 지우지 않는다. </br>
대신 GC가 더 이상 어느 누구에게도 참조되지 않는(사용되지 않는) 객체를 찾아서 메모리에서 제거한다. </br>

</br>

❷ Mark and Sweep 알고리즘 </br>

- Mark (표시): JVM이 루트 객체(Stack의 변수 등)부터 시작해서 연결된 모든 객체를 따라가며 "사용 중"이라고 표시한다. </br>

- Sweep (삭제): 표시되지 않은 객체들을 메모리에서 삭제한다. </br>

- Compact (압축): (알고리즘에 따라) 삭제 후 비어있는 공간들을 메우기 위해 객체들을 한곳으로 모아 메모리 조각화를 방지한다. </br>

</br>

🌟 Stop-the-world </br>
: GC를 실행하기 위해 JVM이 애플리케이션 실행을 잠시 멈추는 현상이다. 이 멈추는 시간을 줄이는 것이 GC 튜닝의 핵심이다. </br>

</details>

<details>
<summary>4. Heap 영역의 세대 구분 (Generational GC) </summary> </br>

대부분의 객체는 금방 생성되었다가 사라진다는 가설(Weak Generational Hypothesis)을 바탕으로 힙을 나눈다. </br>

- Young Generation: 새롭게 생성된 객체들이 머무는 곳. </br>

- Minor GC: 여기서 일어나는 청소. 속도가 매우 빠르고 자주 일어난다. 여기서 살아남은 객체는 'Age' 값이 올라간다. </br>

- Old Generation: Young 영역에서 여러 번의 GC를 견디고 살아남은 '장수 객체'들이 이동하는 곳. </br>

- Major GC (Full GC): 여기서 일어나는 청소. </br>
Young 영역보다 크기가 크기 때문에 청소 시간이 오래 걸리고 서버가 잠시 멈추는 현상이 체감될 수 있다. </br>

</details>

<details>
<summary>5. 자바 프로그램의 컴파일 및 실행 과정 </summary> </br>

❶ 소스 코드 작성: 개발자가 .java 파일을 만든다. </br>

</br>

❷ 컴파일: 자바 컴파일러(javac)가 소스 코드를 JVM이 이해할 수 있는 **바이트코드(.class)**로 변환한다. </br>

</br>

❸ 클래스 로딩: ClassLoader가 필요한 클래스 파일들을 메모리(Method Area)에 올린다. </br>

</br>

❹ 실행 (Execution Engine): </br>

  - Interpreter: 바이트코드를 한 줄씩 기계어로 번역해서 실행한다. </br>

  - JIT(Just-In-Time) 컴파일러: 자주 반복되는 코드를 미리 기계어로 번역해 캐시에 저장해둔다. </br>
  이 덕분에 자바의 실행 속도가 비약적으로 빨라졌다.
  

</details>

<details>
<summary>6. 정리: 왜 백엔드 개발자가 이걸 알아야 하는가? </summary> </br>

- 메모리 효율성: 08번에서 배운 싱글톤 빈이 왜 효율적인지(Heap에 하나만 두고 공유), </br>
  왜 무상태여야 하는지(필드 변수는 공유되는 Heap에 있기 때문)를 기술적으로 증명할 수 있다. </br>


- 장애 대응: 서버가 갑자기 느려지거나 다운될 때, 로그를 보고 "Heap 메모리가 부족하네?" </br>
  혹은 "GC가 너무 오래 걸리네?" 같은 근본적인 원인을 파악할 수 있다. </br>


- 성장판: 단순히 도구를 쓰는 법을 넘어, 그 도구가 돌아가는 원리를 이해하는 '엔지니어'로 성장하기 위한 필수 지식이다.

</details>

---

🔗 참고 </br>
Oracle Java Documentation_ JVM Architecture </br>
https://docs.oracle.com/javase/specs/jvms/se17/html/index.html </br>
