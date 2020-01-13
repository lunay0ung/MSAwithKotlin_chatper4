#### 주요 내용은 [코틀린 마이크로서비스 개발(출판사: 에이콘)]에서 발췌하였음을 밝힙니다. 

# 리액티브 마이크로 서비스 만들기 
## 리액티브 프로그래밍
 우리는 명령형 프로그래밍에 익숙하다. 이런 모델에선 뭔가를 수행하고 결과를 기다리는 동안 대기하면, 프로그램은 블로킹된다. 즉, 데이터를 완전히 얻을 때까지 프로그램이 멈추게 되는 것이다. 이런 블로킹을 우회하기 위해 과거에 널리 사용되던 방법은 가령 데이터를 얻기 위해 별도의 스레드를 생성하는 것이다. 다만 이경우 실제로는 해당 스레드의 작업이 완료될 때까지 스레드를 사용할 수 없으며, 다른 요청을 위해 경우 각각 새로운 스레드를 생성해야 한다. 스레드 풀을 사용할 수도 있지만 결국에는 처리할 수 있는 스레드 수의 한계에 도달하게 된다.

 하지만 리액티브 프로그래밍 모델-넌블러킹 모델을 사용하면 기존의 블로킹 모델보다 더 많은 요청을 처리할 수 있는 고성능 애플리케이션을 구현할 수 있다. 넌블러킹 모델은 단일 결과에만 적용할 수 있는 것이 아니라, 리액티브 데이터 스트림을 구독함으로써 스트림이 흐를 때 받은 데이터를 인쇄하는 기능을 지속적으로 호출할 수 있다. 또한 자원을 더 효율적으로 사용하여 애플리케이션에 필요한 인프라를 줄일 수 있다. 

**리액티브 스트림은 준비되는 즉시 지속적으로 흐르는 데이터의 모음으로, 데이터베이스에서 일부 결과를 쿼리하는 대신 준비될 때마다 결과를 보내기 시작한다고 생각할 수 있다. 많은 최신 데이터베이스 드라이버가 이런 개념을 지원한다.


## 네티 사용하기 

네티는 원래 넌블로킹 io 작업을 수행할 수 있게 하는 클라이언트-서버 프레임워크를 만들려는 아이디어를 가진 Jboss가 개발했다.  
이런 기능을 위해 리액터reactor 패턴의 메시지 기반 구현을 사용한다.  
네티는 http, ssl/tls 또는 dns같은 주요 알고리즘 및 프로토콜을 지원하지만  http/2, 웹소켓, 구글 프로토콜 버퍼 같은 최신 프로토콜도 지원한다.  

### 
- google protocol buffer? https://developers.google.com/protocol-buffers/docs/javatutorial  
> 프로토토콜 버퍼는 구글에서 개발하고 오픈소스로 공개한, 직렬화 데이타 구조 (Serialized Data Structure)이다. C++,C#, Go, Java, Python, Object C, Javascript, Ruby 등 다양한 언어를 지원하며 특히 직렬화 속도가 빠르고 직렬화된 파일의 크기도 작아서 Apache Avro 파일 포맷과 함께 많이 사용된다.
(직렬화란 데이타를 파일로 저장하거나 또는 네트워크로 전송하기 위하여 바이너리 스트림 형태로 저장하는 행위이다.)
> 프로토콜 버퍼는 하나의 파일에 최대 64M까지 지원할 수 있으며, 재미있는 기능중 하나는 JSON 파일을 프로토콜 버퍼 파일 포맷으로 전환이 가능하고, 반대로 프로토콜 버퍼 파일도 JSON으로 전환이 가능하다.  
> 프로토콜 버퍼를 사용하기 위해서는 저장하기 위한 데이타형을 proto file 이라는 형태로 정의한다. 프로토콜 버퍼는 하나의 프로그래밍 언어가 아니라 여러 프로그래밍 언어를 지원하기 때문에, 특정 언어에 종속성이 없는 형태로 데이타 타입을 정의하게 되는데, 이 파일을 proto file이라고 한다.
> 이렇게 정의된 데이타 타입을 프로그래밍 언어에서 사용하려면, 해당 언어에 맞는 형태의 데이타 클래스로 생성을 해야 하는데, protoc 컴파일러로 proto file을 컴파일하면, 각 언어에 맞는 형태의 데이타 클래스 파일을 생성해준다.
출처: [https://bcho.tistory.com/1182](https://bcho.tistory.com/1182) [조대협의 블로그]
