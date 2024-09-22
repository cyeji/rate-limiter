# 처리율 제한 장치의 설계

### 토큰 버킷(token bucket)알고리즘
아마존과 스트라이프가 API 요청을 통제(throttle)하기 위해 이 알고리즘을 사용함
```
토큰 버킷은 지정된 용량을 갖는 컨테이너이다. 이 버킷에는 사전 설정된 양의 토큰이 주기적으로 채워짐.
토큰이 꽉 찬 버킷에는 더 이상의 토큰은 추가되지 않음.
버킷이 가득 차면 추가로 공급된 토큰은 버려짐(overflow)
```

- 토큰 버킷 알고리즘이 받은 인자
1. 버킷 크기 : 버킷에 담을 수 있는 토큰의 최대 개수
2. 토큰 공급률(refill rate) : 초당 몇 개의 토큰이 버킷에 공급되는가

- 버킷은 몇개를 사용해야되나?
```
통상적으로, API 엔드포인트마다 별도의 버킷을 둔다.
```
- 장점
1. 구현이 쉽다
2. 메모리 사용 측면에서도 효율적이다
3. 짧은 시간에 집중되는 트래픽(burst of traffic) 처리 가능하다. 버킷에 남은 토큰이 있기만 하면 요청은 시스템에 전달 될 것이다.
- 단점
1. 이 알고리즘은 버킷 크기와 토큰 공급률이라는 두 개 인자를 가지고 있는데, 이 값을 적절하게 튜닝하는 것이 까다로운 일이 될 것이다.

