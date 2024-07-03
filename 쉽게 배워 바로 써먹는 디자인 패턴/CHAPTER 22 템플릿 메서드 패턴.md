# 템플릿 메서드 패턴(Template Method Pattern)

- 메서드를 이용해 각 단계를 템플릿 구조화하고 행동을 구분
- 구조 변경 않고, 러리 로직의 일부를 재정의
- 상위 클래스에서 처리의 뼈대를 구현하고 하위 클래스에서 세부적인 내용을 구현

## 템플릿 메서드 패턴의 장점:
- 코드 중복을 줄여줌: 공통된 로직을 상위 클래스에 구현하므로, 하위 클래스에서는 해당 로직을 반복해서 작성할 필요가 없음.
- 확장성과 유연성을 제공: 상위 클래스의 템플릿 메서드를 재정의하여 다양한 동작을 구현할 수 있으므로, 새로운 기능을 추가하거나 기존 기능을 변경하기 쉬움.
- 구조화된 디자인: 각 단계를 메서드로 구조화하여 코드의 가독성을 높여줌.

## 템플릿 메서드 패턴의 단점:
- 상위 클래스와 하위 클래스 간의 강한 의존성: 상위 클래스의 변경이 하위 클래스에 영향을 미칠 수 있으므로, 상위 클래스의 수정이 주의를 요구함.
- 유연성 제한: 템플릿 메서드의 구조가 고정되어 있기 때문에, 다른 구조를 가진 알고리즘을 적용하기 어려울 수 있음.

## 템플릿 메서드 예제

```java
public abstract class AbstractClass {
    public void templateMethod() {
        step1();
        step2();
        step3();
    }

    protected abstract void step1();

    protected abstract void step2();

    protected abstract void step3();
}

public class ConcreteClass extends AbstractClass {
    @Override
    protected void step1() {
        // Implementation for step 1
    }

    @Override
    protected void step2() {
        // Implementation for step 2
    }

    @Override
    protected void step3() {
        // Implementation for step 3
    }
}

public class Main {
    public static void main(String[] args) {
        AbstractClass abstractClass = new ConcreteClass();
        abstractClass.templateMethod();
    }
}
```
