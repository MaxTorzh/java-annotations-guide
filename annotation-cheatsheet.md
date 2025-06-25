# 📚 Lombok, Spring Boot & Jakarta Annotations Guide

Краткий справочник по самым полезным аннотациям с примерами и объяснениями.  
*Для Java-разработчиков, кто устал гуглить одно и то же*.

---

## 🛠️ **Lombok Annotations**

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

#### **Примеры**
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


**Сгенерированные методы:**
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


**Сгенерированный код**
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


**Сгенерированный код**
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


**Сгенерированный код**
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


---


<a name="пример-5"></a>
**`@NoArgsConstructor`**  
```java
@NoArgsConstructor
public class User {
    private String name;
}
```

**Генерируется:**
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

**Генерируется:**
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
**` @RequiredArgsConstructor`**  
```java
@RequiredArgsConstructor
public class User {
    private final String name;
    private int age;
}
```

**Генерируется:**
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
**` @Value`**  
```java
@Value
public class User {
    String name;
    int age;
}
```


**Сгенерированный код**
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

**Генерируется:**
```java
public User(String name) {
    this.name = name;
}
```

*Создаёт неизменяемый (immutable) класс: все поля автоматически становятся private final, сеттеры не создаются, а также генерируются:*

*`toString()`*

*`equals()` / `hashCode()`*

*`getter (в виде getXxx())`*

*`requiredArgsConstructor()` для всех final полей*

*Можно ли использовать на уровне поля?* - **✅ Да.** 

*Можно ли использовать на уровне класса?* - **❌ Нет.** 

*Можно ли использовать на уровне конструктора?* - **❌ Нет.**