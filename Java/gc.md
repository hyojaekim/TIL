# [Java](https://github.com/hyojaekim/TIL/tree/master/Java) / [🏠 Home](https://github.com/hyojaekim/TIL)

### Garbage Collection

#### stop-the-world

GC를 실행하기 위해서 실행중인 애플리케이션을 중단하는 것을 말한다. **GC를 실행하는 스레드를 제외한 나머지 스레드 모두 작업을 멈춘다.** 어떠한 GC 알고리즘을 사용하더라도 stop-the-world는 발생하며, GC 튜닝을 한다는 것은 stop-the-world 시간을 줄이는 것을 의미한다.

#### 2가지 영역

Hostspot VM에서는 Young 영역과 Old 영역으로 나뉜다.

**Young 영역은 새로운 객체들이 여기에 위치해서, 많은 객체들이 금방 접근 불가능한 상태가 된다.** 해당 영역에서 객체가 사라질때 **Minor GC가 발생한다고 한다.**

**Old 영역은 Young 영역에서 살아남은 객체들이 이곳으로 복사된다.** 해당 영역에서 객체가 사라질 때 **Major GC 또는 Full GC가 발생한다고 한다.**

#### Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우

Old 영역에는 512바이트 덩어리(chunk)로 되어 있는 **카드 테이블(card table)이 존재한다.** Old 영역에 있는 객체가 Young 영역의 객체를 참조할 때, 정보가 표시된다. 따라서 Young 영역의 GC를 실행할 때, **Old 영역의 모든 객체를 확인하지 않고, 카드 테이블을 확인한다.**

#### Young 영역

새로운 객체들이 저장되는 Young 영역은 **Eden 영역 1개와 Survivor 영역 2개로 총 3개의 영역으로 나뉜다.**

##### 처리 절차

Young 영역의 처리 절차는 아래와 같다.

1. 새로 생성한 대부분의 객체는 Eden 영역에 위치한다.
2. Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동된다.
3. Eden 영역에서 GC가 발생하면 이미 살아남은 객체가 존재하는 Survivor 영역으로 객체가 계속 쌓인다.
4. 하나의 Survivor 영역이 가득 차게 되면 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동한다. 그리고 가득 찬 Survivor 영역은 아무 데이터도 없는 상태로 된다.
5. 이 과정을 반복하다가 계속해서 살아남아 있는 객체는 Old 영역으로 이동하게 된다.

이 절차를 확인해 보면 알겠지만 Survivor 영역 중 하나는 반드시 비어 있는 상태로 남아 있어야 한다. 만약 두 Survivor 영역에 모두 데이터가 존재하거나, 두 영역 모두 사용량이 0이라면 여러분의 시스템은 정상적인 상황이 아니라고 생각하면 된다.

> Eden 영역에 최초로 객체가 만들어지고, Survivor 영역을 통해서 Old 영역으로 오래 살아남은 객체가 이동한다는 사실은 꼭 기억하자.



#### Old 영역

Old 영역은 기본적으로 데이터가 가득 차면 GC를 실행한다. Old 영역의 GC 방식은 JDK 7을 기준으로 5가지 방식이 있다.

Serial GC
Parallel GC
Parallel Old GC(Parallel Compacting GC)
Concurrent Mark & Sweep GC(이하 CMS)
G1(Garbage First) GC

[참고](https://d2.naver.com/helloworld/1329)


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Java/java.md#java---home)
