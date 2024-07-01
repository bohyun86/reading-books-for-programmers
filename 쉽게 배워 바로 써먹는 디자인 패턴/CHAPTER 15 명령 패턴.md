# 명령 패턴(Command Pattern)

- 행동의 호출을 객체로 캡슐화하여 실행
- 동작 자체를 다른 객체에 전달(행동을 객체로 캡슐화)
- 작업의 객체화: 동작의 행위와 행위를 실행하는 호출 메서드를 함께 만듦
- 객체의 동작 행위와 이를 실행하는 호출 부분을 분리
- 콜백 처리와 비슷
- 복구, 저장 등의 기능에 활용

## 구성 요소

- 인터페이스: 멸령을 실행할 메서드 가짐
- 명령: 명령 패턴이 객체를 실행하는 유일한 메서드
- 리시버: 명령을 수신하고 실제 동작을 수행하는 객체
- 인보커: 생성된 명령 객체를 저장하고 관리하는 역할

## 장점

- 실행되는 동작을 캡슐화하여 유연성을 제공합니다.
- 실행되는 동작을 다른 객체에게 전달할 수 있습니다.
- 명령을 취소하거나 다시 실행할 수 있는 기능을 제공합니다.
- 작업의 객체화를 통해 코드의 가독성과 유지보수성을 향상시킵니다.

## 단점

- 많은 클래스와 인터페이스를 도입하여 복잡성을 증가시킬 수 있습니다.
- 실행되는 동작을 캡슐화하기 위해 추가적인 객체 생성이 필요합니다.
- 실행되는 동작을 캡슐화하기 위해 메모리 사용량을 증가시킬 수 있습니다.

## 명령 패턴 예제

```java
// 인터페이스: 명령을 실행할 메서드를 가짐
interface Command {
    void execute();
}

// 명령: 명령 패턴이 객체를 실행하는 유일한 메서드를 구현
class ConcreteCommand implements Command {
    private Receiver receiver;

    ConcreteCommand(Receiver receiver) {
        this.receiver = receiver;
    }

    public void execute() {
        receiver.action();
    }
}

// 리시버: 명령을 수신하고 실제 동작을 수행하는 객체
class Receiver {
    public void action() {
        System.out.println("명령을 수행합니다.");
    }
}

// 인보커: 생성된 명령 객체를 저장하고 관리하는 역할
class Invoker {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void executeCommand() {
        command.execute();
    }
}

// 클라이언트 코드
public class Client {
    public static void main(String[] args) {
        // 리시버 객체 생성
        Receiver receiver = new Receiver();

        // 명령 객체 생성 및 리시버 객체 전달
        Command command = new ConcreteCommand(receiver);

        // 인보커 객체 생성 및 명령 객체 설정
        Invoker invoker = new Invoker();
        invoker.setCommand(command);

        // 명령 실행
        invoker.executeCommand();
    }
}
```

위의 예제는 명령 패턴을 구현한 간단한 자바 코드입니다. 인터페이스를 통해 명령을 실행하는 메서드를 정의하고, 명령 객체는 실제 동작을 수행하는 리시버 객체와 연결됩니다. 인보커 객체는 생성된 명령 객체를 저장하고 실행하는 역할을 합니다. 클라이언트 코드에서는 리시버 객체와 명령 객체를 생성하고, 인보커 객체에 명령 객체를 설정하여 실행합니다.

이 예제를 통해 명령 패턴의 구조와 사용 방법을 이해할 수 있습니다.


