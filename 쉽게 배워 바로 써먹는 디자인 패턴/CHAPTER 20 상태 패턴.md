# 상태 패턴(Status Pattern)

- 상태값에 따른 동작을 각각의 함수 형태로 구별하는 것과 달리 객체로 동작을 분리
- 1개의 객체는 1개의 상태만 구현
- 싱글턴 패턴을 사용해서 중복된 상태 객체 생성되는 것 방지 가능
- 상태 패턴은 조건 분기 없이 상태값을 이용해 객체의 동작을 처리 (제어문은 코드를 실행하는 데 더 많은 부하를 발생시키고, 가독성 떨어뜨림)

## 관련용어
- 국지화: 국지화시 해당 객체에만 영향을 미침

  : 상태에 따른 코드를 보다 쉽게 이해하고 수정할 수 있음

- 상태 전이: 상태값이 동작에 따라 변하는것

## 상태 패턴 예제

```java
// 1. State 인터페이스
public interface State {
    void handle(Context context);
}

// 2. ConcreteStateA 클래스
public class StateA implements State {
    private static final StateA INSTANCE = new StateA();

    private StateA() {}

    public static StateA getInstance() {
        return INSTANCE;
    }

    @Override
    public void handle(Context context) {
        System.out.println("Handling request in State A.");
        context.setState(StateB.getInstance());
    }
}

// 3. ConcreteStateB 클래스
public class StateB implements State {
    private static final StateB INSTANCE = new StateB();

    private StateB() {}

    public static StateB getInstance() {
        return INSTANCE;
    }

    @Override
    public void handle(Context context) {
        System.out.println("Handling request in State B.");
        context.setState(StateA.getInstance());
    }
}

// 4. Context 클래스
public class Context {
    private State state;

    public Context() {
        state = StateA.getInstance(); // 초기 상태 설정
    }

    public void setState(State state) {
        this.state = state;
    }

    public void request() {
        state.handle(this);
    }
}

// 5. Main 클래스
public class Main {
    public static void main(String[] args) {
        Context context = new Context();
        
        // 현재 상태에서 요청 처리
        context.request(); // State A에서 State B로 전이
        context.request(); // State B에서 State A로 전이
        context.request(); // State A에서 State B로 전이
    }
}
```
Context 클래스는 현재 상태를 관리합니다. 초기 상태는 StateA로 설정됩니다.
StateA와 StateB는 각각 자신의 상태에서 처리할 동작을 정의하고, 상태 전이를 수행합니다.
Main 클래스에서는 Context 객체를 생성하고 request 메서드를 호출하여 상태에 따른 동작을 수행합니다.
이 예제에서는 상태 전이를 단순히 StateA와 StateB 사이에서 전환하는 것으로 설정했습니다. 실제 애플리케이션에서는 더 복잡한 상태와 전이가 있을 수 있습니다. 상태 패턴을 사용하면 코드의 가독성과 유지 보수성이 크게 향상됩니다.