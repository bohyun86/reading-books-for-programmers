# 프록시 패턴(Proxy Pattern)
- `프록시` 패턴은 객체 접근을 제어하기 위해 중간 단계에 `대리자`를 위치
- 객체를 두개로 나눠 재구성
- 두 객체는 동일한 인터페이스 규격을 가짐
- 실체 객체를 호출하면 행위를 중간에 가로채서 다른 동작을 수행하는 객체로 변경
- 프록시와 실제 객체는 위임을 통해 연결됨

## 핸들러
- 투과적 특성을 이용하여 요청된 행위를 처리하는 동작
- 실체 객체 수정 발생시 프록시 객체도 변경 필요
- 번거러운 작업을 쉽게 하기 위해 핸들러를 프록시에 추가

## 동적 클래스
- 프록시와 실체 객체를 구별하지 않고 접근하는 객체의 인스턴스 만들기 위해 팩토리 패턴을 같이 사용

## 프록시 패턴 예제
```java
// 실체 객체의 인터페이스
public interface Image {
    void display();
}

// 실체 객체
public class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading image: " + filename);
    }

    public void display() {
        System.out.println("Displaying image: " + filename);
    }
}

// 프록시 객체
public class ImageProxy implements Image {
    private String filename;
    private RealImage realImage;

    public ImageProxy(String filename) {
        this.filename = filename;
    }

    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}

// 클라이언트 코드
public class Client {
    public static void main(String[] args) {
        Image image = new ImageProxy("image.jpg");
        image.display();
    }
}
```