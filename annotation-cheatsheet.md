# 📚 Lombok, Spring Boot & Jakarta Annotations Guide

Краткий справочник по самым полезным аннотациям с примерами и объяснениями.  
*Для Java-разработчиков, кто устал гуглить одно и то же*.

---

## 🛠️ **Lombok Annotations**

### **Генерация кода**
| Аннотация          | Описание                                                                 | Пример |
|--------------------|-------------------------------------------------------------------------|--------|
| `@Getter`/`@Setter` | Автоматические геттеры/сеттеры                                          | [Пример](#пример-1) |
| `@Builder`         | Реализация паттерна Builder для удобного создания объектов               | [Пример](#пример-2) |
| `@Data`            | Всё в одном: `@ToString`, `@EqualsAndHashCode`, `@Getter`/`@Setter`     | [Пример](#пример-3) |

#### **Примеры**
<a name="пример-1"></a>
**1. Простой POJO с Lombok**  
```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private Long id;
    private String name;
}
```

<a name="пример-2"></a>
**2. Паттерн Builder**  
```java
@Builder
public class Product {
    private String name;
    @Builder.Default 
    private int quantity = 1;
}

// Использование:
Product.builder().name("Laptop").build();
```

<a name="пример-3"></a>
**3. Комплексная модель**  
```java
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Employee {
    @Id 
    private UUID id;
    private String name;
}
```

---

## 🌱 **Spring Boot Annotations**

### **Веб-слои**
| Аннотация          | Описание                                                                 | Пример |
|--------------------|-------------------------------------------------------------------------|--------|
| `@RestController` | REST-контроллер (включает `@ResponseBody`)                              | [Пример](#пример-4) |
| `@RequestBody`    | Принимает JSON в параметрах метода                                      | [Пример](#пример-5) |
| `@Valid`          | Включает валидацию для DTO                                              | [Пример](#пример-6) |

#### **Примеры**
<a name="пример-4"></a>
**4. REST-контроллер**  
```java
@RestController
@RequestMapping("/api/users")
@RequiredArgsConstructor
public class UserController {
    private final UserService service;

    @GetMapping("/{id}")
    public User getById(@PathVariable Long id) {
        return service.findById(id);
    }
}
```

<a name="пример-5"></a>
**5. Прием JSON**  
```java
@PostMapping
public User create(@RequestBody @Valid UserDto dto) {
    return service.create(dto);
}
```

---

## 🗃️ **Jakarta (JPA) Annotations**

### **Сущности БД**
| Аннотация          | Описание                                                                 | Пример |
|--------------------|-------------------------------------------------------------------------|--------|
| `@Entity`         | Помечает класс как сущность БД                                          | [Пример](#пример-7) |
| `@OneToMany`      | Связь "один ко многим"                                                  | [Пример](#пример-8) |
| `@Transactional`  | Управление транзакциями                                                 | [Пример](#пример-9) |

#### **Примеры**
<a name="пример-7"></a>
**7. Базовая сущность**  
```java
@Entity
@Table(name = "orders")
@Data
public class Order {
    @Id 
    @GeneratedValue
    private UUID id;
}
```

<a name="пример-8"></a>
**8. Связи между таблицами**  
```java
@OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
private List<OrderItem> items;
```
