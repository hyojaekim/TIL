# 기초적인 페이징 구현 방식의 문제점(offset & limit)
기초적인 페이징 구현 방식은 페이지 번호(offset)와 페이지 사이즈(limit)를 기반으로 구현한 방식을 뜻한다.

기초적인 페이징 구현 방식은 데이터가 많아짐에 따라 장애를 유발할 수 있다.

인덱스를 이용한 쿼리 튜닝이 가장 먼저 최우선 되어야 하지만, 억 단위인 테이블에서 페이징은 인덱스만 태운다고 해결되지는 않는다.

* 기초적인 페이징 구현 방식은 뒤로 갈 수록 느리다. 결국 앞에서 읽었던 행을 다시 읽어야 하기 때문이다.
  * 예시) offset (100,000), limit (20) → 결국에는 100,020개의 행을 읽어야 한다.

# No Offset이 무엇일까?
페이지 번호가 없는 방식을 뜻한다. *(페이스북이나 인스타그램은 페이징을 무한 스크롤 방식을 이용한다)*

No Offset은 기초적인 페이징 구현 방식이랑 달리 offset을 이용하지 않는다.

조회 시작 부분을 인덱스로 빠르게 찾는 방식을 이용한다.

따라서 인덱스로 인해 페이지가 뒤쪽에 있더라도 항상 동일한 성능을 가질 수 있다.

예시) 인덱스로 빠르게 찾는 방식

```sql
SELECT
    *
FROM
    USER
WHERE
    ~~~
    AND id < 마지막으로 조회한 ID
ORDER BY
    id DESC
LIMIT
    페이지 사이즈
```

# [TODO] No Offset 구조는 어떤 단점이 있을까? 
1. where에 사용되는 기준이 되는 Key가 중복이 가능할 경우
2. 현재 상황에서 무조건 페이징 버튼 형식으로만 해야 하는 경우
