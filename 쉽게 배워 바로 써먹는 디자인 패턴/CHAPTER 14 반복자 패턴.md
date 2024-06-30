# 반복자 패턴(Iterator Pattern)
- 내부 구조를 노출하지 않고 집합체를 통해 원소 객체에 순차적으로 접근하는 방법 제공
- 객체를 하나의 데이터 요소로 처리

## 장점
- 내부 구조를 노출하지 않고 원소 객체에 접근 가능
- 다양한 집합체에 대해 일관된 방식으로 접근 가능
- 반복자를 통해 순차적으로 접근하므로 원소의 순서를 보장

## 단점
- 추가적인 반복자 클래스를 구현해야 함
- 집합체의 구조가 변경되면 반복자 클래스도 수정해야 함

## 예제: 자바에서 반복자 패턴 사용하기

```java
import java.util.Iterator;

// 원소 객체를 나타내는 클래스
class Element {
    private String name;

    public Element(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

// 집합체를 나타내는 클래스
class Collection implements Iterable<Element> {
    private Element[] elements;
    private int size;

    public Collection(int capacity) {
        elements = new Element[capacity];
        size = 0;
    }

    public void addElement(Element element) {
        if (size < elements.length) {
            elements[size++] = element;
        }
    }

    @Override
    public Iterator<Element> iterator() {
        return new CollectionIterator();
    }

    // 반복자 클래스
    private class CollectionIterator implements Iterator<Element> {
        private int index;

        public CollectionIterator() {
            index = 0;
        }

        @Override
        public boolean hasNext() {
            return index < size;
        }

        @Override
        public Element next() {
            return elements[index++];
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Collection collection = new Collection(3);
        collection.addElement(new Element("Element 1"));
        collection.addElement(new Element("Element 2"));
        collection.addElement(new Element("Element 3"));

        // 반복자를 통해 원소에 접근
        Iterator<Element> iterator = collection.iterator();
        while (iterator.hasNext()) {
            Element element = iterator.next();
            System.out.println(element.getName());
        }
    }
}
```

위의 예제는 자바에서 반복자 패턴을 사용하는 간단한 예시입니다. `Element` 클래스는 원소 객체를 나타내며, `Collection` 클래스는 집합체를 나타냅니다. `Collection` 클래스는 `Iterable` 인터페이스를 구현하여 반복자를 반환하도록 합니다. 반복자는 `CollectionIterator` 클래스로 구현되며, `hasNext()`와 `next()` 메서드를 통해 순차적으로 원소에 접근할 수 있습니다. `Main` 클래스에서는 `Collection` 객체를 생성하고 원소를 추가한 뒤, 반복자를 통해 원소에 접근하여 출력합니다.