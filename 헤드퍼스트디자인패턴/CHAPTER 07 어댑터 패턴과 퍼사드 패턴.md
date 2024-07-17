# 어댑터 패턴(Adapter Pattern)

- 특정 클래스 인터페이스를 클라이언트에서 요구하는 다른 인터페이스로 변환
- 인터페이스가 호환되지 않아 같이 쓸 수 없었던 클래스를 사용할 수 있게 도와줌

## 어댑터 패턴의 구성 요소

- Target: 클라이언트가 사용할 인터페이스
- Adaptee: 어댑터 패턴을 적용할 클래스
- Adapter: Target 인터페이스를 구현하고, Adaptee 인스턴스를 포함하는 클래스

## 객체 어댑터와 클래스 어댑터

- 객체 어댑터: 어댑터 클래스가 Adaptee 클래스를 포함
- 클래스 어댑터: 어댑터 클래스가 Adaptee 클래스를 상속(자바에서는 다중 상속 지원 안함)

## 관련 패턴들 구분

- 데코레이터: 인터페이스는 바꾸지 않고 책임(기능)만 추가
- 어댑터: 하나의 인터페이스를 다른 인터페이스로 변환
- 퍼사드: 인터페이스를 간단하게 변경

# 퍼사드 패턴(Facade Pattern)

- 인터페이스를 단순하게 만들고 클라이언트와 구성 요소로 이루어진 서브시스템을 분리하는 역할을 함
- 서브시스템에 있는 일련의 인터페이스를 통합 인터페이스로 묶음
- 고수준 인터페이스도 정의하므로 서브시스템을 더 편리하게 사용할 수 있음


## 디자인 원칙

- 최소 지식 원칙(Principle of Least Knowledge): 객체 사이의 상호작용을 최소화하여 객체 간 결합도를 낮춤

***가이드 라인***
1. 객체 자체
2. 메소드에 매개변수로 전달된 객체
3. 메소드를 생성하거나 인스턴스를 만든 객체
4. 객체에 속하는 구성 요소

## 최소 지식 원칙 예제

- 위반한 경우

```java
class Address {
    private String street;

    public String getStreet() {
        return street;
    }

    public void setStreet(String street) {
        this.street = street;
    }
}

class Customer {
    private Address address;

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }
}

class Order {
    private Customer customer;

    public Customer getCustomer() {
        return customer;
    }

    public void setCustomer(Customer customer) {
        this.customer = customer;
    }
}

class OrderProcessor {
    public void printCustomerStreet(Order order) {
        // 최소 지식 원칙을 위반한 코드
        System.out.println(order.getCustomer().getAddress().getStreet());
    }
}
```

- 준수한 경우

```java
class Address {
    private String street;

    public String getStreet() {
        return street;
    }

    public void setStreet(String street) {
        this.street = street;
    }
}

class Customer {
    private Address address;

    public Address getAddress() {
        return address;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    // Customer 클래스가 자신의 주소 정보를 제공하는 메서드를 추가
    public String getCustomerStreet() {
        return address.getStreet();
    }
}

class Order {
    private Customer customer;

    public Customer getCustomer() {
        return customer;
    }

    public void setCustomer(Customer customer) {
        this.customer = customer;
    }

    // Order 클래스가 자신의 고객의 주소 정보를 제공하는 메서드를 추가
    public String getCustomerStreet() {
        return customer.getCustomerStreet();
    }
}

class OrderProcessor {
    public void printCustomerStreet(Order order) {
        // 최소 지식 원칙을 준수한 코드
        System.out.println(order.getCustomerStreet());
    }
}
```