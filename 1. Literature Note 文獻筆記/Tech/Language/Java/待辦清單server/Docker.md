---
tags: []
date: 2025-08-24
time: 17:32
---
# 1) 新增 Postgres 依賴、移除 H2（或暫時關掉）

**build.gradle**

```properties
dependencies {
    // Web / JPA / Validation 依舊保留
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-validation'

    // ① 新增 Postgres JDBC Driver（讓 Spring 會用 PostgreSQL）
    runtimeOnly 'org.postgresql:postgresql'

    // ② （選）移除或註解掉 H2
    // runtimeOnly 'com.h2database:h2'
}

```

> `org.postgresql:postgresql` 的版本由 Spring Boot BOM 管理，通常不用寫版本號。

---

# 2) 用 Docker 起一個 Postgres

在專案根目錄新增 **docker-compose.yml**：

```yml
version: "3.8"
services:
  postgres:
    image: postgres:16
    container_name: todo-postgres
    environment:
      POSTGRES_DB: todo
      POSTGRES_USER: todo
      POSTGRES_PASSWORD: changeit
      TZ: Asia/Taipei
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $$POSTGRES_USER -d $$POSTGRES_DB"]
      interval: 5s
      timeout: 5s
      retries: 20

volumes:
  pgdata:

```

啟動資料庫：

```bash
docker compose up -d # 檢查 
docker compose ps #（可選）看日誌 
docker logs -f todo-postgres
```

[[SQL 大小寫使用哲學]]