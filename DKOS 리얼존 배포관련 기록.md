# DKOS 리얼존 배포관련 기록
## 1. VIP 세팅
```
annotations:
    service.beta.kubernetes.io/openstack-internal-load-balancer: "true"
```
- 쿠버네티스 v1.15 미만 버전의 클러스터에서는 어노테이션(annotations)에 service.beta.kubernetes.io/openstack-internal-load-balancer: "true" 를 넣어주어야 합니다. 
- service.beta.kubernetes.io/openstack-internal-load-balancer: "true"는 OpenStack LBaaS를 이용하기 위해 필요합니다.
- [참조](https://wiki.daumkakao.com/pages/viewpage.action?pageId=647499391)


## 2. 어플리케이션 자원 사용량 제한
### Requests와 Limits는 사용을 보장받을 수 있는 경계선
### Requests
- 적어도 이 만큼의 자원은 컨테이너에게 보장되어야 한다
- 오버커밋을 가능하게 만드는 기능
> 오버커밋이란?
한장된 컴퓨팅 자원을 효율적으로 사용하기 위한 방법으로, 사용할 수 있는 자원보다 더 많은 양을 가상 머신이나 컨테이너에게 할당함으로 전체 자원의 사용률을 높이는 방법

### Limits
- 해당 컨테이너에 유휴 자원이 있는 경우, 최대 limits까지 이용가능함

#### 최소한 Requests 만큼의 자원 사용은 보장되지만, 유휴 메모리 자원이 있다면 최대 Limits까지 사용할 수 있다
