- A Java class that:
    - has a public no-argument constructor.
    - has private properties accessed through public getter and setter methods.
    - should be serializable (implements `java.io.Serializable`).

```java
import java.io.Serializable;

public class PersonBean implements Serializable {
    private String name;
    private int age;

    public PersonBean() {
        // No-argument constructor
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
