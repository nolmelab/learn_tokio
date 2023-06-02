# tokio tutorial 

tokio 튜토리얼은 예전에 한번 읽었습니다. 다시 읽으면서 구성 요소들을 깊게 이해하는 
과정을 다시 밟으려고 합니다. 여러 지점에서 방황으로 느껴질 수 있습니다. 예를 들어, 
tokio-tracing이 나오면 그 부분을 집중적으로 살펴보고 이해할 예정입니다. 

# tutorial 

Tokio는 Rust 프로그래밍 언어를 위한 비동기 런타임입니다. 네트워킹 애플리케이션 작성에 
필요한 구성 요소를 제공합니다. 이는 대규모 서버에서 수십 개의 코어로 작은 임베디드 
장치까지 다양한 시스템을 대상으로 하는 유연성을 제공합니다.

높은 수준에서 Tokio는 몇 가지 주요 구성 요소를 제공합니다:

- 비동기 코드를 실행하기 위한 멀티스레드 런타임.
- 표준 라이브러리의 비동기 버전.
- 다양한 라이브러리로 이루어진 큰 생태계.


# 프로젝트에서의 Tokio의 역할

애플리케이션을 비동기적으로 작성하면 여러 작업을 동시에 수행함으로써 비용을 줄여 확장성을
크게 향상시킬 수 있습니다. 그러나 비동기적인 Rust 코드는 자체적으로 실행되지 않으므로 
실행할 런타임을 선택해야 합니다. Tokio 라이브러리는 다른 모든 런타임의 사용량을 합친 
것보다 더 많이 사용되며, 가장 널리 사용되는 런타임입니다.

게다가, Tokio는 많은 유용한 유틸리티를 제공합니다. 비동기 코드를 작성할 때 Rust 표준 
라이브러리가 제공하는 일반적인 블로킹 API를 사용할 수 없으므로 대신 그들의 비동기 버전을 
사용해야 합니다. 이러한 대체 버전은 Tokio에 의해 제공되며, Rust 표준 라이브러리의 API와 
유사하게 구성되어 있습니다.

# Tokio의 장점

이 섹션에서는 Tokio의 몇 가지 장점을 소개하겠습니다.

## 빠르고 효율적입니다.

Tokio는 Rust 프로그래밍 언어 위에 구축되어 있으며, Rust 자체가 빠르기 때문에 Tokio도 
빠릅니다. 이는 Rust의 철학에 따라서 직접 코드를 작성하여 성능을 개선할 수 없도록 하는 것을 
목표로 합니다.

Tokio는 확장 가능하며, async/await 언어 기능 위에 구축되어 있어 확장 가능성이 높습니다. 
네트워킹과 관련하여 연결을 처리하는 속도에는 지연이 있으므로, 확장하기 위해서는 동시에 
많은 연결을 처리하는 것이 유일한 방법입니다. async/await 언어 기능을 사용하면 동시 작업 
수를 증가시키는 것이 매우 저렴해져 많은 동시 작업에 대해 확장할 수 있습니다.

## 신뢰성이 높습니다.

Tokio는 신뢰성과 효율성을 갖추기 위해 Rust로 구축되었습니다. 많은 연구에서 약 70% 정도의 
심각한 보안 버그가 메모리 안전성 부족으로 인한 것임을 밝혔습니다. Rust를 사용하면 이러한 
버그 유형을 완전히 제거할 수 있습니다.

또한 Tokio는 일관된 동작을 제공하는 데 중점을 둡니다. Tokio의 주요 목표는 예측 가능한 
소프트웨어를 배포하고, 신뢰할 수 있는 응답 시간과 예측할 수 없는 지연 증가 없이 매일 
동일하게 작동하는 것입니다.

## 쉽습니다.

Rust의 async/await 기능을 사용하면 비동기 애플리케이션 작성의 복잡성이 크게 줄어듭니다. 
Tokio의 유틸리티와 활발한 생태계와 함께 애플리케이션 작성은 매우 쉬워집니다.

Tokio는 가능한 경우 표준 라이브러리의 네이밍 규칙을 따릅니다. 이로써 표준 라이브러리만 
사용하여 작성된 코드를 쉽게 Tokio로 작성된 코드로 전환할 수 있습니다. Rust의 강력한 타입 
시스템과 함께, 올바른 코드를 쉽게 작성할 수 있는 능력은 비길 데 없습니다.

## 유연함

Tokio는 다양한 런타임 변형을 제공합니다. 멀티스레드, 작업 스틸링 런타임부터 가벼운 단일 
스레드 런타임까지 모든 것을 포함합니다. 이러한 각각의 런타임은 사용자가 필요에 맞게 조절할 
수 있는 많은 옵션을 제공합니다.


# Tokio를 사용하지 않는 경우

Tokio는 많은 작업을 동시에 처리해야 하는 프로젝트에 유용하지만, 일부 사용 사례에서는 
Tokio가 적합하지 않을 수 있습니다.

- 여러 스레드에서 병렬로 CPU-bound 계산을 실행하여 계산 속도를 높이는 경우. Tokio는 개별 
작업이 대부분의 시간을 IO 대기로 보내는 IO-bound 애플리케이션을 대상으로 설계되었습니다. 
애플리케이션이 병렬로 계산만 실행하는 경우에는 rayon을 사용해야 합니다. 그러나 필요에 따라 
"혼용하여 사용"하는 것도 가능합니다.

- 많은 파일을 읽는 경우. 파일을 많이 읽어야 하는 프로젝트에서도 Tokio가 일반적인 스레드 
풀과 비교했을 때 이점을 제공하지 않습니다. 이는 운영 체제가 일반적으로 비동기 파일 API를 
제공하지 않기 때문입니다.

- 단일 웹 요청을 보내는 경우. Tokio가 유리한 상황은 여러 가지 작업을 동시에 수행해야 할 
때입니다. 비동기 Rust를 위한 라이브러리인 reqwest와 같은 라이브러리를 사용해야 하지만 
동시에 많은 작업을 수행할 필요가 없는 경우, 해당 라이브러리의 블로킹 버전을 선호해야 
합니다. 이렇게 하면 프로젝트가 더 간단해집니다. 물론 Tokio를 사용해도 동작하지만, 블로킹 
API에 비해 실질적인 이점을 제공하지 않습니다. 라이브러리가 블로킹 API를 제공하지 않는 
경우에는 동기 코드와의 연결 방법에 대한 장점에 대한 장점을 참조하십시오.


# 도움 받기

어떤 단계에서든지 도움이 필요한 경우, 언제든 Discord나 GitHub 토론에서 도움을 받을 수 
있습니다. "초보자" 질문을 하시는 것에 대해 걱정하지 마십시오. 모두 처음부터 시작하며 
도움을 주는 것을 기쁘게 생각합니다.
