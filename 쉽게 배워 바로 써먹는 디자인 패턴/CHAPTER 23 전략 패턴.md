# 전략 패턴(Stratege Pattern)

- 객체 내부에서 해결해야 하는 목적을 알고리즘 객체로 분리 적용하는 기법
- 전략: 알고리즘(주어진 문제를 해결하는 방법)
- 전술: 알고리즘이 동작하는 상세 내용
- 템플릿 메서드처럼 알고리즘의 일부만 변경 하는 것이 아니라 행위 전체를 변경

### 분리

- 외부 변화에 보다 쉽게 적응하려면 변화가 예상되는 부분을 분리 하는 것이 좋음
- 대부분 처리 로직 부분의 변화가 예상되므로, 처리 로직을 분리하는 것이 중요

### 템플릿 메서드

- 공통된 기능을 분리하여 템플릿화하고, 추상화를 통해 상황별로 다르게 처리할 수 있도록 실제 동작을 분리

### 캡슐화

- 분리된 알고리즘은 별도의 클래스로 캡슐화 = 전략
- 상황에 맞게 교체하면서 사용

## 전략 패턴 예제

```java
// 전략 인터페이스
interface Strategy {
    void execute();
}

// 전략 구현 클래스 1
class ConcreteStrategy1 implements Strategy {
    @Override
    public void execute() {
        System.out.println("Executing strategy 1");
    }
}

// 전략 구현 클래스 2
class ConcreteStrategy2 implements Strategy {
    @Override
    public void execute() {
        System.out.println("Executing strategy 2");
    }
}

// 컨텍스트 클래스
class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public void executeStrategy() {
        strategy.execute();
    }
}

// 사용 예제
public class StrategyPatternExample {
    public static void main(String[] args) {
        // 전략 객체 생성
        Strategy strategy1 = new ConcreteStrategy1();
        Strategy strategy2 = new ConcreteStrategy2();

        // 컨텍스트 객체 생성 및 전략 설정
        Context context = new Context(strategy1);

        // 전략 실행
        context.executeStrategy();

        // 전략 변경
        context = new Context(strategy2);

        // 전략 실행
        context.executeStrategy();
    }
}
```


