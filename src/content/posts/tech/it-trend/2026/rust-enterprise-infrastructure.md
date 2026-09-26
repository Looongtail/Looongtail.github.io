---
title: "Rust의 부상: 기업 IT 인프라와 데이터센터를 위한 새로운 언어 선택"
description: "Rust가 메모리 안전성과 시스템 성능을 함께 요구하는 클라우드·데이터센터·AI 인프라에서 어떤 역할을 맡을 수 있는지, 실제 적용 사례와 도입 조건을 중심으로 살펴본다."
pubDate: "2026-09-27"
category: "tech"
tags:
  - Rust
  - cloud infrastructure
  - memory safety
  - data platform
  - software security
slug: "tech/it-trend/2026/rust-enterprise-infrastructure"
---

클라우드와 AI 인프라가 커질수록 기업이 관리해야 하는 소프트웨어의 범위도 넓어진다. 네트워크 요청을 중계하는 프록시, 컨테이너와 가상화 환경을 제어하는 구성 요소, 대규모 데이터를 변환하는 실행 엔진, 수많은 서버에서 상태를 수집하는 에이전트가 서비스의 성능과 안정성을 좌우한다. 이 계층에서는 기능을 빠르게 추가하는 일만큼, 취약점을 줄이고 자원 사용량을 예측 가능하게 만드는 일이 중요하다.

Rust는 이 문제를 겨냥해 주목받는 시스템 프로그래밍 언어다. C와 C++에 가까운 제어 능력과 성능을 지향하면서도, 메모리 사용과 동시성에서 발생하기 쉬운 일부 오류를 컴파일 단계에서 발견하도록 설계됐다. 초기에는 시스템 프로그래밍의 대안으로 출발했지만, 현재는 Google, Microsoft, AWS, Cloudflare 등의 운영체제와 클라우드 인프라에서 실제로 활용되고 있다.

중요한 점은 Rust가 기존 언어를 일괄 대체하는 표준이 된다는 데 있지 않다. 기업이 성능, 보안, 운영 비용을 함께 고려해야 하는 실행 계층을 더 세밀하게 분리하고 있다는 흐름에 있다. 이 글은 Rust의 배경과 메모리 안전성의 원리, 글로벌 기업의 적용 사례를 바탕으로 데이터센터와 기업 IT 환경에서의 활용 가능성을 살펴본다.

## 시스템 프로그래밍 언어로의 성장 과정

Rust는 2006년 Graydon Hoare의 개인 프로젝트에서 출발했고, 이후 Mozilla의 지원을 받아 발전했다. 2015년 Rust 1.0이 공개되면서 안정적인 언어와 도구 체계를 갖추기 시작했다. 초기 목표는 C/C++가 제공하는 하드웨어 제어 능력과 실행 성능을 유지하면서도, 수동 메모리 관리에서 반복되는 오류를 줄이는 것이었다.

2021년에는 AWS, Google, Microsoft, Mozilla 등이 참여한 Rust Foundation이 설립됐다. 이 변화는 특정 기업의 연구 프로젝트가 아니라 독립적인 오픈소스 생태계로 운영 기반을 넓혔다는 점에서 의미가 있다. 기업 IT 조직이 Rust를 검토할 때도 언어의 인기보다 장기 유지보수, 도구와 라이브러리의 성숙도, 인력 생태계를 함께 봐야 한다.

## 기업 핵심 인프라에서의 중요성

기업 IT 환경에는 Java, Python, Go, C, C++처럼 역할이 분명한 언어가 이미 널리 사용된다. 업무 시스템과 데이터 분석, 자동화에는 풍부한 생태계와 인력을 갖춘 언어가 유리하고, 운영 도구와 네트워크 서비스에는 다른 특성이 요구된다. 따라서 Rust 도입의 질문은 “모든 시스템을 Rust로 바꿀 것인가”가 아니라 “어떤 컴포넌트에서 기존 방식의 위험과 비용이 큰가”에 가까워야 한다.

특히 외부 입력을 많이 다루거나, 높은 권한으로 실행되거나, 다수의 인스턴스가 상시 동작하는 구성 요소는 작은 결함도 크게 확대될 수 있다. 네트워크 프로토콜 처리, 인증과 암호화 주변 모듈, 데이터 파서, 시스템 모니터링 에이전트, 가상화 제어 계층이 대표적이다. 이 영역에서는 처리량만큼 잘못된 메모리 접근과 동시성 오류를 줄이는 일이 운영 품질과 보안의 일부가 된다.

Rust의 가치는 언어 선호보다 설계 선택지에 있다. 기존 애플리케이션을 다시 작성하는 대신, 신규 서비스 또는 병목이 확인된 구성 요소를 독립적인 모듈로 분리해 검증할 수 있기 때문이다. 이 접근은 기술 전환의 범위와 장애 영향을 제한하면서 실제 성능, 메모리 사용량, 배포·장애 복구 비용을 비교할 기회를 만든다.

## 컴파일 단계 검증을 만드는 언어 설계

Rust는 별도의 가비지 컬렉터 없이 메모리 안전성을 확보하려는 언어다. 핵심은 데이터마다 관리 책임을 두는 소유권, 다른 코드가 데이터를 사용하게 하는 참조와 빌림, 참조 대상의 유효 범위를 다루는 수명 개념이다. 컴파일러는 이 관계를 검사하고, 이미 사라진 데이터에 접근하거나 충돌하는 방식으로 읽기와 쓰기를 시도하는 코드가 있으면 실행 전에 거부한다.

![하나의 문자열 데이터를 두 개의 불변 참조가 함께 빌리는 관계를 시간 흐름으로 보여 주는 RustViz 시각화](/images/contents/it-trend/rust-memory-safety/rustviz-multiple-immutable-borrow.svg)

*그림 1. 하나의 데이터에 여러 불변 참조를 허용하는 빌림 관계의 예시. RustViz 제공, MIT License.*

이 구조는 C나 C++에서 자주 문제가 되는 use-after-free, 이중 해제, 일부 데이터 경쟁을 줄이는 데 목적이 있다. 실행 중에 오류를 추적하는 방식이 아니라, 코드 변경 시점에 제약을 드러내므로 시스템 소프트웨어의 검토 방식에도 영향을 준다. 다만 Rust가 모든 결함을 막는 것은 아니다. 비즈니스 로직 오류, 잘못된 권한 설계, 취약한 의존성은 별도의 검증이 필요하며, 하드웨어·외부 함수 연동처럼 `unsafe`가 필요한 코드도 존재한다.

Java와 Python도 자동 메모리 관리를 통해 상당수의 메모리 오류를 줄인다. 다만 실행 환경의 특성과 가비지 컬렉션이 지연 시간이나 자원 사용량에 영향을 줄 수 있는 워크로드가 있다. Rust의 선택지는 런타임에 새 관리 계층을 추가하기보다, 소유권 이동·참조 권한·유효 범위를 정적으로 검증하는 데 있다. 안전한 Rust 코드에서는 이 검증이 빌드 시점에 끝나므로, 메모리 안전성을 위해 별도의 추적용 가비지 컬렉터를 요구하지 않는다.

개발자가 체감하는 대가도 있다. 소유권과 수명은 기존 언어의 객체 참조 방식에 익숙한 개발자에게 초기 학습 부담이 될 수 있다. 2025년 Rust 설문에서도 컴파일 시간과 저장 공간을 포함한 자원 사용은 생산성을 제한하는 주요 문제로 지적됐다. 언어의 안전성만으로 도입 효과를 판단하기보다 빌드 시간, 디버깅 경험, 라이브러리 성숙도, 채용과 교육 비용을 함께 봐야 하는 이유다.

## 운영 인프라의 적용 사례

Rust의 기업 적용 사례는 대체로 전체 제품을 새 언어로 전환하는 모습과는 다르다. 보안 경계나 대량 트래픽 처리처럼 시스템 특성이 뚜렷한 계층에 먼저 사용된다. 아래 사례는 Rust가 적합한 문제의 범위를 보여주지만, 같은 효과가 모든 기업 환경에서 재현된다는 뜻은 아니다.

| 조직 또는 프로젝트 | 적용 영역 | 기업 IT 관점의 의미 |
| :--- | :--- | :--- |
| Google Android | 시스템 구성 요소와 보안 중심의 네이티브 코드 | 메모리 안전성을 신규 코드의 기본 조건으로 다루는 접근 |
| Microsoft Azure | 핵심 인프라 구성 요소 | C/C++이 필요한 고성능 영역에서의 대안 검토 |
| AWS Firecracker | 서버리스용 microVM 가상화 | 격리와 빠른 시작이 필요한 실행 환경의 설계 선택지 |
| Cloudflare Pingora | 비동기 HTTP 프록시와 네트워크 서비스 | 대량 연결 처리와 사용자 정의가 필요한 프록시 계층의 기반 기술 |

Google은 Android의 신규 시스템 코드에서 Rust를 C/C++의 직접적인 대안으로 사용해 왔다. 2025년 공개한 Android 내부 관측 결과에서는 Rust 코드의 메모리 안전성 취약점 밀도가 C/C++보다 크게 낮았고, 비슷한 규모의 변경에서 코드 리뷰 시간과 롤백 비율도 낮게 나타났다고 설명했다. 이는 Android 개발 환경에서 얻은 결과이므로 모든 프로젝트의 생산성 수치로 일반화할 수는 없지만 보안 강화가 반드시 개발 속도를 늦춘다는 전제를 다시 검토하게 하는 사례다.

![2019년부터 2025년까지 Android의 신규 메모리 비안전 코드와 메모리 안전성 취약점 비율 변화를 보여 주는 막대그래프](/images/contents/it-trend/rust-memory-safety/google-android-memory-safety-trend.png)

*그림 2. Android의 신규 메모리 비안전 코드와 메모리 안전성 취약점 비율 추이. 출처: Google Online Security Blog.*

Google은 2026년 Android Automotive OS 기반 Software-Defined Vehicle 플랫폼에서도 Rust를 주요 개발 언어로 활용한다고 밝혔다. 이는 Google 전체가 Rust로 전환한다는 선언이 아니라, 분산 시스템 인프라와 보안·안정성 요구가 높은 신규 영역에서 주력 선택지로 사용한다는 의미다.

Azure는 C/C++을 사용할 수밖에 없는 고성능 영역에서 Rust를 대안으로 제시하며, 핵심 인프라 일부에 적용했다고 밝혔다. 이 선택은 다중 테넌트 환경과 Confidential Compute로 강화하는 방어 계층의 일부다. 즉 Rust는 단독 해법이 아니라 격리, 암호화, 권한 관리와 결합하는 보안 설계의 한 층으로 이해해야 한다.

![저장 중 데이터와 전송 중 데이터의 암호화에 더해 실행 중 데이터를 Confidential Computing으로 보호하는 구조](/images/contents/it-trend/rust-memory-safety/azure-confidential-computing-three-states.png)

*그림 3. Azure Confidential Computing이 추가하는 ‘실행 중 데이터’ 보호 영역. 출처: Microsoft Learn, Azure Confidential Computing Overview.*

## 클라우드 실행 계층의 적용 범위

AWS와 Cloudflare의 사례는 Rust가 데이터센터와 클라우드 서비스에서 맡는 역할을 구체적으로 보여준다. AWS가 개발한 Firecracker는 Linux KVM 위에서 경량 가상머신인 microVM을 실행하는 오픈소스 기술이다. 서버리스 환경에서 빠른 시작과 워크로드 격리를 목표로 하며, AWS Lambda와 Fargate의 실행 환경에 사용된다. AWS는 이 밖에도 컨테이너 전용 운영체제 Bottlerocket과 인프라 소프트웨어에서 Rust를 활용해 왔다.

Cloudflare의 Pingora는 HTTP 트래픽과 연결 관리를 위한 비동기 멀티스레드 Rust 프레임워크다. Cloudflare는 기존 프록시 계층의 운영 한계를 개선하기 위해 이를 글로벌 네트워크에 적용하고 2024년 오픈소스로 공개했다. 이 두 사례의 공통점은 최종 사용자 기능보다 가상화와 네트워크 프록시처럼 서비스 실행의 기반이 되는 계층에 Rust를 적용했다는 점이다.

가상화와 프록시는 개별 애플리케이션의 성능뿐 아니라 전체 인프라의 자원 사용량과 장애 영향 범위에 영향을 준다. 따라서 특정 컴포넌트의 안정성과 효율성 개선은 다수 서비스에 누적될 수 있다. 기업이 Rust를 평가할 때도 언어 자체의 성능 비교보다, 해당 컴포넌트가 전체 서비스에 만드는 운영 비용과 보안 경계를 먼저 살피는 편이 적절하다.

## 데이터 플랫폼의 실행 계층 역할

데이터 처리 영역에서도 Rust는 전체 분석 환경을 대체하기보다 고성능 실행 엔진의 기반으로 활용된다. 대표적인 사례가 Polars다. Polars는 Rust로 작성된 DataFrame 처리 엔진이며 Python 인터페이스도 제공한다. 개발자는 익숙한 Python 환경에서 변환 로직을 작성하되, 실제 연산은 Rust 기반의 컬럼형·병렬 실행 엔진에 맡길 수 있다. 현재 필자가 수행하고 있는 차세대 SCM Staging 구축 프로젝트에서도 Polars를 주력 Dataframe으로 활용하면서 성능과 안정적인 메모리 사용 모두를 만족하고 있다.

Apache DataFusion은 Apache Arrow의 메모리 형식을 바탕으로 만든 확장 가능한 Rust 쿼리 엔진이다. SQL과 DataFrame API, 컬럼형·스트리밍·멀티스레드 실행 구조를 제공하며, 데이터베이스나 분석 플랫폼을 만드는 팀이 모든 실행 엔진을 처음부터 구현하지 않고 필요한 연산자와 데이터 소스를 조합·확장할 수 있게 한다.

이 사례가 보여주는 것은 Python과 Rust 중 하나만 선택해야 한다는 결론이 아니다. 데이터 파이프라인의 오케스트레이션, 분석 실험, 업무 규칙은 Python 생태계에 남겨 두고, 대용량 파싱·변환·집계처럼 비용이 큰 연산을 네이티브 실행 계층에 맡기는 역할 분담이 가능하다. 실제로 어떤 계층을 분리할지는 데이터 규모, 지연 시간, 운영 인력, 기존 라이브러리 의존성에 따라 달라진다.

AI 인프라에서도 같은 관점이 적용된다. GPU 연산 자체보다 요청을 전달하는 API, 데이터 전처리, 텔레메트리 수집, 노드 상태 관리, 네트워크 통신 같은 주변 구성 요소가 전체 서비스의 처리량과 장애 대응에 영향을 준다. Rust는 이런 주변 계층의 모든 문제를 해결하는 기술이 아니라, 메모리 사용과 동시성 제어가 중요한 부분을 개선하기 위한 하나의 후보가 될 수 있다.

## 데이터센터 운영 컴포넌트

데이터센터는 수많은 서버와 네트워크 장비, 스토리지, 가상화·컨테이너 환경이 결합된 대규모 시스템이다. 전체 인프라의 상태를 계속 수집하고, 장애를 빠르게 식별하며, 제한된 자원을 효율적으로 사용하는 일이 중요하다. 이 환경에서 Rust는 인프라 전체를 대체하는 기술이 아니라, 운영 기능을 담당하는 특정 컴포넌트의 구현 선택지가 될 수 있다.

첫 번째 후보는 시스템 모니터링과 데이터 수집 에이전트다. CPU, 메모리, 디스크, 네트워크 상태를 수집하는 에이전트는 많은 장비에서 상시 실행되므로, 프로세스별 메모리 사용량과 CPU 오버헤드가 누적된다. 두 번째는 API Gateway, reverse proxy, load balancer처럼 대량의 연결과 요청을 처리하는 네트워크 계층이다. 세 번째는 인증 토큰 처리, 데이터 파싱, 네트워크 프로토콜 분석처럼 외부 입력을 직접 다루는 보안·격리 기능이다.

AI 데이터센터에서도 GPU 자체의 연산 성능만큼 GPU 사용량 수집, 리소스 상태 관리, 요청 전달, 데이터 전처리와 네트워크 통신 같은 주변 계층이 중요하다. Rust는 GPU 연산을 대체하기보다 이 실행 계층의 안정성과 자원 효율을 개선하는 후보가 될 수 있다. 다만 어떤 영역에서도 언어만으로 성능이 보장되지는 않으며, 워크로드와 기존 시스템의 연계 구조를 기준으로 검증해야 한다.

## 삼성SDS와 SCP의 활용 가능성

삼성SDS처럼 기업용 IT 서비스를 제공하고 클라우드·데이터센터를 운영하는 기업에서는 Rust의 활용 범위를 더 구체적으로 검토할 수 있다. 서비스 구축과 운영을 함께 수행하는 환경에서는 개발 언어의 선택이 개별 프로젝트의 생산성뿐 아니라 장기 유지보수 비용과 운영 안정성에도 영향을 준다.

Samsung Cloud Platform(SCP)은 컴퓨팅, 스토리지, 네트워킹, 보안, 컨테이너, 데이터 분석, AI/ML과 DevOps 서비스를 제공하며, GPUaaS와 다중 노드 GPU 클러스터도 운영한다. 이 서비스 구조에는 고객 애플리케이션 외에도 리소스 상태를 수집하고 요청을 처리하며 실행 환경을 제어하는 기반 컴포넌트가 필요하다. 따라서 Rust의 가치는 SCP 전체를 새로운 언어로 전환하는 데 있지 않고, 운영 특성이 뚜렷한 일부 컴포넌트의 품질과 자원 효율을 검증하는 데 있다.

기업의 첫 Rust 프로젝트는 전면 재작성보다 경계가 분명한 컴포넌트여야 한다. 예를 들어 상시 실행되는 모니터링 에이전트, 입력 검증이 많은 프로토콜 파서, 대량 연결을 처리하는 프록시 모듈, 데이터 변환 라이브러리처럼 기능과 성능 지표를 독립적으로 측정할 수 있는 영역이 적합하다. 기존 서비스와의 인터페이스를 API 또는 메시지 경계로 두면, 도입 실패가 전체 시스템 장애로 번지는 위험도 줄일 수 있다.

평가는 언어의 인기도가 아니라 운영 지표로 진행해야 한다. CPU와 메모리 사용량, 처리 지연, 오류율, 배포 실패율, 장애 복구 시간, 취약점 대응 시간처럼 기존 구현과 비교 가능한 기준을 먼저 정할 필요가 있다. 보안 측면에서는 `unsafe` 코드의 범위, 외부 라이브러리와 네이티브 연동 지점, 빌드와 의존성 관리 체계를 함께 검토해야 한다.

조직 차원의 준비도도 중요하다. 코드 리뷰어가 소유권 오류와 비동기 실행 모델을 설명할 수 있는지, 장애 상황에서 로그와 프로파일링 도구로 원인을 찾을 수 있는지, 유지보수를 한 팀에만 의존하지 않는지 확인해야 한다. 작은 파일럿에서 도입 효과와 교육 비용을 함께 측정한 뒤 적용 범위를 넓히는 편이 현실적이다.

SCP 관점의 활용 후보는 데이터센터의 서버·네트워크 모니터링 에이전트, 클라우드 플랫폼의 API Gateway와 프록시, Kubernetes 운영용 노드 유틸리티, 데이터 파싱·변환·집계 엔진, AI/GPU 인프라의 텔레메트리와 자원 관리 보조 서비스다. 이는 삼성SDS가 Rust를 이미 사용한다는 뜻이 아니라, 글로벌 사례에서 도출되는 기술적 활용 가능성이다.

| 사업 및 기술 영역 | 활용 검토 방안 | 기대 효과 |
| :--- | :--- | :--- |
| 데이터센터 운영 | 서버·네트워크 모니터링 에이전트 | 경량 실행과 자원 사용 효율화 |
| 클라우드 플랫폼 | API Gateway, 프록시, 네트워크 처리 | 안정적인 대량 요청 처리 |
| Kubernetes 운영 | 노드 에이전트와 시스템 유틸리티 | 실행 오버헤드 관리 |
| 데이터 플랫폼 | 데이터 파싱·변환·집계 엔진 | 대용량 데이터 처리 효율화 |
| AI/GPU 인프라 | 텔레메트리 수집과 자원 관리 보조 서비스 | 인프라 상태 관측과 운영 자동화 |
| 보안 서비스 | 입력 데이터 파서와 보안 처리 모듈 | 메모리 관련 취약점 예방 |

기존 Java·Python·Go 기반 플랫폼을 유지하면서도 성능이나 자원 효율이 중요한 일부 기능을 Rust 컴포넌트로 분리하는 방식이 현실적이다. 예를 들어 Kubernetes 환경에서 상시 실행되는 경량 에이전트, 대량 로그와 메트릭 수집 파이프라인의 데이터 파싱·압축 모듈, AI 인프라의 GPU 자원 모니터링과 노드 상태 수집 서비스가 후보가 될 수 있다. 도입 자체가 GPU 활용률이나 데이터센터 운영 효율을 보장하지는 않으므로, 기존 구현과 CPU·메모리 사용량, 처리 지연, 장애 복구 시간, 유지보수 비용을 비교해야 한다.

## 도입 판단의 한계와 조건

Rust는 메모리 안전성 문제의 상당 부분을 줄일 수 있지만, 시스템의 보안을 자동으로 보장하지는 않는다. 인증·권한 정책이 잘못됐거나, 의존성 공급망이 취약하거나, 운영 절차가 불완전하다면 언어 선택만으로 위험을 해결할 수 없다. 안전한 코드와 별개로 관측성, 테스트, 코드 리뷰, 취약점 대응, 변경 관리가 계속 필요하다.

생태계의 적합성도 업무마다 다르다. 이미 검증된 Java, Go, Python 라이브러리가 문제를 충분히 해결하고 있다면 새로운 언어를 추가하는 비용이 더 클 수 있다. 반대로 성능 병목과 메모리 안전성 위험이 반복해서 확인되고, 모듈 경계를 분명히 나눌 수 있다면 Rust의 장점을 검증할 여지가 커진다. 따라서 도입 판단은 기술적 매력보다 워크로드와 조직 역량의 조합으로 내려야 한다.

벤더와 오픈소스 생태계의 성숙도도 함께 살펴야 한다. 특정 라이브러리가 장기 유지보수되는지, 보안 공지가 신속한지, 팀이 필요한 플랫폼과 운영체제를 지원하는지 확인해야 한다. 인프라 소프트웨어는 배포 이후의 운영 기간이 길기 때문에 초기 개발 속도만으로 선택하면 장기 비용을 놓치기 쉽다.

## 기업 IT의 기술 선택 기준

Rust의 확산은 하나의 언어가 모든 개발 영역을 차지한다는 변화보다, 시스템을 더 세분화해 각 계층에 맞는 기술을 선택하는 흐름으로 이해하는 편이 적절하다. 업무 시스템에는 생산성과 생태계가 중요하고, 데이터 분석에는 탐색과 확장성이 중요하며, 인프라 실행 계층에는 성능·자원 효율·안전성이 더 크게 작용한다.

기업 IT 조직이 우선 답해야 할 질문은 “Rust를 도입할 것인가”가 아니다. 성능과 보안 문제가 실제로 어디에서 발생하는지, 그 영역을 독립적으로 측정하고 운영할 수 있는지, 기존 언어와 어떤 경계로 결합할 것인지가 먼저다. 이 질문에 답할 수 있다면 Rust는 새로운 범용 표준이 아니라 클라우드·데이터·AI 인프라의 운영 품질을 높이기 위한 실용적인 선택지가 될 수 있다.

## 출처

- [Mozilla, Mozilla Welcomes the Rust Foundation](https://blog.mozilla.org/en/mozilla/mozilla-welcomes-the-rust-foundation/)
- [Rust Foundation, Hello World!](https://rustfoundation.org/media/hello-world/)
- [Rust Project, The Rust Programming Language — Understanding Ownership](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html)
- [Rust Project, The Rust Programming Language — References and Borrowing](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)
- [Rust Project, The Rust Programming Language — Validating References with Lifetimes](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html)
- [RustViz, Interactively Visualizing Ownership and Borrowing for Rust (MIT License)](https://github.com/rustviz/rustviz)
- [Google Online Security Blog, Rust in Android: move fast and fix things](https://blog.google/security/rust-in-android-move-fast-fix-things/)
- [Android Developers Blog, AAOS SDV — Secure by Design](https://android-developers.googleblog.com/2026/08/aaos-sdv-secure-by-design.html)
- [Microsoft Azure Blog, Microsoft Azure security evolution: Embrace secure multitenancy, Confidential Compute, and Rust](https://azure.microsoft.com/en-us/blog/microsoft-azure-security-evolution-embrace-secure-multitenancy-confidential-compute-and-rust/)
- [Microsoft Learn, Azure Confidential Computing Overview](https://learn.microsoft.com/en-us/azure/confidential-computing/overview)
- [AWS Open Source Blog, Announcing the Firecracker Open Source Technology](https://aws.amazon.com/blogs/opensource/firecracker-open-source-secure-fast-microvm-serverless/)
- [AWS Open Source Blog, Why AWS Loves Rust, and How We'd Like to Help](https://aws.amazon.com/blogs/opensource/why-aws-loves-rust-and-how-wed-like-to-help/)
- [Cloudflare Blog, Open sourcing Pingora: our Rust framework for building programmable network services](https://blog.cloudflare.com/pingora-open-source/)
- [Polars, User Guide](https://docs.pola.rs/)
- [Apache DataFusion, Introduction](https://datafusion.apache.org/user-guide/introduction.html)
- [Rust Blog, 2025 State of Rust Survey Results](https://blog.rust-lang.org/2026/03/02/2025-State-Of-Rust-Survey-results/)
- [Samsung Cloud Platform, SCP Introduction](https://cloud.samsungsds.com/serviceportal/intro/SCP.html)
- [Samsung Cloud Platform, GPU as a Service](https://cloud.samsungsds.com/serviceportal/services/GPUaaS.html)
