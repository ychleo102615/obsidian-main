---
tags: []
date: 2025-08-24
time: 12:36
---
# 10) 啟動與驗證 API

## 10.1 啟動

`./gradlew bootRun # or ./gradlew build && java -jar build/libs/todo-api-*.jar`

## 10.2 用 `curl` 驗證（另一個終端機）

### 建立 Todo

`curl -X POST http://localhost:8080/api/todos \   -H "Content-Type: application/json" \   -d '{"title":"Buy milk"}'`

### 列出 Todos

`curl http://localhost:8080/api/todos`

### 取得單一 Todo

`curl http://localhost:8080/api/todos/1`

### 局部更新（完成狀態）

`curl -X PATCH http://localhost:8080/api/todos/1 \   -H "Content-Type: application/json" \   -d '{"completed": true}'`

### 刪除

`curl -X DELETE http://localhost:8080/api/todos/1`

（開發中可用 `http://localhost:8080/h2-console` 觀察資料表，JDBC URL：`jdbc:h2:mem:todo`）


# 11) 自動化測試（最小可行）

`src/test/java/com/example/todoapi/todo/TodoControllerTest.java`

```java
  package com.example.todoapi.todo;
  
  import org.junit.jupiter.api.Test;
  import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
  import org.springframework.boot.test.context.SpringBootTest;
  import org.springframework.test.web.servlet.MockMvc;
  import org.springframework.beans.factory.annotation.Autowired;
  
  import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
  import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;
  
  @SpringBootTest
  @AutoConfigureMockMvc
  class TodoControllerTest {
  
      @Autowired MockMvc mvc;
  
      @Test
ㄨ      void createTodo() throws Exception {
          mvc.perform(post("/api/todos")
                  .contentType("application/json")
                  .content("""
                      {"title":"Test item"}
                  """))
             .andExpect(status().isCreated())
             .andExpect(jsonPath("$.title").value("Test item"))
             .andExpect(jsonPath("$.completed").value(false));
      }
  }

```

執行：

`./gradlew test`


- 用 MockMvc 搭配 `@SpringBootTest` 時，就是在模擬整個 application 的行為，所以屬於整合測試。
- mvc 代表model view controller，spring 的 view 代表用戶端可用的輸出格式，如html, json, pdf


# 12) 常見加值事項（依需要選做）
- **Swagger / OpenAPI**：加上 `springdoc-openapi-starter-webmvc-ui` 依賴，即可在 `/swagger-ui.html` 看互動文件。
- **資料持久化到 Postgres**：把 H2 換成 Postgres（Docker 起一個 DB），修改 `application.properties`。
- **分層結構**：保持 `controller / service / repository / domain` 清晰。
- **格式檢查**：加入 Spotless（Java formatter）確保一致風格。
- **容器化**：寫 `Dockerfile` 與 `docker-compose.yml` 方便部署。


---

# 13) API 介面一覽（你提到的第 3 點）

| 方法     | 路徑                | 說明   | 請求體 (JSON)                       | 回應體 (JSON)               |
| ------ | ----------------- | ---- | -------------------------------- | ------------------------ |
| GET    | `/api/todos`      | 列出全部 | —                                | `[{id,title,completed}]` |
| POST   | `/api/todos`      | 新增一筆 | `{ "title": "string" }`          | `{id,title,completed}`   |
| GET    | `/api/todos/{id}` | 取得單一 | —                                | `{id,title,completed}`   |
| PATCH  | `/api/todos/{id}` | 局部更新 | `{ "title":"?", "completed":? }` | `{id,title,completed}`   |
| DELETE | `/api/todos/{id}` | 刪除   | —                                | 204 No Content           |



# 如何在 Spring Boot 專案中加入Swagger / OpenAPI？

在 `build.gradle` 加入：

`dependencies {     implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.5.0' }`

啟動後打開：

`http://localhost:8080/swagger-ui.html`

即可看到互動式 API 文件。




# Gradle 使用 Spotless

`plugins {     id 'com.diffplug.spotless' version '6.25.0' }  spotless {     java {         googleJavaFormat() // 使用 Google Java 格式化風格         target 'src/**/*.java' // 格式化目標檔案     } }`

- 檢查格式：`./gradlew spotlessCheck`
    
- 自動修正格式：`./gradlew spotlessApply`




後續：CI/CD ?