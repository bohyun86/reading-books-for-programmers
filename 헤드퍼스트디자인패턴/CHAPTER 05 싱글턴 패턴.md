# 싱글턴 패턴(Singleton Pattern)

- ex) 스레드 풀, 캐시, 대화상자, 레지스트리 설정, 로거 등
- 클래스 인스턴스를 하나만 만들고, 그 인스턴스로의 전역 접근을 제공
- 생성자가 여러 차례 호출되더라도 실제로는 하나의 인스턴스만 생성되고, 그 인스턴스에 접근할 수 있는 전역 포인트를 제공

## 동기화된 싱글턴 패턴(Synchronized Singleton Pattern)

- 멀티스레드 환경에서 동기화된 싱글턴 패턴을 사용하면, 인스턴스가 여러 개 생성되는 것을 방지할 수 있다.
- 하지만, 동기화된 싱글턴 패턴은 성능 저하를 일으킬 수 있다.
- voletile 키워드를 사용하면, 인스턴스가 메모리에 캐시되는 것을 방지할 수 있다.
- 또한, DCL(Double-Checked Locking)을 사용하면, 동기화된 싱글턴 패턴의 성능을 향상시킬 수 있다.
- DCL은 인스턴스가 생성되어 있는지 확인한 후, 생성되어 있지 않다면 동기화 블록에 진입하여 인스턴스를 생성하는 방식이다.

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

## enum 싱글턴 패턴(Enum Singleton Pattern)

- enum 싱글턴 패턴은 가장 간단하고 안전한 싱글턴 패턴이다.
- enum은 JVM에 의해 싱글턴이 보장된다.
- enum은 직렬화나 리플렉션 공격에 안전하다.

```java
public enum Singleton {
    INSTANCE;
}

public class Main {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.INSTANCE;
        Singleton singleton2 = Singleton.INSTANCE;

        System.out.println(singleton1 == singleton2);
    }
}
```
