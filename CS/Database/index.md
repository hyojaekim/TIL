# [Database](https://github.com/hyojaekim/TIL/tree/master/Database) / [🏠 Home](https://github.com/hyojaekim/TIL)

## 인덱스(Index)

### 정의

RDBMS에서 검색속도를 높이기 사용하는 기술.
INDEX는 색인이고, 해당 TABLE 컬럼을 색인화(따로 파일로 저장)한다.

검색시 해당 TABLE의 레코드를 full scan 하는게 아니라 색인화 되어있는 INDEX 파일을 검색하여 검색속도를 빠르게 한다.

실제로는 RDBMS 에서 사용되는 B-Tree 는 B-Tree 에서 파생된 B+ Tree 를 사용한다.

### 원리

INDEX를 해당 컬럼에 주게 되면 초기 TABLE생성시 만들어진 MYD,MYI,FRM 3개의 파일중에서 MYI에 해당 컬럼을 색인화 하여 저장한다.

INDEX를 해당 컬럼에 만들게 되면 해당 컬럼을 따로 인덱싱하여 MYI 파일에 입력한다. 그래서 사용자가 SELECT쿼리로 INDEX가 사용하는 쿼리를 사용시 해당 TABLE을 검색하는것이 아니라 빠른 TREE로 정리해둔 MYI파일의 내용을 검색한다.

이는 책의 뒷부분에 찾아보기와 같은 의미로 정리해둔 단어 중에서 원하는 단어를 찾아서 페이지 수를 보고 쉽게 찾을수 있는 개념과 같다.

### 사용해야 하는 경우와 그렇지 않은 경우

- **WHERE절에서 사용되는 컬럼**을 인덱스로 만든다.
- **데이터의 중복도가 높은 열은 인덱스로 만들어도 효용이 없다.** (예 : 성별, 타입이 별로 없는 경우, 적은경우)
- **외래키가 사용되는 열에는 인덱스를 되도록 생성**해주는 것이 좋다.
- **JOIN에 자주 사용되는 열에는 인덱스를 생성**해주는 것이 좋다.
- **INSERT / UPDATE / DELETE가 자주 일어나는지를 고려한다.**
- **사용하지 않는 인덱스는 제거하자**


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Database/index.md#Database---home)
