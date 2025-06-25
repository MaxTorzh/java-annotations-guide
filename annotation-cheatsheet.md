# 📚 Lombok, Spring Boot & Jakarta Annotations Guide

Краткий справочник по самым полезным аннотациям с примерами и объяснениями.  
*Для тех, кто устал гуглить одно и то же*.

---

## 🛠️ **Lombok Annotations**

>**Lombok** — это библиотека, которая помогает избавиться от *boilerplate-кода* в Java: `геттеры`, `сеттеры`, `конструкторы`, `toString()`, `equals()` `и т.д.` создаются автоматически.

### **Генерация кода**
| Аннотация                 | Описание                                                                                            | Пример |
|---------------------------|-----------------------------------------------------------------------------------------------------|--------|
| `@Getter`/`@Setter`       | Генерирует геттеры/сеттеры для полей класса.                                                        | [Пример](#пример-1) |
| `@toString`               | Генерирует метод `toString()` с полями класса.                                                      | [Пример](#пример-2) |
| `@EqualsAndHashCode`      | Генерирует методы `equals() и `hashCode().                                                          | [Пример](#пример-3) |
| `@Data`                   | Комбинирует `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode` и `@RequiredArgsConstructor`.   | [Пример](#пример-4) |
| `@NoArgsConstructor`      | Создает конструктор без аргументов.                                                                 | [Пример](#пример-5) |
| `@AllArgsConstructor`     | Создает конструктор со всеми полями.                                                                | [Пример](#пример-6) |
| `@RequiredArgsConstructor`| Создает конструктор только для final или @NonNull полей.                                            | [Пример](#пример-7) |
| `@Value`                  | Неизменяемый объект (final поля, без сеттеров).                                                     | [Пример](#пример-8) |
| `@Builder`                | Паттерн Builder для удобного создания объектов.                                                     | [Пример](#пример-9) |
| `@Slf4j`                  | Добавляет логгер log через SLF4J.                                                                   | [Пример](#пример-10) |

---

## 🌱 **Spring Boot Annotations**

>**Spring Boot** — фреймворк для быстрой разработки Java-приложений. Он использует *аннотации* вместо *XML-конфигураций*, чтобы сделать код более читаемым и поддерживаемым.

### **Генерация кода**
| Аннотация                 | Описание                                                                                            | Пример |
|---------------------------|-----------------------------------------------------------------------------------------------------|--------|
| `@SpringBootApplication`  | Стартовая точка приложения. Объединяет @Configuration, @EnableAutoConfiguration, @ComponentScan.    | [Пример](#пример-11) |
| `@RestController`         | Объединяет @Controller и @ResponseBody.                                                             | [Пример](#пример-12) |
| `@RequestMapping`         | Задаёт базовый URL для контроллера или метода.                                                      | [Пример](#пример-13) |
| `@GetMapping`, `@PostMapping` и др.| Упрощённые версии @RequestMapping для HTTP-методов GET, POST и т.д.                        | [Пример](#пример-14) |
| `@Autowired`              | Внедряет зависимости (DI — Dependency Injection).                                                   | [Пример](#пример-15) |
| `@Service`, `@Repository`, `@Component`| Маркируют классы как компоненты Spring.                                                | [Пример](#пример-16) |
| `@Configuration`          | Класс содержит определения бинов.                                                                   | [Пример](#пример-17) |
| `@Bean`                   | Регистрирует метод как бин в контексте Spring.                                                      | [Пример](#пример-18) |
| `@Value`                  | Внедряет значения из application.properties.                                                        | [Пример](#пример-19) |
| `@Profile`                | Активирует бины только для указанного профиля.                                                      | [Пример](#пример-20) |

---

## ☕ **Jakarta (ранее Java EE) Annotations**

>**Jakarta EE** — стандарт для enterprise-разработки на Java. Используется для создания серверных приложений, REST API, сервлетов, JPA-сущностей и т.д.

### **Генерация кода**
| Аннотация                 | Описание                                                                                            | Пример |
|---------------------------|-----------------------------------------------------------------------------------------------------|--------|
| `@Entity`                 | Указывает, что класс является JPA-сущностью.                                                        | [Пример](#пример-21) |
| `@Table`                  | Задаёт имя таблицы в БД.                                                                            | [Пример](#пример-22) |
| `@Id`                     | Первичный ключ сущности.                                                                            | [Пример](#пример-23) |
| `@GeneratedValue`         | Стратегия генерации ID (например, GenerationType.IDENTITY).                                         | [Пример](#пример-24) |
| `@Column`                 | Настройка столбца базы данных.                                                                      | [Пример](#пример-25) |
| `@OneToMany`, `@ManyToOne`, `@ManyToMany`, `@OneToOne`| Связи между сущностями.                                                 | [Пример](#пример-26) |
| `@JoinColumn`             | Настраивает внешний ключ.                                                                           | [Пример](#пример-27) |
| `@Transient`                   | Поле не сохраняется в БД.                                                      | [Пример](#пример-28) |
| `@Enumerated`                  | Сохраняет enum в БД (например, EnumType.STRING).                                                        | [Пример](#пример-29) |
| `@CreationTimestamp`, `@UpdateTimestamp` (Hibernate)   | Автоматически обновляет даты создания/обновления.                      | [Пример](#пример-30) |

---


#### **Примеры**


---


<a name="пример-1"></a>
**`@Getter`/`@Setter`**
```java
public class User {
    @Getter @Setter
    private String name;

    @Getter
    private int age;
}
```


**Сгенерированный код:**
```java
public String getName() { return name; }
public void setName(String name) { this.name = name; }

public int getAge() { return age; }
// setAge() не генерируется для age
```


*Генерирует методы `getXXX()` и `setXXX()` для полей.*

*Можно ли использовать на уровне поля?* - **✅ Да.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-2"></a>
**`@toString`**
```java
@ToString(of = {"name"})
public class User {
    private String name;
    private int age;
// toString() будет содержать только name.
}
```


**Сгенерированный код:**
```java
public class User {
    private String name;
    private int age;

    @Override
    public String toString() {
        return "User(name=" + name + ")";
    }
}
```

*Генерирует метод toString(), включающий значения указанных полей.*

*Можно ли использовать на уровне поля?* - **✅ Да.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-3"></a>
**`@EqualsAndHashCode`**
```java
@EqualsAndHashCode(of = {"name"})
public class User {
    private String name;
    private int age;
// equals() и hashCode() будут учитывать только поле name.
}
```


**Сгенерированный код:**
```java
public class User {
    private String name;
    private int age;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User)) return false;

        User user = (User) o;

        return name != null ? name.equals(user.name) : user.name == null;
    }

    @Override
    public int hashCode() {
        return name != null ? name.hashCode() : 0;
    }
}
```

*Генерирует методы equals() и hashCode() на основе указанных полей.*

*Можно ли использовать на уровне поля?* - **✅ Да.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-4"></a>
**`@Data`**  
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private Long id;
    private String name;
}
```


**Сгенерированный код:**
```java
public class User {
    private Long id;
    private String name;

    public User() {}

    public User(Long id, String name) {
        this.id = id;
        this.name = name;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User(id=" + id + ", name=" + name + ")";
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User)) return false;

        User user = (User) o;

        if (id != null ? !id.equals(user.id) : user.id != null) return false;
        return name != null ? name.equals(user.name) : user.name == null;
    }

    @Override
    public int hashCode() {
        int result = id != null ? id.hashCode() : 0;
        result = 31 * result + (name != null ? name.hashCode() : 0);
        return result;
    }
}
```

`@Data` - *генерирует все стандартные методы: `геттеры`, `сеттеры`, `toString()`, `equals()`, `hashCode()`.* 

`@AllArgsConstructor` - *создаёт конструктор со всеми полями.* 

`@NoArgsConstructor` - *конструктор без аргументов.*

*Можно ли использовать на уровне поля?* - **✅ Да.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-5"></a>
**`@NoArgsConstructor`**  
```java
@NoArgsConstructor
public class User {
    private String name;
}
```

**Сгенерированный код:**
```java
public User() {}
```

*Генерирует конструктор без аргументов.*

*Можно ли использовать на уровне поля?* - **❌ Нет.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-6"></a>
**`@AllArgsConstructor`**  
```java
@AllArgsConstructor
public class User {
    private String name;
    private int age;
}
```

**Сгенерированный код:**
```java
public User(String name, int age) {
    this.name = name;
    this.age = age;
}
```

*Генерирует конструктор со всеми полями.*

*Можно ли использовать на уровне поля?* - **❌ Нет.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-7"></a>
**`@RequiredArgsConstructor`**  
```java
@RequiredArgsConstructor
public class User {
    private final String name;
    private int age;
}
```

**Сгенерированный код:**
```java
public User(String name) {
    this.name = name;
}
```

*Генерирует конструктор только для final полей или полей с аннотацией @NonNull.*

*Можно ли использовать на уровне поля?* - **❌ Нет.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-8"></a>
**`@Value`**  
```java
@Value
public class User {
    String name;
    int age;
}
```


**Сгенерированный код:**
```java
public final class User {
    private final String name;
    private final int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return this.name;
    }

    public int getAge() {
        return this.age;
    }

    public String toString() {
        return "User(name=" + this.name + ", age=" + this.age + ")";
    }

    public boolean equals(Object o) {
        // реализация equals
    }

    public int hashCode() {
        // реализация hashCode
    }
}
```

*Создаёт неизменяемый (immutable) класс: все поля автоматически становятся private final, сеттеры не создаются, а также генерируются:*

`toString()`

`equals()` / `hashCode()`

`getter (в виде getXxx())`

`requiredArgsConstructor()` для всех final полей


*Можно ли использовать на уровне поля?* - **❌ Нет.** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-9"></a>
**`@Builder`**  
```java
@Builder
public class Product {
    private String name;
    @Builder.Default
    private int quantity = 1;
    private double price;
}
```


**Сгенерированный код:**
```java
public class Product {
    private String name;
    private int quantity = 1;
    private double price;

    Product(String name, int quantity, double price) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
    }

    public static ProductBuilder builder() {
        return new ProductBuilder();
    }

    public static class ProductBuilder {
        private String name;
        private int quantity = 1;
        private double price;

        ProductBuilder() {}

        public ProductBuilder name(String name) {
            this.name = name;
            return this;
        }

        public ProductBuilder quantity(int quantity) {
            this.quantity = quantity;
            return this;
        }

        public ProductBuilder price(double price) {
            this.price = price;
            return this;
        }

        public Product build() {
            return new Product(name, quantity, price);
        }
    }
}
```

*Реализует паттерн Builder, позволяя создавать объекты пошагово, особенно удобно для классов с множеством полей или необязательных параметров.*

*Можно ли использовать на уровне поля?* - **✅ Да (с `@Builder.Default`).** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


**Пример с `@Builder.Default`:**
```java
@Builder
public class Product {
    private String name;
    @Builder.Default
    private int quantity = 1;
    private double price;
}
```

**Сгенерированный код:**
```java
public class Product {
    private String name;
    private int quantity = 1;
    private double price;

    Product(String name, int quantity, double price) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
    }

    public static ProductBuilder builder() {
        return new ProductBuilder();
    }

    public static class ProductBuilder {
        private String name;
        private int quantity = 1;
        private double price;

        ProductBuilder() {}

        public ProductBuilder name(String name) {
            this.name = name;
            return this;
        }

        public ProductBuilder quantity(int quantity) {
            this.quantity = quantity;
            return this;
        }

        public ProductBuilder price(double price) {
            this.price = price;
            return this;
        }

        public Product build() {
            return new Product(name, quantity, price);
        }
    }
}
```

*@Builder.Default позволяет задать значение по умолчанию, которое не перезаписывается, если явно не указано.*

**🛠 Как использовать:**
```java
Product product = Product.builder()
    .name("Laptop")
    .price(999.99)
    .build(); // quantity будет 1 по умолчанию
```


---


<a name="пример-10"></a>
**`@Slf4j`**  
```java
@Slf4j
public class Example {
    public void doSomething() {
        log.info("Hello from Lombok!");
    }
}
```

**Сгенерированный код:**
```java
public class Example {
    private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(Example.class);

    public void doSomething() {
        log.info("Hello from Lombok!");
    }
}
```

*Генерирует конструктор только для final полей или полей с аннотацией @NonNull.*

*Можно ли использовать на уровне поля?* - **❌ Нет** 

*Можно ли использовать на уровне класса?* - **✅ Да.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**


---


<a name="пример-11"></a>
**`@SpringBootApplication`**  
```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

*Точка входа Spring Boot*

`@SpringBootApplication` *объединяет:*

        @Configuration — *класс содержит бины.*

        @EnableAutoConfiguration — *автоматическая настройка Spring.*

        @ComponentScan — *поиск компонентов.*


---


<a name="пример-12"></a>
**`@RestController`**  
```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return "User ID: " + id;
    }
}
```

`@RestController` = `@Controller` + `@ResponseBody`

`@PathVariable` - *извлекает значения из URL-пути и передает их в параметры метода контроллера.*

`@GetMapping` — *обрабатывает `GET`-запросы*


---


<a name="пример-13"></a>
**`@RequestMapping`**  
```java
@RequestMapping("/users")
public class UserController {
    @RequestMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return "User ID: " + id;
    }
}
```

`@RequestMapping` - *задаёт базовый URL для контроллера или метода.*

`@PathVariable` - *извлекает значения из URL-пути и передает их в параметры метода контроллера.*

*/users/{id} будет обрабатываться методом getUser*

*Можно указать HTTP-метод через параметр: method = RequestMethod.GET*


---


<a name="пример-14"></a>
**`@GetMapping`, `@PostMapping` и др.**  
```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping("/{id}")
    public String getUser(@PathVariable Long id) {
        return "User ID: " + id;
    }

    @PostMapping
    public String createUser(@RequestBody String body) {
        return "Received: " + body;
    }
}
```

`@GetMapping`, `@PostMapping` и др. - *упрощённые версии @RequestMapping для конкретных HTTP-методов.*

`@GetMapping` = `@RequestMapping(method = RequestMethod.GET)`

`@PostMapping` = `@RequestMapping(method = RequestMethod.POST)` *и т.д.*

`@PathVariable` - *извлекает значения из URL-пути и передает их в параметры метода контроллера.*

*Автоматически применяет @ResponseBody*

`@RequestBody` - *преобразует тело HTTP-запроса (обычно JSON или XML) в Java-объект. Используется в REST API для приема данных от клиента (например, при POST/PUT-запросах).*


---


<a name="пример-15"></a>
**`@Autowired`**  
```java
@Service
public class MyService {
    public String getMessage() {
        return "Hello from Service";
    }
}

@RestController
public class MyController {
    @Autowired
    private MyService myService;

    @GetMapping("/message")
    public String getMessage() {
        return myService.getMessage();
    }
}
```

`@Autowired` - *внедряет зависимости (DI — Dependency Injection).*

*Spring автоматически создаёт и внедряет экземпляр MyService.*

*Может использоваться на полях, конструкторах и сеттерах.*

`@Service` - *маркировка класса, как компонента Spring. Бизнес-логика*

`@GetMapping` - *упрощённая версия @RequestMapping для конкретного HTTP-метода.*


---


<a name="пример-16"></a>
**`@Service`, `@Repository`, `@Component`**  
```java
@Service
public class MyService {}

@Repository
public class MyRepository {}

@Component
public class MyComponent {}
```

*Маркировка класса, как компонента Spring.*

`@Component` — *общее обозначение компонента.*

`@Service` — *бизнес-логика.*

`@Repository` — *доступ к данным, также предоставляет специфичные исключения.*


---



<a name="пример-17"></a>
**`@Configuration`**  
```java
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

`@Configuration` - *класс содержит определения бинов.*

*Позволяет использовать аннотацию `@Bean` внутри класса.*

`Bean` - *регистрирует метод как бин в контексте Spring.*

*Может быть сканирован как часть контекста Spring.*


---


<a name="пример-18"></a>
**`@Bean`**  
```java
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

`@Configuration` - *класс содержит определения бинов.*

`Bean` - *регистрирует метод как бин в контексте Spring.*

*Возвращает объект, который становится частью Spring-контекста.*

*Имя бина по умолчанию — имя метода (myService).*


---


<a name="пример-19"></a>
**`@Value`**  
```java
@Component
public class MyComponent {
    @Value("${app.name}")
    private String appName;

    public String getAppName() {
        return appName;
    }
}
```

`@Value - *внедряет значения из `application.properties`.*

**app.name=MyAwesomeApp**

`@Component` — *это базовая аннотация Spring, которая помечает класс как "компонент", подлежащий автоматическому обнаружению и регистрации в контексте Spring. Классы с этой аннотацией становятся Spring-бинами и могут быть внедрены в другие компоненты через DI (Dependency Injection).*

---


<a name="пример-20"></a>
**`@Profile`**  
```java
@Component
@Profile("dev")
public class DevConfig {
    public String getConfig() {
        return "Development Mode";
    }
}
```

*Как активировать?.*

**spring.profiles.active=dev**

`@Component` — *это базовая аннотация Spring, которая помечает класс как "компонент", подлежащий автоматическому обнаружению и регистрации в контексте Spring. Классы с этой аннотацией становятся Spring-бинами и могут быть внедрены в другие компоненты через DI (Dependency Injection).*


---


<a name="пример-21"></a>
**`@Entity`**  
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

*Связывает класс с таблицей в БД.*

`@Id` - *поле `id` становится первичным ключом сущности.*

*По умолчанию имя таблицы совпадает с именем класса.*


---


<a name="пример-22"></a>
**`@Table`**  
```java
@Entity
@Table(name = "users_table")
public class User {
    @Id
    private Long id;
    private String name;
}
```

`@Table` - *Задаёт имя таблицы в БД.*

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Id` - *поле `id` становится первичным ключом сущности.*

*Указывает, что данные будут храниться в таблице users_table.*


---


<a name="пример-23"></a>
**`@Id`**  
```java
@Entity
@Table(name = "users_table")
public class User {
    @Id
    private Long id;
    private String name;
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Id` - *поле `id` становится первичным ключом сущности.*

*Обязательно для каждой сущности.*


---


<a name="пример-24"></a>
**`@GeneratedValue`**  
```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Id` - *поле `id` становится первичным ключом сущности.*

`@GeneratedValue` - *Стратегия генерации ID.*

**Стратегии:**

`IDENTITY` — *автоинкремент БД.*

`AUTO` — *выбирается автоматически.*

`SEQUENCE` — *последовательность.*

`TABLE` — *эмуляция через таблицу.*


---



<a name="пример-25"></a>
**`@Column`**  
```java
@Entity
public class User {
    @Id
    private Long id;

    @Column(name = "user_name", nullable = false, length = 100)
    private String name;
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Column` - *Настройка столбца базы данных.*

`@Id` - *поле `id` становится первичным ключом сущности.*

*name → столбец user_name.*

*Не может быть null.*

*Максимальная длина — 100 символов.*


---



<a name="пример-26"></a>
**`@OneToMany`, `@ManyToOne`, `@ManyToMany`, `@OneToOne`**  
```java
@Entity
public class User {
    @Id
    private Long id;

    @OneToMany(mappedBy = "user")
    private List<Order> orders;
}

@Entity
public class Order {
    @Id
    private Long id;

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Id` - *поле `id` становится первичным ключом сущности.*

`@OneToMany`, `@ManyToOne`, `@ManyToMany`, `@OneToOne` - *Связи между сущностями.*

`@JoinColumn` - *используется для связи между сущностями, указывает на внешний ключ (foreign key), связывающий две таблицы.*

**Типы связей:*

`@OneToOne` — *один к одному.*

`@OneToMany` — *один ко многим.*

`@ManyToOne` — *многие к одному.*

`@ManyToMany` — *многие ко многим.*


---


<a name="пример-27"></a>
**`@JoinColumn`**  
```java
@ManyToOne
@JoinColumn(name = "user_id")
private User user;
```

`@Column` - *Настройка столбца базы данных.*

`@ManyToOne` — *Связь между сущностями, многие к одному.*

`@JoinColumn` - *используется для связи между сущностями, указывает на внешний ключ (foreign key), связывающий две таблицы.*


---


<a name="пример-28"></a>
**`@Transient`**  
```java
@Entity
public class User {
    @Id
    private Long id;

    @Transient
    private String tempPassword;
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Id` - *поле `id` становится первичным ключом сущности.*

`@Transient` - *позволяет добавить поле, которое не сохраняется в базу данных. Полезно для временных данных, вычисляемых значений или кэша.*

📌 **Примечание:**

*Это не то же самое, что ключевое слово `transient` в Java (хотя эффект похож).*
`@Transient` *переопределяет поведение JPA, даже если поле не помечено как `transient`.*


---


<a name="пример-29"></a>
**`@Enumerated`**  
```java
@Entity
public class User {
    @Id
    private Long id;

    @Enumerated(EnumType.STRING)
    private Role role;
}

public enum Role {
    USER, ADMIN
}
```

`@Entity` - *указывает, что класс является JPA-сущностью.*

`@Id` - *поле `id` становится первичным ключом сущности.*

`@Enumerated` - *сохраняет значение enum в БД либо как строку, либо как индекс (EnumType.ORDINAL по умолчанию).*

`EnumType.STRING` — *если данные важны и должны быть читаемыми (например, в SQL-запросах).*

`EnumType.ORDINAL` — *если важна экономия места и стабильность порядка.*

*Изменение порядка элементов в enum может сломать данные, если используется `EnumType.ORDINAL`.*


---


<a name="пример-30"></a>
**`@CreationTimestamp`, `@UpdateTimestamp`**  
```java
@Entity
public class User {
    @Id
    private Long id;

    @CreationTimestamp
    private LocalDateTime createdAt;

    @UpdateTimestamp
    private LocalDateTime updatedAt;
}
```

`@Id` - *поле `id` становится первичным ключом сущности.*

`@CreationTimestamp` — *автоматически устанавливает дату при создании сущности.*

`@UpdateTimestamp` — *автоматически обновляется при каждом изменении сущности.*

*Эти аннотации предоставляются Hibernate (не входят в стандарт JPA), поэтому нужно подключить Hibernate-зависимость.*

💡 **Аналог в SQL:**

```java
CREATE TABLE user (
    id BIGINT PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```


---