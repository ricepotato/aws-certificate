# AWS Certificate

### Aurora 복제본이 포함된 Amazon Aurora

- 관계형 데이터베이스
- 마이크로초 대기시간을 일관되게 유지할 수 없음.
- ElasticCache 를 사용하는 경우에도 마이크로초 대시간을 일관되게 유지할 수 없음.
  - Amazon ElastiCache for Memcached란 무엇인가요? : https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/WhatIs.html
- Neptune 은 고도로 연결된 데이터 작업에 최적화된 그래프 데이터베이스임.
  - https://docs.aws.amazon.com/neptune/latest/userguide/intro.html
- Amazon Aurora : https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html

### DyanamoDB Accelerator (DAX) 가 포함된 Amazon DynamoDB

- 키 값 레코드를 지원하는 NoSQL database
- DAX 는 마이크로초 단위로 응답시간을 제공함
- Amazon DynamoDB : https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html
- DynamoDB Accelerator 를 통한 인 메모리 가속화 : https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAX.html

### DR

https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-options-in-the-cloud.html

#### 웜 스탠바이

```
Amazon EC2 인스턴스를 사용하여 AWS 애플리케이션 호스팅 환경을 다시 생성하고 애플리케이션 전체 트래픽의 10% 를 AWS EC2 로 전달 온프레미스 애플리케이션에 장애갑 발생하면 애플리케이션 트레픽 전체를 AWS EC2 로 전달
```

- RTO ~5분
- 인스턴스가 낮은 용량으로 실행되며 몇 분안에 확장할 수 있습니다.
- 어느정도 비용이 발생합니다.
- 기존 애플리케이션 호스팅 환경을 다시 생성하고 일부를 처리
- 장애 복구 계획: https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/plan-for-disaster-recovery-dr.html

#### 파일럿 라이트

```
Amazon EC2 인스턴스를 사용하여 AWS 애플리케이션 호스팅 환경을 다시 생성하고 EC2 인스턴를 중지
온프레미스 애플리케이션에 장애갑 발생하면 중지된 EC2 인스턴스 시작, 애플리케이션 트레픽 전체를 AWS EC2 로 전달
```

- 재해발생 시 복구 간소화 리소스, 비용 최소화
- AWS 리전에 기존 애프리케이션 호스팅 환경을 다시 생성
- 대부분의 리소스를 비활성 상태로 둠
- 테스트 중이나 DR 장애 조치가 필요한 경우에만 리소스 사용
- RPO, RTO 10분

#### 백업 및 복구

```
온프레미스 애플리케이션, 구성 및 데이터를 Amazon S3 버킷에 백업.
온프레미스 애플리케이션에 장애가 발생하면 온프레미스 호스팅 환경을 다시 구축하고 S3 버킷에 저장된 정보에서 애플리케이션을 복원
```

- 백업한 데이터를 다운로드 하여 복원
- 복구에 몇시간 또는 몇일이 소요됨

#### 다중 사이트 액티브 액티브

- RTO 요구사항을 즉시 해결함
- 서비스가 해당 시간 내에 이미 최대 용량으로 실행 중
- 비용이 많이 듬

#### 백업 및 복원

- ROT 5분 초과

### Amazon EC2 구성 세부 정보 조회

- 링크 로컬 주소 사용
- `curl http://169.254.169.254/latest/meta-data`

### Site-to-Site VPN 연결 구축

https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html

#### 가상 private gateway

- VPC 에 연결되어 AWS 에서 Site-to-Site VPN 연결을 생성
- 개방형 퍼블릭 인터넷을 통과할 필요 없이 온프레미스 데이터 센터에서 VPC 암호호된 브라이빗 네트워크 트레픽을 수락할 수 있음

#### 인터넷 gateway

- VPC 에 연결되어 인터넷에서 VPC 안팎으로 트레픽이 흐르도록 함
- 암호화된 VPN 연결이 아닌 개방형 인터넷 트레픽을 허용함
- VPN 연결은 인터넷 gateway를 통해 흐르지 않음

#### NAT gateway

- private Amazon EC2 인스턴스에서 인터넷에 요청을 보낼 수 있음
  - https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html

#### 고객 gateway

- 고객 gateway 디바이스는 고객의 데이터 센터에서 설정 및 구성됨

#### AWS API Gateway

- 개발자가 API 를 생성, 게시, 유지 관리, 모니터링 및 보호할 수 있게 해주는 완전 관리형 서비스
- 벡엔드 서비스의 데이터, 비즈니스 로직 또는 기능에 액세스하는 데 사용되는 정문 역할을 담당함

### 역할을 사용하여 권한 위임

https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#delegate-using-roles

### private subnet

- 인터넷 트레픽이 subnet에 라우팅되지 않음
- 데이터베이스를 private subnet 에 배치하여 보안 계층 추가

### routing

https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html#VPC_Scenario2_Routing

### Application Load Balancer

- 스티키 세션: https://docs.aws.amazon.com/elasticloadbalancing/latest/application/sticky-sessions.html
- 등록 취소 지연 : https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html#deregistration-delay
- EC2 Auto Scaling 의 조정 휴지 : https://docs.aws.amazon.com/autoscaling/ec2/userguide/Cooldown.html

### RDS

- 범용 SSD 스토리지 기본 I/O 성능은 GiB 당 3IOP
- 334GiB 스토리지의 경우 기본성능이 1,002IOPS
- 범용 SSD 스토리지는 프로비저닝 IOPS 스토리지보다 효율적임
