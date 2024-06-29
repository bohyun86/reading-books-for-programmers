# 플라이웨이트 패턴(Flyweight Pattern)
- 객체를 공유하기 위해 구조를 변경
- 객체를 공유하면 객체를 재사용할 수 있어 시스템 자원 절약
- 팩토리 패턴 -> 객체 생성 분리, 싱글턴 패턴 -> 중복생성 방지
- 객체를 생성, 호출하기 전 중복검사로 객체를 관리


## 상태구분
### 본질적 상태
- 객체의 상태값에 따라 달라지지 않고 동일하게 적용되는 것
- 어떤 변경도 없이 객체를 있는 그대로 참조해서 사용
- shared

### 부가적 상태
- 객체를 공유할 때 상태값에 따라 달라지는 것
- 부가적 상태로 객체를 사용하는 경우 객체의 특정 데이터값을 변경해 참조하는 객체에 영향을 주기 위해
- 플라이웨이트 패턴으로 공유할 수 없음(사이드 이펙트 발생)

### 독립 객체
- 공유 객체와 반대되는 의미
- 공유되지 않고 각각의 상황에 맞게 생성된 객체

## 플라이웨이트 패턴 예제

```java
import java.util.HashMap;
import java.util.Map;

// 플라이웨이트 인터페이스
interface Shape {
    void draw();
}

// 구체적인 플라이웨이트 클래스
class Circle implements Shape {
    private String color;
    private int x;
    private int y;
    private int radius;

    public Circle(String color) {
        this.color = color;
    }

    public void setX(int x) {
        this.x = x;
    }

    public void setY(int y) {
        this.y = y;
    }

    public void setRadius(int radius) {
        this.radius = radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing Circle: Color - " + color + ", x - " + x + ", y - " + y + ", radius - " + radius);
    }
}

// 플라이웨이트 팩토리 클래스
class ShapeFactory {
    private static final Map<String, Shape> circleMap = new HashMap<>();

    public static Shape getCircle(String color) {
        Circle circle = (Circle) circleMap.get(color);

        if (circle == null) {
            circle = new Circle(color);
            circleMap.put(color, circle);
            System.out.println("Creating new circle: Color - " + color);
        }

        return circle;
    }
}

// 클라이언트 코드
public class Main {
    private static final String[] colors = { "Red", "Green", "Blue", "Yellow", "Black" };

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            Circle circle = (Circle) ShapeFactory.getCircle(getRandomColor());
            circle.setX(getRandomX());
            circle.setY(getRandomY());
            circle.setRadius(100);
            circle.draw();
        }
    }

    private static String getRandomColor() {
        return colors[(int) (Math.random() * colors.length)];
    }

    private static int getRandomX() {
        return (int) (Math.random() * 100);
    }

    private static int getRandomY() {
        return (int) (Math.random() * 100);
    }
}
```

이 예제는 자바 언어를 사용하여 플라이웨이트 패턴을 구현한 것입니다. `Shape` 인터페이스는 플라이웨이트의 공통 동작을 정의하고, `Circle` 클래스는 구체적인 플라이웨이트 객체를 나타냅니다. `ShapeFactory` 클래스는 플라이웨이트 객체를 생성하고 관리하는 팩토리 역할을 합니다. 클라이언트 코드에서는 `ShapeFactory`를 통해 플라이웨이트 객체를 얻어와 사용합니다.

이 예제를 실행하면, 서로 다른 색상의 원이 무작위로 생성되어 그려지는 것을 확인할 수 있습니다.








