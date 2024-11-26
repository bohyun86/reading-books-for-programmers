### 내용 정리
프로토타입 패턴은 신규 객체를 생성하지 않고 유사한 기존 객체를 복제합니다.
기존 객체를 복제하면 신규 객체를 생성하는 것보다 자원이 절약됩니다.
- new 키워드로 객체 생성시 CPU 사용이 필요, 시간 및 자원 소모
- 복잡한 객체 생성시 초기화 작업 반복 안해도 됨
- 단, 객체의 상태값을 변경할 수 있는 관련 메서드가 미리 만들어져 있어야 함

--- 

### 프로토타입 패턴 (Prototype Pattern)이란?
**프로토타입 패턴 (Prototype Pattern)**은 객체 생성 패턴 중 하나로, 이미 생성된 객체를 복제하여 새로운 객체를 만드는 방식입니다. 즉, 기존 객체를 복사(cloning)해서 새 객체를 생성하기 때문에 새로 객체를 생성하는 데 드는 비용(시간 또는 메모리)을 줄이고, 객체 생성의 복잡성을 간소화할 수 있습니다. 이 패턴은 특히 객체 생성에 많은 자원이 필요하거나 시간이 오래 걸리는 경우에 유용하게 사용됩니다.

프로토타입 패턴은 Java의 `Cloneable` 인터페이스와 `clone()` 메서드를 사용하여 구현할 수 있습니다. 이를 통해 기존의 객체를 새로 복제하여 동일한 상태를 가진 객체를 만드는 것이 가능합니다.

### 프로토타입 패턴의 장점
1. **객체 생성 비용 절감**: 객체의 생성 비용이 큰 경우 동일한 객체를 복제하는 방식으로 객체 생성 시간을 줄일 수 있습니다.
2. **유연성**: 객체를 다양한 상태로 복제하여 필요에 따라 상태를 조금씩 변경해 사용할 수 있습니다.
3. **복잡한 객체 생성 회피**: 복잡한 객체를 처음부터 만드는 대신 기존 객체를 복제하여 필요한 상태만 변경할 수 있습니다.

### 프로토타입 패턴을 사용한 자바 예제
자바에서는 `Cloneable` 인터페이스와 `clone()` 메서드를 사용하여 프로토타입 패턴을 쉽게 구현할 수 있습니다. 아래는 `Shape`라는 클래스를 상속받는 `Rectangle`과 `Circle` 클래스가 있고, 이들을 복제하여 새로운 객체를 만드는 예제입니다.

#### 1. `Shape` 추상 클래스 정의
우선, 복제 가능한 객체의 기본 클래스인 `Shape`를 정의합니다.

```java
abstract class Shape implements Cloneable {
    private String id;
    protected String type;

    abstract void draw();

    public String getType() {
        return type;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    // 프로토타입 복제 메서드
    @Override
    public Object clone() {
        Object clone = null;
        try {
            clone = super.clone();  // clone() 메서드를 호출하여 객체를 복제
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return clone;
    }
}
```

- **`clone()` 메서드**: `Cloneable` 인터페이스를 구현하고 `clone()` 메서드를 사용하여 복제를 지원합니다.
- **`draw()` 메서드**: 추상 메서드로, 각 구체적인 도형에서 구현됩니다.

#### 2. `Rectangle` 클래스 정의
`Shape` 클래스를 상속받아 구체적인 도형인 `Rectangle`을 정의합니다.

```java
class Rectangle extends Shape {
    public Rectangle() {
        type = "Rectangle";
    }

    @Override
    void draw() {
        System.out.println("Inside Rectangle::draw() method.");
    }
}
```

- **`type`**: `Rectangle`이라는 도형의 종류를 설정합니다.
- **`draw()`**: 구체적으로 `Rectangle`을 그리는 동작을 정의합니다.

#### 3. `Circle` 클래스 정의
`Shape` 클래스를 상속받아 구체적인 도형인 `Circle`을 정의합니다.

```java
class Circle extends Shape {
    public Circle() {
        type = "Circle";
    }

    @Override
    void draw() {
        System.out.println("Inside Circle::draw() method.");
    }
}
```

- **`type`**: `Circle`이라는 도형의 종류를 설정합니다.
- **`draw()`**: 구체적으로 `Circle`을 그리는 동작을 정의합니다.

#### 4. `ShapeCache` 클래스 정의
`ShapeCache`는 캐시에서 객체를 복제하는 역할을 합니다. 이미 생성된 객체를 캐시에 저장하고, 이를 필요할 때 복제하여 사용합니다.

```java
import java.util.Hashtable;

class ShapeCache {
    private static Hashtable<String, Shape> shapeMap  = new Hashtable<>();

    public static Shape getShape(String shapeId) {
        Shape cachedShape = shapeMap.get(shapeId);
        return (Shape) cachedShape.clone();
    }

    // 초기화 메서드로, 캐시에 기본 도형을 저장
    public static void loadCache() {
        Rectangle rectangle = new Rectangle();
        rectangle.setId("1");
        shapeMap.put(rectangle.getId(), rectangle);

        Circle circle = new Circle();
        circle.setId("2");
        shapeMap.put(circle.getId(), circle);
    }
}
```

- **`Hashtable<String, Shape> shapeMap`**: 각 도형을 `Hashtable`에 저장해 두고, 필요할 때 이 도형을 복제하여 사용합니다.
- **`loadCache()`**: `Rectangle`과 `Circle` 객체를 생성하여 캐시에 저장합니다.
- **`getShape()`**: `shapeId`에 해당하는 도형을 복제하여 반환합니다.

#### 5. `PrototypePatternDemo` 클래스
이제 `ShapeCache`를 통해 도형을 복제하고 사용하는 예제를 만들어 보겠습니다.

```java
public class PrototypePatternDemo {
    public static void main(String[] args) {
        ShapeCache.loadCache();  // 캐시를 로드하여 기본 객체들 저장

        // 도형 복제하기
        Shape clonedShape1 = ShapeCache.getShape("1");
        System.out.println("Shape : " + clonedShape1.getType());
        clonedShape1.draw();

        Shape clonedShape2 = ShapeCache.getShape("2");
        System.out.println("Shape : " + clonedShape2.getType());
        clonedShape2.draw();

        // 동일한 ID로 다시 복제
        Shape clonedShape3 = ShapeCache.getShape("1");
        System.out.println("Shape : " + clonedShape3.getType());
        clonedShape3.draw();
    }
}
```

### 실행 결과
```
Shape : Rectangle
Inside Rectangle::draw() method.
Shape : Circle
Inside Circle::draw() method.
Shape : Rectangle
Inside Rectangle::draw() method.
```

위 결과에서 볼 수 있듯이, 캐시에 저장된 도형 객체들을 복제하여 사용하고 있으며, 동일한 객체를 복제하더라도 서로 독립적인 객체로 동작합니다.

### 프로토타입 패턴의 장점과 단점
#### 장점
1. **객체 생성 비용 감소**: 객체를 복제함으로써 새로 객체를 만드는 데 드는 비용을 줄일 수 있습니다.
2. **복잡한 객체 생성 회피**: 복잡한 초기 설정이 필요한 객체를 복제하여 손쉽게 새로운 객체를 만들 수 있습니다.
3. **다양한 구성 가능**: 원본 객체의 상태를 변경함으로써 복제된 객체에 대해 다양한 구성을 손쉽게 적용할 수 있습니다.

#### 단점
1. **클론 메서드의 복잡성**: 객체의 필드가 많거나 깊은 복사가 필요한 경우 `clone()` 메서드의 구현이 복잡해질 수 있습니다.
2. **Cloneable 인터페이스의 제약**: 자바의 `Cloneable` 인터페이스와 `clone()` 메서드는 사용하기 까다롭고, 기본적으로 얕은 복사만을 수행하기 때문에 깊은 복사를 직접 구현해야 하는 경우가 있습니다.

### 언제 사용해야 하는가?
- **복잡한 객체 생성**이 자주 일어날 때, 객체 생성 비용을 줄이기 위해 사용합니다.
- **동일한 형태의 객체를 여러 개 생성해야 하는 경우**, 프로토타입을 복제하여 성능을 향상시킬 수 있습니다.
- **객체의 초기 설정이나 구성에 복잡한 절차가 필요한 경우**, 이미 설정된 객체를 복제하여 빠르게 객체를 생성할 수 있습니다.

프로토타입 패턴은 객체 생성의 복잡성과 비용을 줄이고, 기존 객체의 상태를 재사용할 수 있도록 하는 데 적합한 패턴입니다. 특히 자바에서는 `Cloneable` 인터페이스와 `clone()` 메서드를 활용하여 쉽게 구현할 수 있지만, 올바른 복제 방법(얕은 복사 또는 깊은 복사)을 고려하여 사용해야 합니다.