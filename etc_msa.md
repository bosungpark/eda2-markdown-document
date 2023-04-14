이벤트기반 아키텍처 구축하기...우아한 형제들
=

하나의 시스템에 존재하던 두 도메인의 물리적인 분리.

느슨한 결합을 가져감으로써 타 시스템에 대한 의존과 영향도를 줄이고 각 시스템의 목적에 집중함으로써 강한 응집을 갖는 시스템을 만들 수 있습니다. Event Driven 은 이를 돕는다.

물리적인 시스템의 분리로 인해 코드 레벨의 호출이 동기적인 HTTP 통신으로 변하나 여전히 대상 도메인을 호출해야한다는 의도가 남아있기 때문에 물리적인 시스템 분리만으로는 결합이 느슨해졌다고 볼 수는 없다.

물리적인 의존을 제거하는 방법으로 쉽게 떠올릴 수 있는 것은 비동기 방식이 있다. 대표적인 비동기 방식으로는 별도 스레드를 통한 HTTP 방식과 메시징 시스템을 이용한 방식이다.

HTTP 방식은 별도의 스레드를 통해, 주 흐름과의 직접적인 결합은 피할 수 있다는 장점이 있지만, 상 도메인을 호출한다는 의도가 남아있다.

메시징시스템 역시 이를 사용하는 아키텍처가 항상 느슨한 결합을 보장하지는 않는다.

메시지를 발송하는 것으로 물리적인 의존이 제거되지만 결합은 느슨해지지 않는다.

메시징 시스템으로 보낸 메시지가 대상 도메인에게 기대하는 목적을 담았다면, 이것은 이벤트가 아닌 메시징 시스템을 이용한 비동기 요청일 뿐이다.

우리가 발행해야할 이벤트는 도메인 이벤트로 인해 달성하려는 목적이 아닌 도메인 이벤트 그 자체다.

마이크로서비스 아키텍처의 장단점...pop it
=
모놀리스 방식의 소프트웨어에서는 주로 3계층(3-tier) 아키텍처를 사용 합니다.

프리젠테이션 계층 > 비즈니스 계층 > 데이터 접근 계층

이때, 모든 코드는 같은 코드베이스에 위치하며 하나의 단위로 배포 됩니다.

마이크로서비스 아키텍처는 다른 서비스에 의존성이 없고 배포와 관리를 단독으로 할 수 있는 수준에서 제품 또는 프로젝트를 독립적인 서비스로 나누라고 이야기합니다.

장점
 - 마이크로서비스에서는 각 서비스는 독립적이고 새로운 프로젝트이며 요구사항에 맞는 어떠한 언어든지 사용해서 개발될 수 있습니다.
 - 특정 서비스만 집중하기 때문에 코드 저장소는 매우 작을 것이고 개발자는 코드를 잘 알고 있을 것입니다.
 - 서비스가 다른 서비스와 통신할 필요가 있을때 API를 통해(구체적으로 REST 서비스에 의해) 서비스들은 통신할 수 있습니다.
 - 중앙화된 데이터베이스가 없습니다. 


단점
- 서비스가 장애가 나는 경우 장애를 추적하는 것은 힘든 작업이 될 수 있습니다.
-  각 서비스는 모놀리스 소프트웨어의 프로세스간 통신에 비해 좀 더 큰 오버헤드를 가진 API/원격 호출을 통해 통신합니다.

마이크로서비스 아키텍처. 그것이 뭣이 중헌디?...pop it
=
마이크로서비스 아키텍처는 하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처를 말합니다. 애플리케이션을 특화된 기능별로 나누게 되면 자연스럽게 애플리케이션의 추상화(abstraction)가 가능해집니다. 

 일반적으로 다음의 항목들 중에서 대부분이 현재 상황에 해당한다고 생각되면 마이크로서비스 아키텍처 패턴에 대해서 고민을 시작해 보는 것도 나쁘지 않습니다.

1. 애플리케이션의 배포에 한 시간 이상 소요된다.
2. 단순한 기능 하나를 수정해도 전체 기능에 대한 QA가 필요하다.
3. 단순한 버그 수정이 더 중대한 버그를 생산하는 일이 많아졌다.
4. 현재의 애플리케이션을 기능별로 나눈다고 가정했을 때 수십개의 마이크로서비스가 가능하다.

서비스 복잡도가 증가하면서 모놀리틱 아키텍처가 가지는 문제점들은 배포 시간의 증가, 부분적 스케일 아웃의 어려움, 안정성의 감소 등 여러가지가 있습니다. 그 중에서도 굳이 한가지를 꼽자면 애플리케이션을 구성하는 프로그래밍 언어, 또는 프레임워크의 변경이 거의 불가능에 가까울 정도로 어렵다는 점 입니다.

마이크로서비스 아키텍처 패턴은 그 이름에서도 유추할 수 있듯이 모놀리틱 아키텍처로 구성된 하나의 큰 서비스를 독립적인 역할을 수행하는 작은 단위의 서비스로 분리하여 설계하는 패턴을 말합니다. 여기에서 말하는 독립적인 역할이란 주로 기능적인 요소를 의미합니다.

하나의 데이터베이스를 각각의 개별 서비스가 공유해서 사용하는 방식도 가능하지만 마이크로서비스 아키텍처가 가지는 근본적인 장점을 최대한 활용하기 위해서는 서비스별로 별도의 데이터베이스를 사용하는 것이 필요합니다. 

마이크로서비스 아키텍처의 장점
    - 변경이 다른 서비스에 미치는 영향이 적습니다
    - 전체 애플리케이션을 스케일 아웃할 필요가 없기 때문에 불필요한 자원의 낭비를 줄일 수 있습니다.
    - 시스템의 아키텍처가 개발 조직과 나아가서 회사의 조직 문화에 큰 영향을 미친다
마이크로서비스 아키텍처의 장점
    - 서비스 간의 통신에 대한 처리가 추가적으로 필요하다
    - 분산된 데이터베이스는 트랜잭션 관리가 용이하지 않기 때문에 데이터의 정합성을 맞추기 위한 노력이 추가적으로 필요하다.
    - 수 많은 서비스를 배포하고 관리하는 데에 어려움이 있다.

마이크로 서비스는 왜 점점 더 각광을 받을 수 밖에 없을까?...pop it
=
기업의 소프트웨어 시스템 구성이 마이크로 서비스 형태일 때 확실히 사업적으로 민첩해진다

마이크로 서비스는 빠른 시장 진입에 유리하다. 

불필요한 결합을 제거하는 일, 이벤트 드리븐으로 이종 시스템 사이의 정합성을 서서히 맞춰주는 일


우버의 마이크로서비스 적용기 해설...pop it
=
마이크로서비스 적용 목적을 확장성 개선 better scalability에 두고 있습니다. 흥미로운 사실은 확장성Scalability라는 모호한 목표를 구체화 하기 위해 세 가지 지표를 정했습니다. 트래픽 증가 처리(handling growing traffic)와 새로운 기능 추가(adding new features easily) 그리고 조직 성장에 따르는 아키텍처 적용(adopting an architecture that can adapt itself readily to the growth of the organization)이 그 지표입니다.

*MVCS와 UDR 적용 (핵심 매커니즘)*
1. 코드 사이에 존재하는 결합을 줄이기 위해 내린 중요한 설계 결정d esign decisions을 두 가지로 말합니다. 하나는 MVCS 적용인데 이는 널리 알려진 MVC(Model-View-Controller) 패턴에 서비스의 S를 추가한 개념입니다. 데이터 보관을 담당하는 코드를 비즈니스 로직에서 분리하기 위해 MVC에 S를 추가한 것이죠.


2. RDBMS(제품은 PostgreSQL)을 UDR(Uber’s globally replicated datastore)하는 자체 분산 데이터저장소로 바꾼 것입니다.
   
*서비스 확장을 위한 Tornado, TChannel/Hyperbahn, Thrift 적용*
1. 비동기 네트워크 프로그래밍(Asynchronous networking)입니다. 우버는 기존 통신 로직이 파이썬으로 짜여져 있다고 하는데, 이벤트 기반의 대용량 비동기 통신을 가능하게 하는 솔루션인 Tornado를 써서 처리량을 늘렸다고 합니다. 
2. 서비스 모니터링(Service discovery and resiliency)인데요. 장애가 발생했을 때 그 지점을 정확하게 알고 장애가 연쇄적으로 확산되지 않도록 응급 차단하는 일(circuit breaking 이라고 함)과 서비스 수준을 통제(SLA)하는 일을 의미합니다. 
3. 엄격한 인터페이스 정의입니다. 우버는 여러 언어의 클라이언트를 지원하는 Thrift라는 솔루션을 활용해서 원격 서비스에 대해 인터페이스를 명확하게 정의하고 쓰게 하여 주고 받는 데이터 불일치(혹은 버전 불일치)를 막았다고 합니다. 

*운영 안정화를 위한 세 가지 원칙*
1. 병목 지점 확인을 위해서 부하 테스트load tests 수행
2. 컨데이터container 사용으로 하드웨어 효율을 높임
3. 시스템 복구 및 취약점 식별을 위해 서비스 모의 장애 수행

You Cannot Have Exactly-Once Delivery...breaking new geek
=
Within the context of a distributed system, you cannot have exactly-once message delivery.
You cannot have exactly-once delivery semantics in any of situations.

distributed systems are all about trade-offs. 
There are essentially three types of delivery semantics: at-most-once, at-least-once, and exactly-once.

So where does the trade-off come into play, and why is exactly-once delivery impossible? The answer lies in the Byzantine Generals Problem. sending 10 letters doesn’t really provide any additional guarantees. 

State changes are idempotent and applying the same state change multiple times does not lead to inconsistencies as long as the application order is consistent with the delivery order. Consequently, guaranteeing at-least once semantics is sufficient and simplifies the implementation.

Every major message queue in existence which provides any guarantees will market itself as at-least-once delivery. If it claims exactly-once, it’s because they are lying to your face in hopes that you will buy it or they themselves do not understand distributed systems. 

When using confirms, producers recovering from a channel or connection failure should retransmit any messages for which an acknowledgement has not been received from the broker. There is a possibility of message duplication here, because the broker might have sent a confirmation that never reached the producer (due to network failures, etc). Therefore consumer applications will need to perform deduplication or handle incoming messages in an idempotent manner.

The way we achieve exactly-once delivery in practice is by faking it. Either the messages themselves should be idempotent, meaning they can be applied more than once without adverse effects, or we remove the need for idempotency through deduplication.

To reiterate, there is no such thing as exactly-once delivery. We must choose between the lesser of two evils, which is at-least-once delivery in most cases. 

 This can be used to simulate exactly-once semantics by ensuring idempotency or otherwise eliminating side effects from operations.
