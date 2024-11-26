## 내용 정리
- 빌더 패턴은 복잡한 구조를 가진 복합 객체의 생성 과정을 분리하여 처리하는 패턴
- 팩토리 패턴은 단일 클래스의 객체만 생성, 반환하므로 요청된 객체가 복합 객체일 경우 팩토리 패턴 적용 못함
- 복합 객체는 한 단계로만 생성 못함 -> 단계별로 객체 생성 분리하고 관계를 결합하는 과정 필요
- 복합 객체 생성 로직을 별도 클래스로 분리하며 분리한 로직을 알고리즘이라 부름
- 빌더 패턴은 추상 팩토리에서 유사한 객체의 제품군을 알고리즘화하여 다양한 복합 객체를 생성, 관리하는 용도로 사용

---

### 빌더 패턴 (Builder Pattern)이란?
**빌더 패턴 (Builder Pattern)**은 객체의 생성 과정에서 복잡한 단계가 필요한 경우, 각 단계를 개별적으로 수행하면서 최종적으로 객체를 생성할 수 있도록 도와주는 생성 패턴 중 하나입니다. 즉, 복잡한 객체를 생성하는 과정을 캡슐화하여 더 간단하고 유연하게 객체를 만들 수 있게 합니다.

빌더 패턴은 특히 객체 생성 시 매개변수가 많거나, 다양한 형태의 객체를 생성해야 할 때 유용합니다. 이러한 복잡성을 줄이기 위해 객체의 생성 과정을 분리하고, 체이닝(Chaining) 방식으로 가독성 있는 객체 생성 메서드를 제공합니다.

#### 빌더 패턴의 특징
1. **객체의 불변성 유지**: 빌더 패턴은 필수적인 속성과 선택적인 속성을 명확하게 구분하여 객체를 생성합니다. 이를 통해 생성된 객체의 불변성을 보장할 수 있습니다.
2. **가독성**: 필드가 많은 객체를 생성할 때 빌더 패턴을 사용하면 객체 생성 과정이 가독성이 높아지고 코드를 이해하기 쉬워집니다.
3. **유연성**: 생성자의 매개변수 개수가 많아질 때 빌더 패턴은 여러 생성자의 필요성을 없애고, 사용자가 필요한 필드만 설정할 수 있도록 유연성을 제공합니다.

### 빌더 패턴을 사용한 자바 예제
아래 예시는 빌더 패턴을 사용해 `Car` 객체를 생성하는 예제입니다. `Car` 클래스는 다양한 속성(모델, 색상, 엔진 타입 등)을 가질 수 있으며, 빌더 패턴을 통해 각 속성을 설정하여 객체를 생성합니다.

```java
// Car 클래스 정의
public class Car {
    // 필드들
    private final String model;         // 필수
    private final String color;         // 필수
    private final String engineType;    // 선택
    private final int doors;            // 선택

    // private 생성자 - 빌더만이 객체를 생성할 수 있도록 제한
    private Car(CarBuilder builder) {
        this.model = builder.model;
        this.color = builder.color;
        this.engineType = builder.engineType;
        this.doors = builder.doors;
    }

    // toString 메서드 - 객체 정보를 출력하기 위한 용도
    @Override
    public String toString() {
        return "Car{" +
                "model='" + model + '\'' +
                ", color='" + color + '\'' +
                ", engineType='" + engineType + '\'' +
                ", doors=" + doors +
                '}';
    }

    // CarBuilder 클래스 (내부 정적 클래스)
    public static class CarBuilder {
        // 필드들 - Car 클래스와 동일한 필드 정의
        private final String model;
        private final String color;
        private String engineType = "default engine";  // 기본값 제공
        private int doors = 4;                         // 기본값 제공

        // 필수 필드에 대한 빌더 생성자
        public CarBuilder(String model, String color) {
            this.model = model;
            this.color = color;
        }

        // 선택적 필드 설정 메서드들
        public CarBuilder engineType(String engineType) {
            this.engineType = engineType;
            return this;  // 체이닝을 위해 자기 자신 반환
        }

        public CarBuilder doors(int doors) {
            this.doors = doors;
            return this;  // 체이닝을 위해 자기 자신 반환
        }

        // 빌더를 통해 최종적으로 Car 객체 생성
        public Car build() {
            return new Car(this);
        }
    }
    
    // 테스트용 메인 메서드
    public static void main(String[] args) {
        // 빌더를 사용한 Car 객체 생성
        Car car1 = new Car.CarBuilder("Sedan", "Red")
                        .engineType("V8")
                        .doors(2)
                        .build();
                        
        System.out.println(car1);

        Car car2 = new Car.CarBuilder("SUV", "Blue")
                        .build();  // 선택적 필드 설정 없이 기본값 사용

        System.out.println(car2);
    }
}
```

### 코드 설명
1. **Car 클래스**:
   - `Car` 클래스는 **모델**, **색상**, **엔진 타입**, **문 개수**라는 필드를 가지고 있습니다.
   - 이 중 `model`과 `color`는 필수 필드이고, `engineType`과 `doors`는 선택적인 필드입니다.
   - `Car` 클래스의 생성자는 `private`으로 선언되어 있어 외부에서 직접 생성할 수 없으며, **빌더**를 통해서만 객체를 생성할 수 있습니다.

2. **CarBuilder 클래스**:
   - `CarBuilder`는 `Car` 클래스 내부에 있는 **정적 클래스**입니다.
   - 빌더 클래스는 `Car` 클래스와 동일한 필드를 가지고 있으며, 필수적인 필드는 생성자에서 설정하고, 선택적인 필드는 **체이닝 메서드**(`engineType`, `doors`)를 통해 설정합니다.
   - `build()` 메서드를 호출하면 최종적으로 `Car` 객체를 생성합니다.

3. **체이닝**:
   - 빌더 패턴은 **체이닝**을 사용해 객체를 생성할 수 있도록 하므로, 가독성이 매우 좋습니다.
   - 예를 들어 `new Car.CarBuilder("Sedan", "Red").engineType("V8").doors(2).build();`와 같이 체이닝으로 쉽게 객체를 설정하고 생성할 수 있습니다.

4. **예제 실행 결과**:
   ```
   Car{model='Sedan', color='Red', engineType='V8', doors=2}
   Car{model='SUV', color='Blue', engineType='default engine', doors=4}
   ```
   - `car1`은 모든 필드를 설정한 경우이고, `car2`는 필수 필드만 설정하고 나머지는 **기본값**을 사용한 경우입니다.

### 빌더 패턴의 장점
1. **가독성**: 빌더 패턴을 사용하면 필드의 갯수가 많거나, 여러 생성자를 만들기 번거로운 경우 체이닝을 사용해 객체 생성 과정을 더 가독성 있게 표현할 수 있습니다.
2. **유연성**: 객체 생성 시 필요한 필드만 설정하고 불필요한 필드는 생략할 수 있습니다.
3. **유지보수**: 코드 변경이 필요할 때, 기존 생성자의 매개변수를 수정하는 대신 빌더 클래스에서 새로운 메서드를 추가하여 손쉽게 확장할 수 있습니다.
4. **불변성**: 객체가 생성된 이후에는 변경되지 않도록 설계하여 불변성을 유지할 수 있습니다.

### 빌더 패턴의 사용 시기
- **객체 생성에 많은 매개변수가 필요한 경우**: 객체를 생성할 때 필드가 많고, 여러 생성자가 필요할 때 빌더 패턴을 사용하면 더 쉽게 관리할 수 있습니다.
- **생성자 오버로딩을 줄이고 싶을 때**: 다양한 조합의 매개변수를 가진 생성자를 여러 개 만드는 대신, 빌더 패턴으로 객체 생성을 더 깔끔하고 유연하게 할 수 있습니다.
- **복잡한 객체를 단계적으로 생성하고 싶은 경우**: 필수적인 필드를 먼저 설정하고, 이후에 선택적인 필드를 단계적으로 설정하는 방식이 유리할 때 사용합니다.

빌더 패턴은 특히 코드의 **가독성**과 **유지보수성**을 높이기 위해 많이 사용되며, 이러한 장점 덕분에 최근에는 롬복(Lombok) 라이브러리와 같은 자동 빌더 생성 도구를 통해 많이 사용되고 있습니다.