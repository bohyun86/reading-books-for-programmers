# 싱글턴 패턴(Singleton Pattern)

### 싱글턴 패턴이 사용되는 상황
- 공유 자원 접근
- 복수의 시스템이 하나의 자원에 접근할 때
- 유일한 객체가 필요할 때
- 값의 캐시가 필요할 때

클래스 내에서 하나의 객체만 사용할 경우 싱글턴 패턴 사용
프레임워크에서는 싱글턴 패턴을 다양한 곳에서 폭넓게 사용

## 싱글턴 패턴 예제
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // private constructor to prevent instantiation
    }

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