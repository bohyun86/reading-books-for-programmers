# 체인 패턴(Chain Pattern)

- 객체 메시지의 송신과 수신을 분리해서 처리
- 하나의 상태값에 복수의 동작 객체를 처리할 수 있도록 하나의 사슬 형태로 묶어서 처리
- 체인 패턴으로 연결된 객체는 상태값을 스스로 판별하여 자신의 행동을 실행
- 순차적으로 탐색하면서 요청된 객체를 수행하기 때문에 다소 지연 시간 발생
- 하나의 객체를 처리할 때 클래스 객체 한 개의 메서드에서 책임을 지는 것이 아니라 여러 객체의 메서드에서 동시에 책임을 처리

## 체인 패턴 예제

```java
// 체인 패턴에서 사용될 추상 클래스
abstract class Handler {
    private Handler nextHandler;

    public void setNextHandler(Handler nextHandler) {
        this.nextHandler = nextHandler;
    }

    public void handleRequest(Request request) {
        if (canHandle(request)) {
            processRequest(request);
        } else if (nextHandler != null) {
            nextHandler.handleRequest(request);
        } else {
            System.out.println("No handler found for the request.");
        }
    }

    protected abstract boolean canHandle(Request request);

    protected abstract void processRequest(Request request);
}

// 실제 처리를 담당하는 클래스
class ConcreteHandlerA extends Handler {
    @Override
    protected boolean canHandle(Request request) {
        // A 클래스가 처리할 수 있는 조건을 확인
        return request.getType().equals("A");
    }

    @Override
    protected void processRequest(Request request) {
        // A 클래스에서 실제 처리하는 로직 구현
        System.out.println("Request handled by ConcreteHandlerA");
    }
}

class ConcreteHandlerB extends Handler {
    @Override
    protected boolean canHandle(Request request) {
        // B 클래스가 처리할 수 있는 조건을 확인
        return request.getType().equals("B");
    }

    @Override
    protected void processRequest(Request request) {
        // B 클래스에서 실제 처리하는 로직 구현
        System.out.println("Request handled by ConcreteHandlerB");
    }
}

// 요청 객체
class Request {
    private String type;

    public Request(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}

// 클라이언트 코드
public class ChainPatternExample {
    public static void main(String[] args) {
        // 체인 구성
        Handler handlerA = new ConcreteHandlerA();
        Handler handlerB = new ConcreteHandlerB();
        handlerA.setNextHandler(handlerB);

        // 요청 생성
        Request requestA = new Request("A");
        Request requestB = new Request("B");
        Request requestC = new Request("C");

        // 요청 처리
        handlerA.handleRequest(requestA); // ConcreteHandlerA에서 처리
        handlerA.handleRequest(requestB); // ConcreteHandlerB에서 처리
        handlerA.handleRequest(requestC); // No handler found for the request.
    }
}
```
