# spring-redis-test
### 레디스 센티널 아키텍처
- 아키텍처 구성 : 레디스 센티넬, 레디스 마스터, 레디스 레플리카로 구성
- 역할
  - 센티넬: 레디스 서버들의 상태를 주기적으로 모니터링, 마스터 서버가 서비스할 수 없는 상태가 되면 다른 레플리카를 마스터 서버로 변경(승격)
  - 마스터: 레플리카 서버들에 데이터를 복제하여 동기화한다.
  - 레플리카: 마스터 데이터의 복제본, 두 대 이상 설정하는 것으로 고려

클라이언트는 레디스 센티널 서버들에 마스터 서버를 질의하고 마스터 서버에 명령어를 실행한다. 마스터 서버가 죽어 새로운 마스터 서버가 선정되면 센티널은 클라이언트에 새로운 마수트 서버의 정보를 리포트한다. 그러므로 스프링 애플리케이션에서 레디스 커넥션을 설정할 때는 센티넬 서버들의 주소를 설정해야 한다.

3대의의 센티널 서버 운영 중 다수의 센티널 서버(2대)가 마스터 서버가 장애라고 판단하면 마스터 서버를 서비스에서 제외하고 장애 복구 절차를 실행한다. (쿼럼)


### 레디스 클러스터 아키텍처
- 로드밸런서에 의해 여러대의 서버가 관리되고 있는 분산 환경에서 세션을 어떻게 관리할것인가?
