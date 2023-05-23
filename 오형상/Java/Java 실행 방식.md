
### Java의 실행방식

1️⃣ 자바로 개발된 프로그램을 실행하면 JVM은 OS로 부터 메모리를 할당한다.
2️⃣ 자바 컴파일러(javac)가 자바 소스코드(.java)를 자바 바이트코드(.class)로 컴파일 한다.
3️⃣ Class Loader를 통해 JVM Runtime Data Area로 로딩한다.
4️⃣ Runtime Data Area 에 로딩된 .class는 Execution Engine을 통해 해석한다.
5️⃣ 해석된 바이트 코드는 Runtime Data Area의 각 영역에 배치되어 수행되며, 이 과정에서 Execution engine에 의해 GC 작동과 스레드의 동기화가 이루어진다.
