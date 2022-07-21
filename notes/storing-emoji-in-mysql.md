---
tags: aws database rds mysql emoji unicode charset
---

# Storing emoji in AWS RDS MySQL

1. parameter group에서 다음 각 호에 해당하는 녀석들 값 변경
    - character_set_client = utf8mb4
    - character_set_connection = utf8mb4
    - character_set_database = utf8mb4
    - character_set_results = utf8mb4
    - character_set_server = utf8mb4
    - collation_connection = utf8mb4_unicode_ci
    - collation_server = utf8mb4_unicode_ci
2. parameter group을 db instance에 적용하고 재부팅
3. 확인해보고
    ```sql
    SHOW GLOBAL VARIABLES WHERE Variable_name LIKE 'character\_set\_%' OR Variable_name LIKE 'collation%'
    ```
4. database, table, column 모조리 다 바꿔줘야 함
    - database
        ```sql
        ALTER DATABASE db CHARACTER SET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
        ```
    - table
        ```sql
        ALTER TABLE tbl DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
        ``` 
    - column
        ```sql
        ALTER TABLE tbl MODIFY COLUMN col TEXT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci NULL;
        ``` 
