# Amazon ECS (Elastic Container Service)
AWS 환경에서 컨테이너 애플리케이션을 쉽게 실행, 확장 및 보호할 수 있는 컨테이너 오케스트레이션 서비스

## 아키텍처
![image](https://user-images.githubusercontent.com/20418155/175031743-8ccea43c-596f-4c34-9849-decb7bdb22ed.png)

![image](https://user-images.githubusercontent.com/20418155/175027159-768cb706-f57e-4fe0-8066-d20a84557fff.png)


## 구성 요소
|구성 요소|설명|Kubernates|
|------|---|---|
|ECS Task|컨테이너 최소 실행 단위|Pod|
|ECS Service|필요한 테스크 수를 유지, ELB와 연동되어 외부로 서비스 노출|Deployment or Service|
|ECS Cluster|테스크가 실행되는 논리적 그룹|Cluster or Namespace|
### ECS Task (작업)
- 작업 정의 내용을 기반으로 ECS 클러스터에 속하는 인스턴스(또는 Fargate) 배포
- 컨테이너 이미지 맵핑을 통해 컨테이너를 정의

### ECS Service (서비스)
- 서비스 유형(replica, daemon)과 작업 배치 전략(Binpacking, Spread, Random)을 선택 가능
- 로드 벨런서(ALB) -> 부하 분산
- 서비스 Auto Scaling 적용 가능

```
※ Auto Scaling

클러스터 생성 -> Auto Scaling Group 생성 -> 인스턴스 시작 -> 작업 수행 -> ECS에서 CloudWatch 지표 반영
-> 문제 발생 -> ASG 스케일링
```


### ECS Cluster (클러스터)
- 작업이 시작되는 논리적인 그룹
- 클러스터 생성 시, EC2 인스턴스 구축 및 생성 후, 클러스터에 추가 인스턴스 등록 가능 (여러개의 인스턴스)

## 추가 서비스
### ECR (Elastic Container Registry)
- 완전 관리형 컨테이너 레지스트리
- 배포 워크플로우를 간소화함 (EKS, ECS, Lambda, Fargate)

### Cloud9
- 서버 내에 작업할 수 있는 IDE 환경

### CloudWatch
- 애플리케이션 모니터링
- 리소스 사용률을 최적화하는 데 필요한 데이터와 실행 가능한 인사이트를 제공
- 이상 동작을 감지, 경보 설정, 로그와 지표 시각화

### ALB (Amazon Application Load Balancer)
- Load Balancer

## 실제
ECR에 도커 이미지를 올리고, ECS통해 이미지를 클러스터 내에 있는 EC2로 가져온다. 이 때, 로드 밸런서로는 ALB(EC2에서 로드 밸런서 생성)를 사용하고, CloudWatch를 통해 모니터링한다.
