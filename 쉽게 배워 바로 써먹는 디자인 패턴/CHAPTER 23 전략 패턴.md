# 전략 패턴(Stratege Pattern)

- 객체 내부에서 해결해야 하는 목적을 알고리즘 객체로 분리 적용하는 기법
- 전략: 알고리즘(주어진 문제를 해결하는 방법)
- 전술: 알고리즘이 동작하는 상세 내용
- 템플릿 메서드처럼 알고리즘의 일부만 변경 하는 것이 아니라 행위 전체를 변경

***분리***

- 외부 변화에 보다 쉽게 적응하려면 변화가 예상되는 부분을 분리 하는 것이 좋음
- 대부분 처리 로직 부분의 변화가 예상되므로, 처리 로직을 분리하는 것이 중요

***템플릿 메서드***

- 공통된 기능을 분리하여 템플릿화하고, 추상화를 통해 상황별로 다르게 처리할 수 있도록 실제 동작을 분리

***캡슐화***

- 분리된 알고리즘은 별도의 클래스로 캡슐화 = 전략
- 상황에 맞게 교체하면서 사용

***전략 패턴 예제***

```java
// 전략 인터페이스
// PaymentStrategy.java
public interface PaymentStrategy {
    void pay(int amount);
}

// CreditCardPayment.java
public class CreditCardPayment implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public CreditCardPayment(String name, String cardNumber, String cvv, String dateOfExpiry) {
        this.name = name;
        this.cardNumber = cardNumber;
        this.cvv = cvv;
        this.dateOfExpiry = dateOfExpiry;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid with credit card.");
    }
}

// PayPalPayment.java
public class PayPalPayment implements PaymentStrategy {
    private String emailId;
    private String password;

    public PayPalPayment(String emailId, String password) {
        this.emailId = emailId;
        this.password = password;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using PayPal.");
    }
}

// CryptoPayment.java
public class CryptoPayment implements PaymentStrategy {
    private String walletAddress;

    public CryptoPayment(String walletAddress) {
        this.walletAddress = walletAddress;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using Cryptocurrency.");
    }
}

// ShoppingCart.java
public class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(int amount) {
        paymentStrategy.pay(amount);
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // 신용카드 결제
        cart.setPaymentStrategy(new CreditCardPayment("John Doe", "1234567890123456", "786", "12/23"));
        cart.checkout(100);

        // 페이팔 결제
        cart.setPaymentStrategy(new PayPalPayment("myemail@example.com", "mypassword"));
        cart.checkout(200);

        // 암호화폐 결제
        cart.setPaymentStrategy(new CryptoPayment("1A2B3C4D5E6F7G8H9I0J"));
        cart.checkout(300);
    }
}

```
