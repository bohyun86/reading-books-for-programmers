# 감시자 패턴

- 수동적으로 상태값을 전달 받아 처리
- 자바에서는 observer 인터페이스와 observable 클래스 제공

## 구성
***클래스***

- 주체(subject)

  : 인터페이스 (add, delete, notify 메서드)

- 실제 주체(cocreteSubject)

  : 여러 감시자를 저장

- 감시자(observer)
- 실체 객체(concreateObserver)

***그룹***
- 통보를 위한 ***주체-실체***클래스

  : 객체의 등록, 삭제, 통보 담당

- 처리를 위한 ***감시자-실체*** 클래스

  : 통보를 수신 받아 처리

## 주요 용어

- 등록: 동작하는 모든 객체 주체에 등록, 언제든 등록, 제거 가능
- 독립적: 주체는 상태 변화 시 감시자에 변경된 상태만 전달
- 일대다 관계: 주체 다수의 감시자 객체 가짐
- 구독 관계: 통보는 단방향성을 가짐 (게시-구독 패턴)
- 복합 관계: 다수의 감시자 객체 가짐
- 브로드캐스팅: 모든 감시자에게 상태 변화 메시지 보냄, 불필요한 객체에도 메시지 전다
- 능동적 통보: 감시자 객체에서도 변화를 주체에 통보, 주체는 이 변화를 다른 감시자에게 보낼 수도 있음

## 감시자 패턴 예제

```java
// 주체 인터페이스
interface Subject {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// 실제 주체 클래스
class ConcreteSubject implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String state;

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(state);
        }
    }

    public void setState(String state) {
        this.state = state;
        notifyObservers();
    }
}

// 감시자 인터페이스
interface Observer {
    void update(String state);
}

// 실체 객체 클래스
class ConcreteObserver implements Observer {
    private String state;

    public void update(String state) {
        this.state = state;
        // 상태 변화에 대한 처리 로직 작성
    }
}

// 예제 사용
public class Example {
    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();
        ConcreteObserver observer1 = new ConcreteObserver();
        ConcreteObserver observer2 = new ConcreteObserver();

        subject.addObserver(observer1);
        subject.addObserver(observer2);

        subject.setState("New state");
    }
}
```




