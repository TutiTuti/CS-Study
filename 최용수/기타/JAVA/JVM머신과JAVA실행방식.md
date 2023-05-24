## JVM ( JAVA Virtual Machine ) 
JVM은 자바 프로그램 실행환경을 만들어주는 소프트웨어이며, 메모리 관리(GC)를 수행하며 스택 기반의 가상머신이다.     
JVM은 자바 애플리케이션을 클래스 로더를 통해 읽어 자바 API와 함께 실행할 수 있도록 한다.      
자바코드를 컴파일하여 .class의 바이트 코드로 만들면 이코드가 자바 가상 머신 환경에서 실행된다.     
### JVM의 구조
![img1 daumcdn](https://github.com/kj-cs-study/CS-Study/assets/37789623/66b46343-427b-4b08-9531-5bf81505b58b)       
> -  JVM의 구조는 Class Loader, Execution engine, Runtime Data Area, JNI, Native Method Library로 이루어져 있다.      
> > - Class Loader : JVM 내에 클래스를 로드하고 링크를 통해 배치하는 작업을 수행하는 모듈     
> > - Excytuib engine : 바이트 코드를 실행시키는 역활
> > > - 인터프리터 : 바이트 코드를 한 줄씩 실행한다.
> > > - JIT컴파일러 : 인터프리터의 효율을 높이기 위한 컴파일러로 인터프리터가 반복되는 코드를 발견하면 네이티브 코드로 바꿔준다.
> > > - GC(Garbage Collector) : 힙영역에서 사용되지 않은 객체들을 제거하는 작업을 의미한다.
> > - Runtime Data Areas : 프로그램 실행중에 사용되는 다양한 영역이다.
> > > - PC Register : Thread가 시작될 때 생성되며 현재 수행 중인 JVM의 명령어 주소를 가지고 있다.
> > > - Stack Area : 지역변수, 파라미터 등이 생성되는 영역이며 실제 객체는 Heap에 할당되고 해당 레퍼런스만 Stakc에 저장된다.
> > > - Heap Area : 동적으로 생성된 오브젝트와 배열이 저장되는 곳으로 GC의 대상 영역이다.
> > > - Method Area : 클래스 멤버 변수, 메소드 정보, Type 정보, Constant Pool, static, final변수 등이 생성된다.
> > - JNI(Java Native Interface) : 자바 애플리케이션에서 C,C++,어셈블리어로 작성된 함수를 사용할 수 있는 방법을 제공한다. Native키워드를 사용해 메서드를 호출한다.  
> > - Natice Method Library : C,C++로 작성된 라이브러리다. 자바 이외의 언어로 작성된 네이티브 코드를 실행할 떄 사용되는 메모리 영역으로 일반적인 C스택을 사용한다.
### JAVA의 실행방식
1. 자바로 개발된 프로그램을 실행하면 JVM은 OS로 부터 메모리를 할당한다.
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 자바 바이트코드(.class)로 컴파일 한다.
3. Class Loader를 통해 JVM Runtime Data Area로 로딩한다.
4. Runtime Data Area 에 로딩된 .class는 Execution Engine을 통해 해석한다.
5. 해석된 바이트 코드는 Runtime Data Area의 각 영역에 배치되어 수행되며, 이 과정에서 Execution engine에 의해 GC 작동과 스레드의 동기화가 이루어진다.

