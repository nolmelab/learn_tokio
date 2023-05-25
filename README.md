# 들어가며

tokio는 러스트의 비동기 실행기(Executor)와 각종 유틸리티(tokio\_utility 등)를 구현하여 서버 프로그래밍을 비동기로 구현할 수 있게 한 일련의 패키지에 대한 이름이자 패키지이기도 합니다.&#x20;

tokio는 다양한 백엔드 구현에 이미 많이 사용되었습니다. 하지만 여전히 러스트와 함께 성장 중에 있습니다. 러스트 커뮤니티는 디스코드를 많이 활용하고 있습니다. 토키오도 마찬가지로 [디스코드 서버](https://discord.gg/tokio)를 운영 중에 있습니다.

무엇을 어떻게 공부해야 할까요?

* 먼저, tokio 튜토리얼은 꼭 읽고 이해해야 하는 문서입니다. 비동기 처리에 대한 개요이며 비동기로 뭔가를 동시에 처리하는 감을 잡아야 하기 때문입니다.&#x20;
* 그 다음은 바로 examples를 따라가면 될 것 같습니다. examples에는 여러 가지 예시가 있는데 필요에 따라 선택해서 진행하면 될 것 같습니다.&#x20;
  * connect.rs&#x20;
  * echo.rs
  * chat.rs&#x20;
  * tinyhttp.rs
  * 저의 경우 위와 같은 순서로 진행하면서 토키오 + 러스트 코드 분석을 함께 하려고 합니다.&#x20;
