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

<a name="пример-2"></a>
**2. Паттерн Builder с @Builder**  
```java
@Builder
@ToString
public class Product {
    private String name;
    private double price;
    @Builder.Default 
    private int quantity = 1;
}

// Использование:
Product laptop = Product.builder()
    .name("MacBook Pro")
    .price(1999.99)
    .build();