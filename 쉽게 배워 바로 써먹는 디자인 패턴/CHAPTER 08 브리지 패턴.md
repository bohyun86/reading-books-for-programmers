<h3>내용정리</h3>
<p>상속은 클래스의 계층을 분리하고 기능을 확장하지만 강력한 결합관계와 불필요한 메소드도 같이 포함</p>
<p>브리지 패턴을 적용하여 해결 가능</p>
<p>브리지 패턴은 복합 객체를 다시 재정의하여 추상 계층화된 구조
<br/>- 하나의 계층만으로 설계된 복합 객체는 브리지 패턴 아님</p>
<p>브리지는 구현 계층과 추상 계층 두곳을 연결하는 다리</p>

<h4>브리지 패턴의 구성요소</h4>
<table>
    <thead>
        <tr>
            <th>구성요소</th>
            <th>설명</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Implementor</td>
            <td>구현부의 인터페이스를 정의합니다.</td>
        </tr>
        <tr>
            <td>ConcreteImplementor</td>
            <td>구현부의 구체적인 로직을 포함합니다.</td>
        </tr>
        <tr>
            <td>Abstraction</td>
            <td>구현체의 인터페이스를 정의하며 클라이언트 코드가 이를 통해 구현체와 상호작용할 수 있습니다.</td>
        </tr>
        <tr>
            <td>RefinedAbstraction</td>
            <td>Abstraction의 하위 클래스이며 추가적인 기능을 제공합니다.</td>
        </tr>
    </tbody>
</table>

<h4>장점</h4>
<p>분리된 추상 계층과 구현 계층 독립적인 확장이 가능</p>
<h4>단점</h4>
<p>추상화를 통해 코드를 분리할 경우 설계가 복잡해짐</p>

## Implementor Interface

```java
// Implementor 인터페이스
interface Device {
    void turnOn();
    void turnOff();
    void setVolume(int volume);
}

// ConcreteImplementor 클래스
class TV implements Device {
    private int volume;

    @Override
    public void turnOn() {
        System.out.println("TV is turned on.");
    }

    @Override
    public void turnOff() {
        System.out.println("TV is turned off.");
    }

    @Override
    public void setVolume(int volume) {
        this.volume = volume;
        System.out.println("TV volume set to " + volume);
    }
}

class Radio implements Device {
    private int volume;

    @Override
    public void turnOn() {
        System.out.println("Radio is turned on.");
    }

    @Override
    public void turnOff() {
        System.out.println("Radio is turned off.");
    }

    @Override
    public void setVolume(int volume) {
        this.volume = volume;
        System.out.println("Radio volume set to " + volume);
    }
}

// Abstraction 클래스
abstract class RemoteControl {
    protected Device device;

    public RemoteControl(Device device) {
        this.device = device;
    }

    public void turnOn() {
        device.turnOn();
    }

    public void turnOff() {
        device.turnOff();
    }

    public void setVolume(int volume) {
        device.setVolume(volume);
    }
}

// RefinedAbstraction 클래스
class AdvancedRemoteControl extends RemoteControl {

    public AdvancedRemoteControl(Device device) {
        super(device);
    }

    public void mute() {
        device.setVolume(0);
        System.out.println("Device is muted.");
    }
}

// 클라이언트 코드
public class BridgePatternExample {
    public static void main(String[] args) {
        Device tv = new TV();
        RemoteControl tvRemote = new RemoteControl(tv);
        
        tvRemote.turnOn();
        tvRemote.setVolume(30);
        tvRemote.turnOff();

        Device radio = new Radio();
        AdvancedRemoteControl radioRemote = new AdvancedRemoteControl(radio);

        radioRemote.turnOn();
        radioRemote.setVolume(20);
        radioRemote.mute();
        radioRemote.turnOff();
    }
}

