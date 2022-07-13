---
tags: aws rds mysql connection-pool maximum nodejs
---

# maximum connections

## max_connections
개발바닥 유튜브 보다가 인프런 Node.js 서버 장애 이야기를 접하게 되었다.
트래픽이 엄청 몰릴 때 ECS service auto-scaling max capacity를 100까지 (단일 서버 100대!) 올려 돌리는데도 해결되지 않았던 문제의 진범은 DB max_connections 이었다는 SSUL.
(lock queries, slow queries, .. 당시 상황이 복잡했던 다른 이유들도 말씀해주셨지만)

![](attachments/2022-07-13-13-12-41.png)

AWS 공식 문서를 보니 max_connections 값은 다음과 같이 계산된다는데,
`max_connections = DBInstanceClassMemory/12582880`

가령, 내가 지금 관심 있는 db.t3.medium 의 경우 RAM이 4GB인데, 이렇게 확인해보면 307개라고 나온다.
```sql
SHOW GLOBAL VARIABLES LIKE 'max_connections';
```
![](attachments/2022-07-13-13-13-22.png)

## NestJS + TypeORM + mysql
현재 위와 같은 환경으로 작업하고 있고, mysql 의 pool option을 살펴보면, connectionLimit default 값이 `10`으로 되어 있는데,
다음과 같이 extra 에 넣어주면 적용되겠다.

```typescript
export const AppDataSource = new DataSource({     
  type: "mysql",     
  host: "localhost",     
  port: 3306,     
  username: "test",     
  password: "test",     
  database: "test",     
  extra: {
    connectionLimit: 20,
  }
})
```

> References
> - https://www.youtube.com/watch?v=52t9DlwmqJI&ab_channel=%EA%B0%9C%EB%B0%9C%EB%B0%94%EB%8B%A5
> - https://aws.amazon.com/ko/premiumsupport/knowledge-center/rds-mysql-max-connections/
> - https://github.com/mysqljs/mysql#pool-options
> - https://typeorm.io/#quick-start
