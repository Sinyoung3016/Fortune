---
layout: post
title: "[객체지향설계] Design Patterns"
date: 2020-10-24 00:00:00
categories: [SOPHOMORE]
tags: [OBJECT_ORIENTED_PROGRAMMING]
last_modified_at: 2020-10-25
---

[https://refactoring.guru/design-patterns](https://refactoring.guru/design-patterns)

---

### Design Pattern

<p>
: 소프트웨어를 설계할 때 자주 발생하는 문제를 정형화하여 재사용할 수 있게 하는 해결책
<br>: 확장과 수정이 용이하여, 설계 이후에도 추가적인 유지보수 비용이 적음
<br>: = 응집도는 높이고 결합도는 낮게
<br>: Context(상황), Problem(문제), Solution(해결책)으로 구성
</p>

<p>
<br>Types of Design Patterns
<br>* Creational : 객체 생성에 관련된 패턴, 캡슐화
<br>* Structural : 클래스와 객체를 조합한 더 큰 구조를 만드는 패턴
<br>* Behavioral : 클래스와 객체 간의 상호 작용에 관련된 패턴, 책임과 역할 분배
</p>

#### SingleTon_Creational

<p>
: 전역 변수를 사용하지 않고, 객체를 하나만 생성하여, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴
<br>: 하나의 인스턴스만 생성해야하기 때문에, getInstance메소드를 통해 모든 클라이언트에게
동일한 인스턴스를 반환함.
</p>

<p>
예를 들어, 프린트 하나를 10개의 앱에서 공유하여 사용한다.
<br>프린터는 하나이기 때문에 Printer Class를 이용하려면, new Printer()가 반드시
<br>한번만 호출되어야 한다. 따라서 외부에서 생성자를 호출할 수 없게 생성자는 private하다.
<br>외부에 인스턴스를 제공하는 메소드는 static하다.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/7-1.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
public final class Singleton {
    //상속을 막기 위해 final
    private static Singleton instance;
    //instance의 값을 유지하기 위해 static
    public String value;

    private Singleton(String value) {
        try {
            Thread.sleep(1000);
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        }
        this.value = value;
    }

    public static Singleton getInstance(String value) {
        if (instance == null) {
            instance = new Singleton(value);
        }
        return instance;
        //하나의 객체만을 반환.
    }
}
```

---

#### Factory Method_Creational

<p>
: 객체 생성 처리를 서브 클래스로 분리해 처리하도록 캡슐화하는 패턴
<br>즉, 객체의 생성 코드를 별도의 클래스나 메소드르 분리해, 객체 생성의 변화에 대비.
</p>

<p>
* Product : 팩토리 메소드로 생성될 객체의 공통 인터페이스
<br>* ConcreteProduct : 구체적으로 객체가 생성되는 클래스
<br>* Creator : 펙토리 메소드를 갖는 클래스
<br>* ConcreteCreator : 펙토리 메소드를 구현하는 클래스로 ConcreteProduct 객체를 생성
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/7-2.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
public interface Button { //Product
    void render();
    void onClick();
}
public class HtmlButton implements Button { //ConcreteProduct
    public void render() {
        System.out.println("HtmlButton-render");
    }
    public void onClick() {
        System.out.println("HtmlButton-onclick");
    }
}
public class WindowsButton implements Button { //ConcreteProduct
    public void render() {
        System.out.println("WindowButton-render");
    }
    public void onClick() {
        System.out.println("WindowButton-onclick");
    }
}

public abstract class Dialog { //Creator

    public void renderWindow() {
        Button okButton = createButton();
        okButton.render();
    }
    public abstract Button createButton();
}
public class HtmlDialog extends Dialog { //ConcreteCreator

    @Override
    public Button createButton() {
        return new HtmlButton();
    }
}
public class WindowsDialog extends Dialog { //ConcreteCreator

    @Override
    public Button createButton() {
        return new WindowsButton();
    }
}

public class Demo {
    private static Dialog dialog;

    public static void main(String[] args) {
        configure();
        runBusinessLogic();
    }

    static void configure() {
        if (System.getProperty("os.name").equals("Windows 10")) {
            dialog = new WindowsDialog();
        } else {
            dialog = new HtmlDialog();
        }
    }

    static void runBusinessLogic() {
        dialog.renderWindow();
    }
}

```

---

#### Strategy_Behavioral

<p>
: 행위를 클래스로 캡슐화 하여 동적으로 행위를 자유롭게 바꿀 수 있게하는 패턴
<br>같은 문제를 해결하는 여러 알고리즘이 클래스별로 캡슣화되어 있고 이들이 필요할 때,
구조가 변하지 않고 교체할 수 있도록 함으로써 동일한 문제를 다른 알고리즘으로 해결할 수 있게함.
<br> 즉, 전략을 쉽게 바꿀 수있도록 해주는 디자인 패턴
</p>

<p>
* Strategy
<br>&emsp;: 인터페이스나 추상 클래스로 외부에서 동일한 방식으로 알고리즘을 호출하는 방법을 명시
<br>* ConcreteStrategy
<br>&emsp;: 패턴에서 명시한 알고리즘을 실제로 구현한 클래스
<br>* Context
<br>&emsp;: 패턴을 이용하는 역할, 필요에 따라 동적으로 구체적인 전략을 바꿀 수 있도록 Setter메소드를 제공.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/7-3.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
public interface Strategy {
   public int doOperation(int num1, int num2);
}
public class OperationAdd implements Strategy{ //ConcreteStrategy
   @Override
   public int doOperation(int num1, int num2) {
      return num1 + num2;
   }
}
public class OperationSubstract implements Strategy{ //ConcreteStrategy
   @Override
   public int doOperation(int num1, int num2) {
      return num1 - num2;
   }
}
public class OperationMultiply implements Strategy{ //ConcreteStrategy
   @Override
   public int doOperation(int num1, int num2) {
      return num1 * num2;
   }
}

public class Context {
   private Strategy strategy;

   public Context(Strategy strategy){
      this.strategy = strategy;
   }

   public int executeStrategy(int num1, int num2){
      return strategy.doOperation(num1, num2);
   }
}

public class Demo {
   public static void main(String[] args) {
      Context context = new Context(new OperationAdd());
      System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

      context = new Context(new OperationSubstract());
      System.out.println("10 - 5 = " + context.executeStrategy(10, 5));

      context = new Context(new OperationMultiply());
      System.out.println("10 * 5 = " + context.executeStrategy(10, 5));
   }
}
```
---

#### Observer_Behavioral

<p>
: 한 객체의 상태 변화에 따라 다른 객체의 상태도 연동되도록 일대다 객체 위존 관계를 구성하는 패턴
<br>: 데이터의 변경이 발생했을 겅우, 상태 클래스나 객체에 의존하지 않으면서, 데이터 변경을 통보함.
</p>

<p>
예를 들어, 유튜브를 구독하면, 해당 유튜브의 새로운 동영상이 업데이트 되면(state), 알림이 온다.(update)
<br>구독을 해지하면, 더 이상 알림이 오지 않는다. 여기서는 observer가 구독자, subject가 유튜버.
</p>

<p>
<br>* Observer : 데이터의 변경을 통보받는 인터페이스
<br>* Subject : ConcreteObserver객체를 관리
<br>* ConcreteObserver
<br>&emsp;: ConcreteSubject 의 변경을 통보받는 클래스로, 데이터 변경을 위해 setState가 있음.
<br>* ConcreteSubject
<br>&emsp;: 변경 관리 대상이 되는 데이터가 있는 통보하는 클래스로, update를 구현하여 변경을 통보받음.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/7-4.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
public class Subject {

   private List<Observer> observers = new ArrayList<Observer>();
   private int state;

   public int getState() {
      return state;
   }
   public void setState(int state) {
      this.state = state;
      notifyAllObservers();
   }
   public void attach(Observer observer){
      observers.add(observer);
   }
   public void notifyAllObservers(){
      for (Observer observer : observers) {
         observer.update();
      }
   }
}

public abstract class Observer {
   protected Subject subject;
   public abstract void update();
}
public class BinaryObserver extends Observer{
   public BinaryObserver(Subject subject){
      this.subject = subject;
      this.subject.attach(this);
   }
   @Override
   public void update() {
      System.out.println( "Binary String: " + Integer.toBinaryString( subject.getState() ) );
   }
}
public class OctalObserver extends Observer{
   public OctalObserver(Subject subject){
      this.subject = subject;
      this.subject.attach(this);
   }
   @Override
   public void update() {
     System.out.println( "Octal String: " + Integer.toOctalString( subject.getState() ) );
   }
}
public class HexaObserver extends Observer{
   public HexaObserver(Subject subject){
      this.subject = subject;
      this.subject.attach(this);
   }
   @Override
   public void update() {
      System.out.println( "Hex String: " + Integer.toHexString( subject.getState() ).toUpperCase() );
   }
}

public class Demo {
   public static void main(String[] args) {
      Subject subject = new Subject();

      new HexaObserver(subject);
      new OctalObserver(subject);
      new BinaryObserver(subject);

      System.out.println("First state change: 15");
      subject.setState(15);
      System.out.println("Second state change: 10");
      subject.setState(10);
   }
}
```

---

#### Adapter_Structual

<p>
: 한 클래스의 인터페이스를 클라이언트에서 사용하고자 하는 다른 인터페이스로 변환할 때 사용.
<br>: 이를 사용하면, 인터페이스 호환성이 맞지 않아 같이 사용할 수 없는 클래스를 연관 관계로 연결해서 사용 가능.
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/7-5.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
public interface AdvancedMediaPlayer {
   public void playVlc(String fileName);
   public void playMp4(String fileName);
}
public class VlcPlayer implements AdvancedMediaPlayer{
   @Override
   public void playVlc(String fileName) {
      System.out.println("Playing vlc file. Name: "+ fileName);
   }
   @Override
   public void playMp4(String fileName) {
      //do nothing
   }
}
public class Mp4Player implements AdvancedMediaPlayer{

   @Override
   public void playVlc(String fileName) {
      //do nothing
   }
   @Override
   public void playMp4(String fileName) {
      System.out.println("Playing mp4 file. Name: "+ fileName);
   }
}

public interface MediaPlayer {
   public void play(String audioType, String fileName);
}
public class MediaAdapter implements MediaPlayer {
   AdvancedMediaPlayer advancedMusicPlayer;

   public MediaAdapter(String audioType){
      if(audioType.equalsIgnoreCase("vlc") ){
         advancedMusicPlayer = new VlcPlayer();
      }else if (audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer = new Mp4Player();
      }
   }

   @Override
   public void play(String audioType, String fileName) {
      if(audioType.equalsIgnoreCase("vlc")){
         advancedMusicPlayer.playVlc(fileName);
      }
      else if(audioType.equalsIgnoreCase("mp4")){
         advancedMusicPlayer.playMp4(fileName);
      }
   }
}
public class AudioPlayer implements MediaPlayer {
   MediaAdapter mediaAdapter;

   @Override
   public void play(String audioType, String fileName) {
      if(audioType.equalsIgnoreCase("mp3")){
         System.out.println("Playing mp3 file. Name: " + fileName);
      }
      else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")){
         mediaAdapter = new MediaAdapter(audioType);
         mediaAdapter.play(audioType, fileName);
      }
      else{
         System.out.println("Invalid media. " + audioType + " format not supported");
      }
   }
}

public class Demo {
   public static void main(String[] args) {
      AudioPlayer audioPlayer = new AudioPlayer();

      audioPlayer.play("mp3", "beyond the horizon.mp3");
      audioPlayer.play("mp4", "alone.mp4");
      audioPlayer.play("vlc", "far far away.vlc");
      audioPlayer.play("avi", "mind me.avi");
   }
}
```

---

#### Bridge_Structural

<p>
: 구현부에서 추상층을 분리하여, 각자 독립적으로 변형과 확장이 가능하게 함.
<br>: 즉, 기능과 구현에 대해서 두 개를 별도의 클래스로 구현.
</p>

<p>
* Abstraction
<br>&emsp;: 기능 계층 구현 부분에 해당하는 클래스를 인스턴스로 가지고, 해당 인스턴스를 통해 구현부분의 메소드를 호출
<br>* RefindedAbstraction
<br>&emsp;: 기능 계층에서 새로운 부분을 확장한 클래스
<br>* Implementor
<br>&emsp;: Abstraction의 기능을 구현하기 위한 인터페이스
<br>* ConcreteImplementor
<br>&emsp;: 실제 기능을 구현
</p>

<figure>
<center><img src="/Fortune/assets/sophomore/OOP/7-6.png" alt="Midnight" style="width:100%"></center>
</figure>

```{.cpp}
public interface Device { //Implementor
    boolean isEnabled();
    void enable();
    void disable();
    void printStatus();
}
public class Radio implements Device { //ConcreteImplementor
    private boolean on = false;
    @Override
    public boolean isEnabled() {
        return on;
    }
    @Override
    public void enable() {
        on = true;
    }
    @Override
    public void disable() {
        on = false;
    }
    @Override
    public void printStatus() {
        System.out.println("| I'm radio.");
    }
}
public class Tv implements Device { //ConcreteImplementor
    private boolean on = false;

    @Override
    public boolean isEnabled() {
        return on;
    }
    @Override
    public void enable() {
        on = true;
    }
    @Override
    public void disable() {
        on = false;
    }
    @Override
    public void printStatus() {
        System.out.println("| I'm TV set.");
    }
}

public interface Remote { //Abstraction
    void power();
}
public class BasicRemote implements Remote { //RefinedAbstraction
    protected Device device;

    public BasicRemote() {}
    public BasicRemote(Device device) {
        this.device = device;
    }
    @Override
    public void power() {
        System.out.println("Remote: power toggle");
        if (device.isEnabled()) {
            device.disable();
        } else {
            device.enable();
        }
    }
}
public class AdvancedRemote extends BasicRemote {

    public AdvancedRemote(Device device) {
        super.device = device;
    }
    public void mute() {
        System.out.println("Remote: mute");
        device.setVolume(0);
    }
}

public class Demo {
    public static void main(String[] args) {
        testDevice(new Tv());
        testDevice(new Radio());
    }

    public static void testDevice(Device device) {
        System.out.println("Tests with basic remote.");
        BasicRemote basicRemote = new BasicRemote(device);
        basicRemote.power();
        device.printStatus();

        System.out.println("Tests with advanced remote.");
        AdvancedRemote advancedRemote = new AdvancedRemote(device);
        advancedRemote.power();
        device.printStatus();
    }
}
```

<br>
<br>



