---
tags: 
date: 2025-08-14
time: 23:56
---
# **0) 目標與範圍**

- 用 Java 21 + Spring Boot 建立 REST API（CRUD）。
    
- 內建 H2 記憶體資料庫（開發用），之後可切到 Postgres。
    
- 以 Gradle 為建置工具。
    
- 提供可跑的範例程式與 curl 驗證指令。


# 1) 安裝與確認環境
## 刪除之前的版本

找到最根目錄的地方，刪掉 `/Library/Java/JavaVirtualMachine` 下的jdk。
我刪掉了 `zulu-18.jdk` ，我不知道為什麼裝的。看資料夾時間是2022年。

## 安裝 Java 21（Temurin 版）

```bash
brew install --cask temurin21
```

### 設定 JAVA_HOME
```bash
/usr/libexec/java_home -V
# 複製 21 對應的路徑，然後：
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 21)' >> ~/.zshrc
source ~/.zshrc
```
不確定為什麼需要這麼做，GPT說很多工具都會用到這個。


[[2025-08-17|2025-08-17 Sun, 23:09]]
# 2) 建立專案骨架

兩種方式，選一：
### **方式 A：用 Spring Initializr 網頁產生（最直覺）**
- 打開：[start.spring.io](https://start.spring.io)
- Project: **Gradle - Groovy**
- Language: **Java**
- Spring Boot: **3.x（支援 Java 21）**
- Group: com.example
- Artifact: todo-api
- Dependencies：Spring Web, Spring Data JPA, Validation, H2 Database
- 下載壓縮檔，解壓後 cd todo-api

### **方式 B：用 curl 從 Initializr 直接拉（快速）**
```bash
curl https://start.spring.io/starter.zip \
  -d dependencies=web,data-jpa,validation,h2 \
  -d type=gradle-project \
  -d groupId=com.example \
  -d artifactId=todo-api \
  -d name=todo-api \
  -d javaVersion=21 \
  -o todo-api.zip

unzip todo-api.zip -d .
cd todo-api
```

我擔心使用這個工具會miss掉一些該學習的東西。
### **優點（幫你省下時間去專注學習重點）**
- 你不用卡在「為什麼我的 classpath 設錯，專案跑不起來？」這種細節。
- 能把時間花在 **Spring Boot 本身的概念**（Controller、Service、Repository、Dependency Injection）。
- 你可以更快寫出一個 API，獲得正回饋。
    
### **缺點（可能失去對底層的感知）**
- 你可能不知道 **Gradle/Maven 是怎麼解析依賴**。
- 你可能沒經歷過 **手動管理 jar 檔**的痛苦。
- 你一開始可能會誤以為「這些工具就是黑魔法」，而不是簡化的封裝。

# 3) 專案基本設定


```bash
#  3.1 建 .gitignore （若 Initializr 已附帶可略）
curl -L https://www.toptal.com/developers/gitignore/api/java,gradle,intellij,macos > .gitignore

./gradlew bootRun
# 第一次跑會下載依賴，完成後監聽在 http://localhost:8080
# Ctrl + C 可停止
```


# 4) 資料模型與資料庫設定（H2）

src/main/resources/application.properties（若不存在就建立）：
```properties
# H2（開發用）
spring.datasource.url=jdbc:h2:mem:todo;DB_CLOSE_DELAY=-1;MODE=PostgreSQL
spring.datasource.driverClassName=org.h2.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# H2 console（方便檢查資料）
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

### application.properties 在 Java（常見是 Spring Boot）專案的用途
application.properties（或 application.yml）是 Spring Boot 預設的「設定檔」，用來集中宣告應用程式的可配置參數──像資料庫連線、server port、log 等行為。Spring Boot 會自動讀取它並把裡面的鍵值映射成可注入的設定（property）供應用程式使用與自動組態 (auto-configuration)。


# 5) 建立 Todo 實體（Entity）

`src/main/java/com/example/todoapi/todo/Todo.java`

```java
package com.example.todoapi.todo;

import jakarta.persistence.*;
import jakarta.validation.constraints.NotBlank;
import java.time.OffsetDateTime;

@Entity
public class Todo {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @NotBlank
    private String title;

    private boolean completed = false;

    private OffsetDateTime createdAt = OffsetDateTime.now();
    private OffsetDateTime updatedAt = OffsetDateTime.now();

    @PreUpdate
    public void onUpdate() { this.updatedAt = OffsetDateTime.now(); }

    // getters & setters 省略或用 Lombok（若要用，請加 lombok 依賴）
    // ... getters/setters ...
}

```

> 想省樣板碼可加入 Lombok 依賴，這裡先保持零依賴。


我發現這裡我看不懂的東西可多了。

1. @ 符號是Java原生的註解（Annotation）功能，有原生的 e.g. `@Override` 。與 `//` Commentary不一樣。**地位**：屬於 Java 語言的一部分，有「**語法等級的支援**」。
2.  **JDBC** = Java Database Connectivity，Java 提供的標準 API，用來從 Java 程式連接與操作關聯式資料庫（開連線、下 SQL、讀結果）。
3. Dao 為 Data access object 的簡稱， 一個負責「與資料來源（通常是 DB）」溝通的物件／類別，封裝 CRUD 與 SQL 詳細實作。對外暴露簡單的方法（例如 save(), findById(), findAll()），把資料庫細節藏起來。 。在Clean Architecture中： 把 JDBC/SQL 實作封裝起來，提供給上層（service/use-case）使用。**DAO 是外層的細節實作**。


## **1. `@Id`**

- **來源**：`jakarta.persistence.Id`
- **用途**：  
    標示此欄位是 **主鍵 (Primary Key)**。  
    每個 JPA 實體類必須有且只有一個 `@Id` 欄位，用來唯一識別資料列。
值的產生需搭配其他註解設定。

## **2. `@GeneratedValue`**

- **來源**：`jakarta.persistence.GeneratedValue`
- **用途**：  
    告訴 JPA，**主鍵值由系統自動生成**，而不是程式手動設定。
	
`strategy` 指定生成策略，常見有四種：
1. **`GenerationType.AUTO`**
    - 預設值，JPA 會根據底層資料庫自動選擇合適策略。
2. **`GenerationType.IDENTITY`**
    - 使用資料庫的 **自動遞增 (auto-increment)** 機制，例如 MySQL 的 `AUTO_INCREMENT`，PostgreSQL 的 `SERIAL`。
    - **由資料庫在 INSERT 時生成主鍵**，JPA 在插入後再回填這個值。
3. **`GenerationType.SEQUENCE`**
    - 使用資料庫 **sequence** 產生主鍵，例如 Oracle 的 `sequence`。
    - 需搭配 `@SequenceGenerator`。
4. **`GenerationType.TABLE`**
    - 用一個獨立的表來模擬主鍵生成器，使用較少，性能較差。

# 6) Repository 介面

`src/main/java/com/example/todoapi/todo/TodoRepository.java`

`package com.example.todoapi.todo;  import org.springframework.data.jpa.repository.JpaRepository;  public interface TodoRepository extends JpaRepository<Todo, Long> {}`

```java
package com.example.todoapi.todo;

import org.springframework.data.jpa.repository.JpaRepository;


public interface TodoRepository extends JpaRepository<Todo, Long> {}

```

---

# 7) DTO 與驗證（可維持 API 輸入/輸出乾淨）

`src/main/java/com/example/todoapi/todo/TodoDtos.java`

```java
package com.example.todoapi.todo;

import jakarta.validation.constraints.NotBlank;

public class TodoDtos {

    public record CreateReq(@NotBlank String title) {}
    public record UpdateReq(String title, Boolean completed) {}

    public record Resp(Long id, String title, boolean completed) {
        public static Resp from(Todo t) {
            return new Resp(t.getId(), t.getTitle(), t.isCompleted());
        }
    }
}
```

## `record` 的概念

- `record` 是 Java 14 引入、Java 16 正式版的特性，目的是快速定義不可變的資料結構。
- 編譯器會自動幫你生成：
    - `private final` 欄位
    - 全參數建構子
    - `equals()`、`hashCode()`、`toString()`
    - 欄位的存取方法（例如 `title()`）
- 適合用來定義 DTO 或純資料模型。

#### 巢狀型別
```java
  class Outer {
      static class Inner {}
  }
```
使用時就是 `Outer.Inner`。

在這裡，`TodoDtos` 是外層容器，`CreateReq`、`UpdateReq`、`Resp` 是它的**內部型別 (nested record)**，用來分組管理 DTO，避免散落在檔案各處。


```java 
  public record CreateReq(@NotBlank String title) {}
```
看起來像「函式定義」，但其實是「型別定義」，它幫你自動生成：
- 一個不可變類別，內含 title 欄位
- 一個全參數建構子
- title() 方法
- equals()、hashCode()、toString()
所以 CreateReq 是一個類別（型別），不是函式。


# 8) Service（商業邏輯層，保持 Controller 精簡）

`src/main/java/com/example/todoapi/todo/TodoService.java`
```java
  package com.example.todoapi.todo;
  
  import org.springframework.stereotype.Service;
  import org.springframework.transaction.annotation.Transactional;
  import java.util.List;
  
  @Service
  @Transactional
  public class TodoService {
      private final TodoRepository repo;
  
      public TodoService(TodoRepository repo) { this.repo = repo; }
  
      public List<Todo> list() { return repo.findAll(); }
  
      public Todo create(String title) {
          Todo t = new Todo();
          t.setTitle(title);
          return repo.save(t);
      }
  
      public Todo get(Long id) { return repo.findById(id).orElseThrow(); }
  
      public Todo update(Long id, String newTitle, Boolean completed) {
          Todo t = get(id);
          if (newTitle != null) t.setTitle(newTitle);
          if (completed != null) t.setCompleted(completed);
          return repo.save(t);
      }
  
      public void delete(Long id) { repo.deleteById(id); }
  }
  
```

## `@Transactional` 的作用

- **來源**：`org.springframework.transaction.annotation.Transactional`
- **用途**：
    - 讓該類別或方法執行時在 Spring 管理的 **交易（Transaction）** 中執行。
    - Spring 會用 AOP（動態代理）攔截呼叫，在方法進入前開啟交易，方法結束後提交 (commit)，若發生例外則回滾 (rollback)。
- **加在類別上的效果**：
    - **是的，會套用到此類別所有公開 (public) 方法**，等同於在每個 public 方法上都標註 `@Transactional`。
    - 如果類別和方法同時標註，以**方法上的設定優先**。


# 9) REST Controller（API 介面）

`src/main/java/com/example/todoapi/todo/TodoController.java`
```java
  package com.example.todoapi.todo;
  
  import org.springframework.http.HttpStatus;
  import org.springframework.web.bind.annotation.*;
  import jakarta.validation.Valid;
  import java.util.List;
  
  import static com.example.todoapi.todo.TodoDtos.*;
  
  @RestController
  @RequestMapping("/api/todos")
  public class TodoController {
      private final TodoService service;
      public TodoController(TodoService service) { this.service = service; }
  
      @GetMapping
      public List<Resp> list() {
          return service.list().stream().map(Resp::from).toList();
      }
  
      @PostMapping
      @ResponseStatus(HttpStatus.CREATED)
      public Resp create(@Valid @RequestBody CreateReq req) {
          return Resp.from(service.create(req.title()));
      }
  
      @GetMapping("/{id}")
      public Resp get(@PathVariable Long id) {
          return Resp.from(service.get(id));
      }
  
      @PatchMapping("/{id}")
      public Resp update(@PathVariable Long id, @RequestBody UpdateReq req) {
          return Resp.from(service.update(id, req.title(), req.completed()));
      }
  
      @DeleteMapping("/{id}")
      @ResponseStatus(HttpStatus.NO_CONTENT)
      public void delete(@PathVariable Long id) {
          service.delete(id);
      }
  }
```