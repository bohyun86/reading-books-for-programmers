# 복합체 패턴(Composite Pattern)
- 객체가 또 다른 객체를 포함하는 것
- 객체들은 트리 구조형태의 계층화 구조를 가짐
- 복합체 패턴은 객체들을 트리 구조로 구성하여 부분-전체 계층을 표현
- 수평으로 확장하는 것은 하나의 객체가 여러 객체를 포함 하는 것

## 재귀적 결합
- 재귀적 결합을 통해 하나의 객체가 다수의 연결 객체를 가질 수 있으며 복합체가 객체를 포함할 때는 단일 객체, 
복합객체를 가리지 않습니다.

## 장단점 및 결과
- 장점
    - 객체들을 트리 구조로 구성하여 부분-전체 계층을 표현
    - 클라이언트 코드에서 객체들을 일관되게 다룰 수 있음
    - 새로운 종류의 객체를 쉽게 추가할 수 있음
    - 객체들을 자유롭게 조합하여 복합 객체를 만들 수 있음
- 단점
    - 설계가 복잡해질 수 있음
    - 클라이언트 코드가 객체들의 구조를 알아야 함
    - 객체들이 동일한 인터페이스를 사용하지 않을 경우 복합체 패턴을 사용할 수 없음

```
// Graphic.java
interface Graphic {
    void print();
}

// Ellipse.java
class Ellipse implements Graphic {

    @Override
    public void print() {
        System.out.println("Ellipse");
    }
}

// CompositeGraphic.java
import java.util.ArrayList;
import java.util.List;

class CompositeGraphic implements Graphic {

    // Collection of child graphics.
    private List<Graphic> childGraphics = new ArrayList<>();

    // Adds the graphic to the composition.
    public void add(Graphic graphic) {
        childGraphics.add(graphic);
    }

    // Removes the graphic from the composition.
    public void remove(Graphic graphic) {
        childGraphics.remove(graphic);
    }

    // Prints the graphic.
    @Override
    public void print() {
        for (Graphic graphic : childGraphics) {
            graphic.print();
        }
    }
}

// CompositeDemo.java
public class CompositeDemo {

    public static void main(String[] args) {
        // Initialize four ellipses
        Ellipse ellipse1 = new Ellipse();
        Ellipse ellipse2 = new Ellipse();
        Ellipse ellipse3 = new Ellipse();
        Ellipse ellipse4 = new Ellipse();

        // Initialize three composite graphics
        CompositeGraphic graphic = new CompositeGraphic();
        CompositeGraphic graphic1 = new CompositeGraphic();
        CompositeGraphic graphic2 = new CompositeGraphic();

        // Composes the graphics
        graphic1.add(ellipse1);
        graphic1.add(ellipse2);
        graphic1.add(ellipse3);

        graphic2.add(ellipse4);

        graphic.add(graphic1);
        graphic.add(graphic2);

        // Prints the complete graphic (four times the string "Ellipse").
        graphic.print();
    }
}


```