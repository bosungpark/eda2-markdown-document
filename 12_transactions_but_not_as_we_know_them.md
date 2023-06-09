중복 문제
=
이벤트 드리븐 환경에서 중복 문제는 중요하다. 이를 해결하기 위해서는 멱등성과 exactly once를 보장해줄 수 있는 환경이 중요하다.

1. 카프카의 트랜잭션을 사용하는 것
2. 멱등성을 보장하는 코드를 짜는 것

트랜잭션을 통한다면 각 서비스별로 중복과 관련한 문제를 캡슐화 할 수 있다. 이는 어플리케이션 단의 고민을 인프라 단계로 넘기는 것이라고 볼 수 있다. 단, 트랜잭션은 인풋과 아웃풋이 모두 카프카를 통할 때에만 해당한다. 또 서로 다른 서비스에서 이미 커밋이 일어난 경우 역시 어쩔수 없다. 사가 패턴을 사용해야 한다.

반대로 코드레벨의 멱등성 구현은 각각의 서비스의 구현의 복잡도를 높이고, 에러의 가능성이 존재하게 한다는 위험도 있다.

