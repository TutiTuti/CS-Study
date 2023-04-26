# 데이터베이스에서 인덱스를 사용하는 이유
장단점에 대해 설명해주세요.

## ▪ 인덱스란?  INDEX

> **인덱스(Index)**는 **데이터베이스의 테이블에 대한 검색 속도를 향상 시켜주는  
자료구조 이다**.  ( 책의 목차 )
> 

### 예시 [[database] DB 인덱스(INDEX)란? | 코딩장이 (itholic.github.io)](https://itholic.github.io/database-index/)

서점에 진열된 책들의 이름, 카테고리, 위치를 저장한 테이블(book_store)에 
10000권의 책 데이터가 랜덤으로 저장 되어있다.

| rowid | name | category | location |
| --- | --- | --- | --- |
| 1 | let’s start java | java | A |
| 2 | python basic | python | K |
| 3 | js for seinor | javascript | B |
| 4 | let’s start java | java | C |
| … | … | … | … |
| 4222 | java? java! | java | Z |
| 4223 | pythonic thinking | python | A |
| … | … | … | … |
| 9999 | javavara | java | K |
| 10000 | i love C++ | C++ | N |

여기서 java라는 카테고리의 책의 이름,위치를 찾기 위해 쿼리문을 입력

```jsx
SELECT name,location FROM book_store WHERE category=’java’
```

현재 인덱스가 없기 때문에 컴퓨터는 10000개를 전부다 스캔해서 결과를 찾는다.

```jsx
CREATE INDE* index_category ON book_store(category)
```

명령어를 이용해 인덱스를 생성하면 category를 기준으로 데이터가 정렬되어 있기 
때문에 다시 쿼리문을 입력하면 데이터를 전보다 빠르게 찾을 수 있다.

### 인덱스 구조

인덱스 구조는 대표적으로 **해시(Hash table)와 B+tree** 가 있다.

**해시**는 ( Key와 Value )로 쌍을 표현하며 값을 구하는 방식이다.
해시 충돌이라는 변수가 존재하지만 평균적으로 **O(1)**의 원하는 데이터를 탐색할 수 있는 구조이나 부등호 연산을 자주 사용하는 데이터베이스에서는 잘 사용하지 않는다.

**B+tree**는 기존의 B-tree의 full scan시 모든 노드를 돌아야 하는 단점을 개선한 구조이다.
특징으로 B+tree는 **leaf node에만 데이터를 저장**하고 나머지 node에는 자식 포인터만 저장한다.
**leaf node끼리는 Linked list로 연결**되어서 full scan, 순차검색연산을 효율적으로 할 수 있다.


![776 PNG](https://user-images.githubusercontent.com/37789623/234503739-7bff4c48-7b33-4b90-b2f5-4005a4a3925e.png)

**B+tree 예시** [데이터베이스 인덱스는 왜 'B-Tree'를 선택하였는가 :: 이뇽의세상 (tistory.com)](https://helloinyong.tistory.com/296)

### ▪ 장점 / 단점

### (장) 데이터를 빠르게 찾을 수 있다!

조건검색 Where 절의 효율성
정렬 Order by 절의 효율성
Min, Max의 효율적인 처리 

### (단) DML에 취약

SELECT를 제외한 **INSERT, UPDATE, DELETE**에서 데이터가 추가되거나 바뀐다면 테이블 내의
값을 다시 정렬해줘야 하며 INDEX테이블과 원본 테이블 두 군데의 데이터 수정 작업을 해줘야 한다.

### (단) 약 10%의 추가 저장 공간이 필요하다.

속도 향상을 위해 인덱스를 많이 생성을 하는 경우 그만큼 공간이 더 필요하고 관리 비용이
많이 올라 갈 수 있다.

### (단) 잘못 사용하는 경우 오히려 검색 성능 저하

인덱스는 테이블의 전체 데이터 중에서 **10~15% 이하의 데이터를 처리하는 경우에만 효율적**이고 그 이상의 데이터를 처리하거나 **데이터 형태**에 따라 인덱스를 사용하지 않는 것이 더 낫다.
ex>성별같이 범위가 좁은 경우 인덱스를 읽고 다시 많은 데이터를 조회해야 한다.
