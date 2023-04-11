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