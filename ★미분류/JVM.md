# JVM(Java Virtual Machine)

Java로 개발한 프로그램을 컴파일하여 만들어지는 바이트코드를 실행시키기 위한 가상머신 <br><br>
운영체제(OS)에 상관없이 JAVA 애플리케이션을 실행 할 수 있도록 해준다.

<br>

![JVM](https://github.com/yumalg12/tech-study/assets/134472265/4cc89623-4366-4c00-a7f6-f17691e928c4)



### JVM 구성 요소

1. **Class Loader** : 런타임 시점에 클래스를 로딩하게 해주며 클래스의 인스턴스를 생성하면 클래스 로더를 통해 메모리에 로드한다.

2. **Runtime Data Areas** : JVM이 프로그램을 수행하기 위해서 운영체제(OS)로부터 별도로 할당 받은 메모리 공간으로 크게 5가지 영역으로 나눈다.

    - PC Register : 스레드가 어떤 부분을 어떤 명령으로 실행해야할 지에 대한 기록을 하는 부분으로 현재 수행중인 JVM 명령의 주소를 가진다.

    - JVM Stack : 메서드의 매개변수, 지역변수, return 주소, 임시변수 등의 정보를 기록하는 스택
각 스레드 별로 생성되기 때문에 다른 스레드는 접근할 수 없으며 메서드 호출이 종료되면 스택에서 정보들이 제거된다.

    - Native Method Stack : 기계어로 작성된 프로그램을 실행시키는 영역.
자바 외의 언어로 작성된 네이티브 코드들을 위한 스택이다.

    - Method Area : 클래스 정보를 처음 메모리 공간에 올릴 때 초기화되는 대상을 저장하기 위한 메모리 공간.
모든 쓰레드가 공유하는 메모리 영역으로 클래스, 인터페이스, 메서드, 필드, Static 변수 등의 바이트 코드를 보관한다.

    - Heap : 프로그램 상에 런타임 시에 동적으로 할당하여 사용하는 영역이다. 클래스를 이용해 객체를 생성하면 힙에 저장된다.

<br>

3. **Execution Engine(실행 엔진)** : 클래스를 실행시키는 역할로, 로드된 클래스의 바이트코드를 실행하는 런타임 모듈이 바로 실행 엔진이다.
자바 바이트 코드를 명령어 단위로 읽어 실행하는데, Interpreter방식과 JIT Compiler방식을 사용한다.

```

Interpreter(인터프리터) : 자바 바이트 코드를 명령어 단위로 읽어서 실행한다. 한줄씩 수행하므로 수행 속도가 느리다는 단점이 있다.

JIT Compiler : 바이트코드를 컴파일하여 네이티브 코드로 변환하여 사용한다. 

```

<br>

4. **Garbage Collector** : 유효하지 않은 메모리인 가비지를 정리해주는 역할

<br><br>

### JVM에서의 실행과정
1. Class Loader를 통해 .class 파일들을 JVM에 올린다.
2. JVM에 있는 .class 파일들을 Execution Engine의 Interpreter와 JIT Compiler를 통해 해석된다.
3. 해석된 바이트 코드는 Runtime Data Areas에 배치되어 실질적인 수행이 이루어진다. 

<br>

<hr>
<br>

[출처]
- https://code-lab1.tistory.com/92
- https://kingofbackend.tistory.com/123
