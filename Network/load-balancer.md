# [Network](https://github.com/hyojaekim/TIL/tree/master/Network) / [🏠 Home](https://github.com/hyojaekim/TIL)

### 로드 밸런서(Load Balancer)

#### "왜 필요하나?"

수천, 수만 명의 클라이언트가 있다면 서버의 응답처리 속도는 늦어지게 된다. 문제를 해결하기 위해서 아래의 방법이 존재한다.

`Scale-up - 서버가 빠르게 동작하기 위해 하드웨어 성능을 높이는 방법`
`Scale-out - 여러 대의 서버가 나누어서 일을 처리하는 방법`

`Scale-out`은 하드웨어 성능을 높이는 것보다 비용이 저렴하고, 하나의 서버가 죽어도 여러 대의 서버가 있기 때문에 무중단 서비스가 가능하다.

**이때 여러 대의 서버에게 균등하게 트래픽을 분산시켜 주는 것이 로드 밸런서(Load Balancer)이다. 트래픽이 많은 경우, 서버의 로드율, 부하량, 속도저하 등을 고려해 분산 처리하도록 해결해 주는 서비스이다.**

<hr>

#### "그렇다면 하나의 로드 밸런서가 여러 서버로 분산시키는데 로드 밸런서에서 장애가 발생하면 어떻게 하냐?"

로드 밸런서를 이중화 시키면 될 것 같습니다.
메인 로드 밸런서와 여유분의 로드 밸런서를 두어서 로드 밸런서끼리 Health Check를 해서 메인 로드 밸런서가 동작하지 않으면 다른 로드 밸런서로 변경되어 운영하면 될 것 같습니다.



### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Network/load-balancer.md#Network---home)
