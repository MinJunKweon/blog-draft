# MSA(Microservices Architecture)란?

MSA(마이크로서비스 아키텍처)란, 서비스 지향 아키텍처(Service-Oriented Architecture)의 변형 중 하나로서, 결합도를 낮춘 서비스들의 모음으로 애플리케이션을 구성한 구조를 말합니다. MSA의 서비스는 잘게 쪼개져있고, 프로토콜은 가볍습니다.

> Microservice architecture – a variant of the service-oriented architecture (SOA) structural style – arranges an application as a collection of loosely coupled services. In a microservices architecture, services are fine-grained and the protocols are lightweight.
>
> 출처 - [위키피디아](https://en.wikipedia.org/wiki/Microservices)

### MSA의 탄생배경

전통적인 서비스 지향 아키텍처는 모놀리식 아키텍처(Monolithic Architecture)가 주를 이뤘습니다. 모놀리식 아키텍처는 하나의 애플리케이션으로 모든 기능과 시스템 컴포넌트들을 관리했습니다. 그렇다보니 모놀리식 아키텍처는 몇 가지 한계점들이 존재했습니다:

1. **Side Effect** - 기능 간의 결합도가 높아서, 작은 변경에도 사이드 이펙트가 존재할 수 있으므로 테스트해야하는 범위가 넓습니다.
2. **정적인 스케일링** - 서버 증설(Scale-up)이 필요할 때, 애플리케이션 하나를 통째로 증설해야하기 때문에 특정 기능만 증설하는 등의 동적인 스케일링이 불가능합니다.
3. **장애에 민감한 애플리케이션** - 특정 기능에 장애가 발생했을 때, 다른 기능들까지 모두 중단됩니다. 또한, 무중단으로 동작해야하는 서비스를 배포할 때 부담이 큽니다.

등등

**MSA는 모놀리식 아키텍처의 한계점을 보완하고, 서비스가 좀 더 동적으로 동작하게 해줍니다.**

1. **테스트 범위 한정** - 각 서비스들은 프로토콜(HTTP, gRPC 등)을 통해 통신하기 때문에, 통신 스펙이 변경되지 않는 이상 사이드 이펙트(Side-Effect)가 존재하지 않습니다.
2. 