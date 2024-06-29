### 어댑터 패턴(Adapter Pattern)
어댑터 패턴(래퍼 패턴, 중개 패턴): 보정만을 위해 설계된 객체
수정 불가능한 문제를 분리된 객체로 쉽게 해결하도록 도움
연관성이 없는 2개의 객체를 묶어 인터페이스를 통일화 -> 변경 인터페이스로 기존의 코드를 재사용
#### 클래스 어댑터
- 2개의 클래스를 상속받아 기존 클래스의 메서드를 다른 메서드로 대체하는 방법
- 최신 프로그래밍 언어는 다중 상속 지원하지 않아 클래스 어댑터 표현 어려움

#### 객체 어댑터
- 객체의 의존성을 이용해 문제 해결

어댑터 패턴은 220V를 110V에 연결하기 위한 컨버터를 사용하는 것과 유사

### 어댑터 패턴의 예를 자바 언어로 작성

```java
// Target interface
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Adaptee class
class AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file: " + fileName);
    }

    public void playMp4(String fileName) {
        System.out.println("Playing mp4 file: " + fileName);
    }
}

// Adapter class
class MediaAdapter implements MediaPlayer {
    private AdvancedMediaPlayer advancedMediaPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer = new AdvancedMediaPlayer();
        }
    }

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMediaPlayer.playVlc(fileName);
        }
    }
}

// Client class
class AudioPlayer implements MediaPlayer {
    private MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file: " + fileName);
        } else if (audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media type: " + audioType);
        }
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.play("mp3", "song.mp3");
        audioPlayer.play("vlc", "movie.vlc");
        audioPlayer.play("mp4", "video.mp4");
        audioPlayer.play("avi", "video.avi");
    }
}
```

이 예제는 어댑터 패턴을 사용하여 `MediaPlayer` 인터페이스를 구현하는 `AudioPlayer` 클래스가 `AdvancedMediaPlayer` 클래스의 기능을 활용할 수 있도록 합니다. `MediaAdapter` 클래스는 `AdvancedMediaPlayer`를 `MediaPlayer` 인터페이스에 맞게 어댑팅하여 사용합니다. 이를 통해 `AudioPlayer`는 다양한 유형의 미디어 파일을 재생할 수 있습니다.