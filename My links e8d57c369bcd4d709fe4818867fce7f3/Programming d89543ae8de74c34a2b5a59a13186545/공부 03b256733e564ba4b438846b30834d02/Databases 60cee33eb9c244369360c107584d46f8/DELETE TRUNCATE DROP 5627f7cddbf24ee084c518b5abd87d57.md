# DELETE/TRUNCATE/DROP

1) DELETE

- WHERE 절을 사용하여 테이블에 있는 데이터를 하나하나 선택하여 제거하는 방식
- WHERE 절을 사용하지 않고 테이블의모든 데이터를 삭제 하더라도, 내부적으로는 한줄 한줄 일일이 제거하는 과정을 거침.
- 처리속도가 늦고, 퍼포먼스에 좋지 않은 영향을 줄 수 있음
- 원하는 데이터만 골라서 삭제할 때에는 DELETE 사용 / 전체 데이터 삭제할 때에는 TRUNCATE 사용
- 데이터를 삭제 하더라도 데이터가 담겨있던 Storage는 Release 되지 않는다.
- DELETE된 데이터는 COMMIT 명령어를 사용하기 전이라면, ROLLBACK 명령어를 통해 되돌릴 수 있음
    
    ```sql
    DELETE FROM dbtable;
    DELETE FROM dbtable WHERE {조건};
    ROLLBACK;
    COMMIT;
    ```
    

2) TRUNCATE 

- 전체데이터를 한번에 삭제하는 방식 (↔DELETE)
- 최초 생성되었을 당시의 Storage만 남기고, 데이터가 남겨있던 Storage는 Release 된다.
- TRUNCATE TABLE 을 하면 CREATE TABLE을 한 직후 상태와 같다.
- 자동 COMMIT이 되는 명령어이기 때문에, 이미 지운 데이터는 되돌릴 수 없다.
    
    ```sql
    TRUNCATE TABLE dbtable;
    ```
    

3) DROP

- 테이블 자체를 완전히 날려버리는 방식 → 처음부터 없었던 테이블처럼
- 테이블 자체가 모두 지워지며, 해당 테이블에 생성되어있던 모든 인덱스도 사라진다
- 자동 COMMIT이 되는 명령어이기 때문에, 이미 지운 데이터는 되돌릴 수 없다.

```sql
DROP TABLE dbtable;$
```

![Untitled](DELETE%20TRUNCATE%20DROP%205627f7cddbf24ee084c518b5abd87d57/Untitled.png)

![Untitled](DELETE%20TRUNCATE%20DROP%205627f7cddbf24ee084c518b5abd87d57/Untitled%201.png)