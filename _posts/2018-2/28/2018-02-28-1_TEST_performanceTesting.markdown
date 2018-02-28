---

layout: post
title: "(WEB) Performance Testing Guide for web App"
category: WEB

---

## Performance Testing Guide for web App
### Chapter 1 을 읽고 성능 테스트의 정의를 정리하시오.
* [링크](https://msdn.microsoft.com/ko-kr/library/bb924356.aspx)
#### Core Activities of Performance Testing
1. Identify the Test Environment
  * 실제 물리적(H/W, S/W, 네트워크 등..) 환경, 가용자원, 도구 등을 식별합니다.
2. Identify Performance Acceptance Criteria
  * 응답시간(유저), throughput(business), 자원 최적화 등 목표와 제한을 만듭니다.
  * 이 이외에 여러가지 성공 기준들을 성립하는 기간입니다.
3. Plan and Design Tests
  * 시나리오를 만들고 여러 변동성을 고려하여 테스트 케이스를 만듭니다.
  * 그리고 이러한 테스트를 하나 이상의 시스템으로 통합하여 분석하고 준비합니다.
4. Configure the Test Environment
  * 테스트 환경, 도구, 자원 등 필요한 것들과 전략, 가능한 테스트 들을 고려합니다.
5. Implement the Test Design
  * Test Design에 따라 성능 테스트를 개발합니다.
6. Execute the Test
  * 테스트를 실행하고 모니터링 합니다. 분석을 위한 테스트 결과들을 수집합니다. 
7. Analyze Results, Report and Retest
  * 결과 데이터를 통합하고 교차 기능팀(cross-functional team)끼리 혹은 개별적으로 분석합니다.
  * 설정된 임계값 이내에 모든 값이 들었을 경우, 원하는 모든 정보를 수집했을 경우 테스트는 마무리 됩니다.
  * 하지만 불완전한 경우 나머지 테스트의 우선순위를 정하고 다시 테스트합니다.

#### Why Do Performance Testing
1. 릴리즈 준비상태 평가
  * 프로덕션 환경에서 프로그램의 성능 특징을 예상할 수 있고 이러한 것들을 어떻게 해결할지 판단할 수 있습니다. 릴리즈 전 성능 향상, 하드웨어 업그레이드 등을 이해관계자가 판단할 수 있게 하는 중요 지표가 됩니다.
  * 사용자가 불만족 할만한 부분을 미리 판단, 회사의 신뢰도에도 직접적 영향이 가는 부분 예측
2. 인프라 적합성 평가
  * 현재 인프라의 적합성을 판단하고 이 인프라 내에서 원하는 성능을 나타내고 있는지를 판단. 향후 자원 투입 등에도 예측, 영향을 줄 수 있다.
3. 개발된 SW 퍼포먼스 적합성 평가
  * 현재와 이후 변경될 기능, 제품의 비교를 제공
4. 퍼포먼스 튜닝의 효율성 증대를 위한 평가
  * 제품의 병목현상, 로드 등을 미리 판단

#### Project Context
Project Context에 대한 이해가 밑받침 되면서 성능 테스트가 일어나야 한다. 
Project Context에는
1. 프로젝트의 전체적인 통찰, 의도
2. 성능 테스팅의 목적
3. 성능 성공 기준
4. 개발 life cycle
5. 프로젝트 스케줄
6. 예산
7. 환경
8. 테스터, 팀의 역량
9. 성능 고려의 우선순위
10. 성능이 안좋을 때 비즈니스에 미치는 영향
이외에 프로젝트 비전, 시스템의 목적, 유저, 고객들의 기대 등을 생각해 볼 수 있다.

#### The Relationship Between Performance Testing and Tuning
##### Cooperative Effort
대부분 튜닝을 목적으로 성능 테스팅을 하게 되는데 이러한 테스트를 할 때 교차 기능팀(cross-functional team)이 모두 포함되어야 시스템 전반적으로 기대한 효과를 얻을 수 있습니다.

##### Tuning Process Overview
성능 테스팅과 다르게 반복적인 방식이 투입됩니다.
성능 테스트에는 일반적으로 빠른 변경과 테스트가 필요합니다. 
테스트 도중 문제가 발생되면 독립적인 성능테스트 팀과 튜닝팀이 투입되어 수정에 나섭니다. 이후 개선점을 반영하여 변경을 확인합니다.

##### performance, Load, and Stress Testing
* Performance testing: 시스템의 속도, 확장성, 안정성 등을 테스트합니다. 
  * 응답시간, throughput, 자원 최적화 등에 초점이 맞춰서 테스팅이 이뤄집니다.
* Load testing: 작업 중 발생하는 로드때문에 성능에 영향을 주는 것을 검증하는 과정이 주로 이뤄집니다.
* Stress testing: 작업 중 예상되는 조건을 초과할 경우 프로그램의 특성, 유효성을 검증하는데 초점이 맞춰집니다. 제한된 메모리, 디스크 공간 부족, 서버 장애 등 stress상황이 주어졌을 때 성능 특성을 측정하는데 있습니다.

##### Baselines
baseline을 만드는 것은 성능 향상 후 얼마나 발전되는지 평가할 목적으로 테스트를 실행하는 프로세스 중 하나입니다.
baseline은
* 이후 비교기준이 되며
* 측정항목이며 재사용이 가능해야 합니다.
* 지나친 일반화는 금물이며(다른 버전에서 그 기준선이 유효하지 않을 수도 있음)
* 진화되게 됩니다.(재정의)


##### Benchmarking
다른 조직에서 승인한 업계 표준과 시스템 성능을 비교하는 프로세스 입니다.
벤치마킹은
* 규칙을 따라야하지만
* 규칙을 따라 투명한 결과를 낼 수 있습니다.

##### Terminology(용어)
* 프린트 참조


### Chapter 2 를 읽고 성능 테스트의 종류를 정리하고, 해당 테스트가 어떤 상황에서 필요한지 직접 생각하여 정리하시오. (Word 2 page 분량)

### Chapter 3 을 읽고 성능테스트시에 어떤 위험사항이 있는지 정리하시오. (Word 1 page 분량)

### Part 2 를 읽고 성능테스트시 어떤 작업들이 필요한지 정리하시오. (Word 2 page 분량)

### Part 3 를 읽고 테스트 환경에 대해 정리하시오. (Word 1 page 분량)

### Part 4 를 읽고 성능테스트의 목적에 대해 정리하시오. (Word 2 page 분량)

### Part 5 를 읽고 테스트의 계획과 디자인에 대해 정리하시오.(Word 2 page 이상)

### Part 6 을 읽고 테스트 실행에 대해 정리하시오.(Word 2 page 이상)

### Part 7 을 읽고 테스트 결과 분석에 대해 정리하시오.(Word 2 page 이상)

### Part 8 을 읽고 Load 테스트와 Stress 테스트의 차이를 정리하시오. (Word 1 page)


<br/><br/>
