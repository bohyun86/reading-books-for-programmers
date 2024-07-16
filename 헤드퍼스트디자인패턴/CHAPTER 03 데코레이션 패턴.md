# 데코레이터 패턴(Decorator Pattern)

- 객체에 추가 요소를 동적으로 더할 수 있습니다. 데코레이터를 사용하면 서브클래스를 만들 때보다 훨씬 유연하게 기능을 확장할 수 있습니다.
- 데코레이터 형식이 그 데코레이터로 감싸는 객체의 형식과 같아야 함, 상속을 통해서 형식을 맞춤

## 데코레이터 패턴 요소

- Component: 인터페이스나 추상 클래스로 구성된 구성요소
- ConcreteComponent: Component의 구현 클래스
- Decorator: Component와 동일한 인터페이스를 가지며, ConcreteComponent 객체를 참조하는 인스턴스 변수를 가지고 있음
- ConcreteDecorator: Decorator의 하위 클래스로, 데코레이터의 기능을 확장하는 역할

## 디자인 원칙

- OCP(Open-Closed Principle): 클래스는 확장에는 열려 있어야 하지만 변경에는 닫혀 있어야 한다.

