# 중재자 패턴(Mediator Pattern)

- 분산된 객체의 행동을 중재
- 객체 간 복잡한 상호 관계를 중재하며 객체 간에 복잡한 관계로 묶인 것을 재구성
- 서로 의존적인 M:N의 관계를 가진 객체를 느슨한 1:1 관계로 변경
- 하나의 중재자와 여러 동료 객체로 구성, 동료 객체의 강력한 결합 구조를 느슨한 결합 구조로 개선
- 중개하는 행동마다 concreteMediator 클래스 생성(하나의 mediate() 메서드 구현) (인터페이스 활용)
- 동료 객체는 하나의 setMediator() 메서드를 필수로 선언(추상클래스 활용)
- 동료 객체는 처리요청 메서드, 처리 부여받는 메서드
- 양방향 통신 가능

## 중재자 패턴 예제

```java
// Mediator interface
interface Mediator {
    void mediate(String message, Colleague colleague);
}

// Concrete mediator class
class ConcreteMediator implements Mediator {
    private Colleague colleague1;
    private Colleague colleague2;

    public void setColleague1(Colleague colleague1) {
        this.colleague1 = colleague1;
    }

    public void setColleague2(Colleague colleague2) {
        this.colleague2 = colleague2;
    }

    @Override
    public void mediate(String message, Colleague colleague) {
        if (colleague == colleague1) {
            colleague2.receive(message);
        } else if (colleague == colleague2) {
            colleague1.receive(message);
        }
    }
}

// Colleague abstract class
abstract class Colleague {
    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }

    public abstract void send(String message);

    public abstract void receive(String message);
}

// Concrete colleague class
class ConcreteColleague1 extends Colleague {
    public ConcreteColleague1(Mediator mediator) {
        super(mediator);
    }

    @Override
    public void send(String message) {
        mediator.mediate(message, this);
    }

    @Override
    public void receive(String message) {
        System.out.println("ConcreteColleague1 received: " + message);
    }
}

// Concrete colleague class
class ConcreteColleague2 extends Colleague {
    public ConcreteColleague2(Mediator mediator) {
        super(mediator);
    }

    @Override
    public void send(String message) {
        mediator.mediate(message, this);
    }

    @Override
    public void receive(String message) {
        System.out.println("ConcreteColleague2 received: " + message);
    }
}

// Usage example
public class MediatorPatternExample {
    public static void main(String[] args) {
        ConcreteMediator mediator = new ConcreteMediator();

        ConcreteColleague1 colleague1 = new ConcreteColleague1(mediator);
        ConcreteColleague2 colleague2 = new ConcreteColleague2(mediator);

        mediator.setColleague1(colleague1);
        mediator.setColleague2(colleague2);

        colleague1.send("Hello from colleague1!");
        colleague2.send("Hi from colleague2!");
    }
}
```








