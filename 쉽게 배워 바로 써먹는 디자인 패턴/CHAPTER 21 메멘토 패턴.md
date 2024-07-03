# 메멘토 패턴(Memento Pattern)

- 객체의 스냅숏(특정 시점의 객체 상태)을 생성하고 저장
- undo 형태로 읽어오면 객체 상태 복원

***인터페이스***

- 원조본(Originator): 광범위한 메멘토의 접근을 모두 허용
- 케어테이커(Caretaker): 제한된 범위 안에서 허용

***Memento 클래스***

- 정보를 저장하는 프로퍼티(protected)와 저장된 객체에 접근하기 위한 메서드로 구성

***Originator 클래스***

- 실체 객체와 메멘토 사이의 중간 매개체 역할 수행

***CareTaker 클래스***

- 다수의 메멘토를 보관하고 관리(저장하고 읽어오는 역할)
- 스택 구조를 이용해 구현

## 메멘토 패턴 예제

```java
// 예제 코드

// Memento 클래스
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// Originator 클래스
class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
    }
}

// CareTaker 클래스
class CareTaker {
    private Stack<Memento> mementoStack = new Stack<>();

    public void addMemento(Memento memento) {
        mementoStack.push(memento);
    }

    public Memento getMemento() {
        return mementoStack.pop();
    }
}

// 예제 사용
public class Main {
    public static void main(String[] args) {
        Originator originator = new Originator();
        CareTaker careTaker = new CareTaker();

        originator.setState("State 1");
        careTaker.addMemento(originator.saveStateToMemento());

        originator.setState("State 2");
        careTaker.addMemento(originator.saveStateToMemento());

        originator.setState("State 3");
        careTaker.addMemento(originator.saveStateToMemento());

        Memento memento = careTaker.getMemento();
        originator.getStateFromMemento(memento);
        System.out.println("Current State: " + originator.getState());

        memento = careTaker.getMemento();
        originator.getStateFromMemento(memento);
        System.out.println("Current State: " + originator.getState());

        memento = careTaker.getMemento();
        originator.getStateFromMemento(memento);
        System.out.println("Current State: " + originator.getState());
    }
}
```
