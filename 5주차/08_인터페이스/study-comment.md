## 8.1 인터페이스의 역할

---

- 자바에서 인터페이스는 객체의 사용 방법을 정의한 타입이다.
- 인터페이스는 객체의 교환성을 높여주기 때문에 다형성을 구현하는 매우 중요한 역할을 한다.
- 개발 코드가 직접 객체의 메소드를 호출하면 간단한데 중간에 인터페이스를 두는지?
    - 개발 코드를 수정하지 않고 사용하는 객체를 변경할 수 있도록 하기 위해서
    - 인터페이스는 하나의 객체가 아니라 여러 객체들과 사용이 가능하므로 어떤 객체를 사용하느냐에 따라서 실행 내용과 리턴 값이 다를 수 있다.
    - 개발 코드 측면에서 코드 변경 없이 실행 내용과 리턴값을 다양화할 수 있다.

## 8.2 인터페이스 선언

---

### 8.2.1 인터페이스 선언

```java
[ public ] interface 인터페이스명 {...}
```

- 인터페이스 이름은 클래스 이름을 작성하는 방법과 동일하다.
- 첫문자를 대문자로 하고 나머지는 소문자로 작성하는 것이 관례
- public 접근 제한은 다른 패키지에서도 인터페이스를 사용할 수 있도록 해준다.

```java
public interface RemoteControl {}
```

- 클래스는 필드, 생성자, 메소드를 구성 멤버로 가지는데 비해 인터페이스는 상수와 메소드만 구성멤버로 가진다.
- 인터페이스는 객체로 생성할 수 없기 때문에 생성자를 가질 수 없다.

```java
interface 인터페이스명 {
	//상수
	타입 상수명 = 값;
	//추상 메소드
	타입 메소드명(매개변수,...);
	//디폴트 메소드
	default 타입 메소드명(매개변수,...) {...}
	//정적 메소드
	static 타입 메소드명(매개변수) {...}
```

> 상수 필드
>
- 인터페이스는 객체 사용 설명서이므로 런타임 시 데이터를 저장할 수 있는 필드를 선언할 수 없다.
- 그러나 상수 필드 선언이 가능하다.
- 상수는 인터페이스에 고정된 값으로 런타임 시에 데이터를 바꿀 수 없다. 상수를 선언할 때는 반드시 초기값을 대입해야한다.

> 추상 메소드
>
- 객체가 가지고 있는 메소드를 설명한 것으로 호출할 때 어떤 매개값이 필요하고 리턴타입이 무엇인지만 알려준다.
- 실제 실행부는 객체가 가지고 있다.

> 디폴트 메소드
>
- 디폴트 메소드는 인터페이스에 선언되지만 사실은 객체가 가지고 있는 인스턴스 메소드라고 생각해야한다
    - 자바 8에서 디폴트 메소드를 허용한 이유는 기존 인터페이스를 확장해서 새로운 기능을 추가하기 위해서이다.

> 정적 메소드
>
- 정적 메소드도 역시 자바 8부터 작성할 수 있는데 디폴트 메소드와는 달리 객체가 없어도 인터페이스만으로 호출이 가능하다.

### 8.2.2 상수 필드 선언

- 인터페이스는 데이터를 저장할 수 없기 때문에 데이터를 저장할 인스턴스 또는 정적 필드를 선언할 수 없다.
- 대신 상수 필드만 선언할 수 있다.
- 상수는 public static final로 선언하는데 클래스에서 이미 학습한 바가 있다.
- 따라서 인터페이스에 선언된 필드는 모두 public static final의 특성을 갖는다.
- public, static, final을 생략하더라도 자동적으로 컴파일 과정에서 붙게된다.

```java
[ public static final ] 타입 상수명 = 값;
```

- 상수명은 대문자로 작성하되, 서로 다른 단어로 구성되어 있을 경우에는 언더바(_)로 연결하는 것이 관례이다.
- 인터페이스는 상수 static {} 블록으로 초기화할 수 없기 때문에 반드시 선언과 동시에 초기값을 지정해야한다.

- RemoteControl 인터페이스에 MAX_VALUE와 MIN_VALUE를 선언한 모습

```java
//RemoteControl.java 상수 필드 선언
public interface RemoteControl {
	public int MAX_VOLUME = 10;
	public int MIN_VOLUME = 0;

```

### 8.2.3 추상 메소드 선언

- 인터페이스를 통해 호출된 메소드는 최종적으로 객체에서 실행된다.
- 그렇기 때문에 인터페이스의 메소드는 실행 블록이 없는 추상 메소드로 선언한다.
    - 추상 메소드는 리턴 타입, 메소드명, 매게변수만 기술되고 중괄호 {}를 붙이지 않는 메소드
- 인터페이스에 선언된 추상 메소드는 모두 public abstract의 특성을 갖기 때문에 public abstract를 생략하더라도 자동적으로 컴파일 과정에서 붙게된다.
- 세 메소드는 모두 리턴 타입이 void라는 것과 turnOn(), turnOff() 메소드는 호출 시 매개값이 필요없고, setVolume() 메소드만 int  매개값이 필요함을 알려주고있다.

```java
//RemoteControl.java 메소드 선언

public interface RemoteControl {
	//상수
	public int MAX_VOLUME = 10;
	public int MIN_VOLUME = 0;
	
	//추상 메소드
	public void turnOn();
	public void turnOff();
	public void setVolume(int volume);
}
```

### 8.2.4 디폴트 메소드 선언

- 디폴트 메소드는 자바 8에서 추가된 인터페이스의 새로운 멤버다.
- 형태는 클래스의 인스턴스 메소드와 동일한데 default 키워드가 리턴 타입 앞에 붙는다.
- 디폴트 메소드는 public 특성을 갖기 때문에  public을 생략해도 자동적으로 컴파일 과정에서 붙게된다.

```java
[public] default 리턴타입 메소드명(매개변수, ...) {...}
```

- RemoteControl 인터페이스에서 무음 처리 기능을 제공하는 setMute() 디폴트 메소드를 선언했다

```java
//RemoteControl.java 메소드 선언

interface RemoteControl {
	//상수
	int MAX_VOLUME = 10;
	int MIN_VOLUME = 0;
	
	//추상 메소드
	void turnOn();
	void turnOff();
	void setVolume(int volume);
	
	//디폴트 메소드
	default void setMute(boolean mute) {
		if(mute) {
			System.out.println("무음 처리합니다");
		} else {
			System.out.println("무음 해제합니다");
		}
	}
}
```

### 8.2.5 정적 메소드 선언

- 정적 메소드는 디폴트 메소드와 마찬가지로 자바 8에서 추가된 인터페이스
- 형태는 클래스의 정적 메소드와 동일하다
- 정적 메소드는 public 특성을 갖기 때문에  public을 생략하더라도 자동적으로 컴파일 과정에서 붙게된다.

```java
[public] static 리턴타입 메소드명(매개변수, ...) {...}
```

- RemoteControl 인터페이스에서 밧데리를 교환하는 기능을 가진 changeBattery() 정적 메소드

```java
//RemoteControl.java 메소드 선언

public interface RemoteControl {
	//상수
	int MAX_VOLUME = 10;
	int MIN_VOLUME = 0;
	
	//추상 메소드
	void turnOn();
	void turnOff();
	void setVolume(int volume);
	
	//디폴트 메소드
	default void setMute(boolean mute) {
		if(mute) {
			System.out.println("무음 처리합니다");
		} else {
			System.out.println("무음 해제합니다");
		}
	}
	
	//정적 메소드
	static void changeBattery() {
		System.out.println("건전지를 교환합니다.");
	}
}
```

## 8.3 인터페이스 구현

---

- 개발코드가 인터페이스 메소드를 호출하면 인터페이스는 객체의 메소드를 호출한다.
- 객체는 인터페이스에서 정의된 추상 메소드와 동일한 메소드 이름, 매개 타입, 리턴 타입을 가진 실체 메소드를 가지고 있어야한다.
- 이러한 객체를 인터페이스의 구현 객체라고 하고 구현 객체를 생성하는 클래스를 구현 클래스라고 한다.

### 8.3.1 구현 클래스

- 구현 클래스는 보통의 클래스와 동일한데 인터페이스 타입으로 사용할 수 있음을 알려주기 위해 선언부에 implement 키워드를 추가하고 인터페이스명을 명시해야한다.

```java
public class 구현 클래스명 implements 인터페이스명 {
	//인터페이스에 선언된 추상 메소드의 실체 메소드 선언
}
```

- 인터페이스에 선언된 추상 메소드의 실체 메소드를 선언해야 한다.
- 다음은 Televison과 Audio라는 이름을 가지고 있는 RemoteControl 구현 클래스를 작성하는 방법
- 클래스 선언부 끝에 implements RemoteControl이 붙어 있기 때문에 이 두 클래스는 RemoteControl 인터페이스로 사용이 가능하다.
- RemoteControl에는 3개의 추상 메소드가 있기 때문에 Television과 Audio는 이 추상메소드들에 대한 실체 메소드를 가지고 있어야한다.

```java
//Television.java 구현 클래스

public class Television implements RemoteControl {
	//필드
	private int volume;
	
	//turnOn() 추상 메소드의 실체 메소드
	public void turnOn() {
		System.out.println("TV를 켭니다");
	}
	//turnOff() 추상 메소드의 실체 메소드
	public void turnOff() {
		System.out.println("TV를 끕니다");
	}
		//setVolume() 추상 메소드의 실체 메소드
		//인터페이스 상수를 이용해서 volume 필드의 값을 제한
	public void setVolume(int volume) {
		if(volume>RemoteControl.MAX_VOLUME) {
			this.volume = RemoteControl.MAX_VOLUME;
		} else if (volume<RemoteControl.MIN_VOLUME) {
			this.volume = RemoteControl.MIN_VOLUME;
		} else {
			this.volume = volume;
		}
		System.out.println("현재 TV 볼륨: " + volume);
	}
}
```

```java
//Audio.java 구현 클래스

public class Audio implements RemoteControl {
	//필드
	private int volume;
	
	//turnOn() 추상 메소드의 실체 메소드
	public void turnOn() {
		System.out.println("Audio를 켭니다.");
	}
	
	//turnOff() 추상 메소드의 실체 메소드
	public void turnOff() {
		System.out.println("Audio를 끕니다");
	}
		//setVolume() 추상 메소드의 실체 메소드
		//인터페이스 상수를 이용해서 volume 필드의 갑을 제한
	public void setVolume(int volume) {
		if(volume>RemoteControl.MAX_VOLUME) {
			this.volume = RemoteControl.MAX_VOLUME;
		} else if (volume<RemoteControl.MIN_VOLUME) {
			this.volume = RemoteControl.MIN_VOLUME;
		} else {
			this.volume = volume;
		}
		System.out.println("현재 Audio 볼륨: " + volume);
	}
}
```

- 구현 클래스에서 인터페이스의 추상 메소드들에 대한 실체 메소드를 작성할 때 주의할 점은 인터페이스의 모든 메소드는 기본적으로 public 접근 제한을 갖기 때문에 public보다 더 낮은 접근 제한으로 작성할 수 없다.
- public을 생략하면 “Cannot reduce the visibility of the inherited method”라는 컴파일 에러를 만나게 된다.
- 만약 인터페이스에 선언된 추상 메소드에 대응하는 실체 메소드를 구현 클래스가 작성하지 않으면 구현 클래스는 자동적으로 추상 클래스가 된다.
- 그렇기 때문에 클래스 선언부에 abstract 키워드를 추가해야한다.

```java
public abstract class Television implements RemoteControl {
	public void turnOn() {...}    //setVolume()실체 메소드가 없다
	public void turnOff() {...}   //일부만 구현
```

- 인터페이스의 추상메소드에 대한 실체 메소드를 자동으로 생성해주는 기능을 제공(이클립스)
    - 코드 창에서 인터페이스를 implements한 이후에 이클립스 메뉴에서 [Source → Override/implement Methods]를 선택하고 추상 메소드를 체크한 후 ok
- 구현 클래스가 작성되면 new  연산자로 객체를 생성할 수 있다.
- 문제는 어떤 타입의 변수에 대입하느냐이다.
- Television 객체를 생성하고 Television 변수에 대입한다고 인터페이스를 사용하는 것이 아니다.

```java
Television tv = new Television();
```

- 인터페이스로 구현 객체를 사용하려면 다음과 같이 인터페이스 변수를 선언하고 구현 객체를 대입해야한다.
- 인터페이스 변수는 참조 타입이기 때문에 구현 객체가 대입될 경우 구현 객체의 번지를 저장한다.

```java
인터페이스 변수;
변수 = 구현객체;
-------------------
인터페이스 변수 = 구현객체;
```

- RemoteControl 인터페이스로 구현 객체인 Television과 Audio를 사용하려면 RemoteControl 타입 변수 rc를 선언하고 구현 객체를 대입해야 한다.

```java
//RemoteControlExample.java 인터페이스 변수에 구현 객체 대입

public class RemoteControlExample {
	public static void main(String[] args) {
		RemoteControl  rc;
		rc = new Television();
		rc = new Audio();
	}
}
```

- 인터페이스 사용 방법은 다음절에 자세히 살펴보고 여기서는 구현 객체를 인터페이스 변수에 대입해서 사용한다는 것만 알아두자

### 8.3.2 익명 구현 객체

- 구현 클래스를 만들어 사용하는 것이 일반적이고, 클래스를 재사용할 수 없기 때문에 편리하지만 일회성의 구현 객체를 만들기 위해 소스 파일을 만들고 클래스를 선언하는 것은 비효율적이다.
- 자바는 소스 파일을 만들지 않고도 구현 객체를 만들 수 있는 방법을 제공하는데 이것이 익명 구현 객체이다.
- 다음은 익명 구현 객체를 생성해서 인터페이스 변수에 대입하는 코드이다.

```java
인터페이스 변수 = new 인터페이스() {
	//인터페이스에 선언된 추상 메소드의 실체 메소드 선언
};
```

- new 연산자 뒤에는 클래스 이름이 와야하는데, 이름이 없다.
- 인터페이스() {}는 인터페이스를 구현해서 중괄호{}와 같이 클래스를 선언하라는 뜻이고 new 연산자는 이렇게 선언된 클래스를 객체로 생성한다.
- 중괄호{}에는 인터페이스에 선언된 모든 추상 메소드들의 실체 메소드를 작성해야한다.
- 추가적으로 필드와 메소드를 선언할 수 있지만 익명 객체 안에서만 사용할 수 있고 인터페이스 변수로 접근할 수 없다.

```java
//RemoteControl의 익명 구현 객체

public class RemoteControlExample {
	public static void main(String[] args) {
		RemoteControl rc = new RemoteControl() {
			public void turnOn() {/*실행문*/}
			public void turnOff() {/*실행문*/}
			public void setVolume(int volume) {/*실행문*/}
		};
	}
}
```

- 모든 객체는 클래스로부터 생성되는데 익명 구현 객체도 마찬가지다
- RemoteControllerExample.java를 컴파일 하면 자바 컴파일러에 의해 자동으로 다음과 같은 클래스 파일이 만들어진다.

```java
RemoteControlExample$1.class
```

- RemoteControlExample 이름뒤에 $가 붙고 생성번호가 붙는데 생성 번호는 1부터 시작한다.
- 두번째 익명 구현 객체를 만들었다면 클래스 파일명은 RemoteControlExample$2

### 8.3.3 다중 인터페이스 구현 클래스

- 인터페이스 A와 B가 객체의 메소드를 호출할 수 있으려면 객체는 이 두 인터페이스를 모두 구현해야한다.

```java
public class 구현클래스명 implements 인터페이스A, 인터페이스B {
	//인터페이스 A에 선언된 추상 메소드의 실체 메소드 선언
	//인터페이스 B에 선언된 추상 메소드의 실체 메소드 선언
}
```

- 다중 인터페이스를 구현할 경우, 구현 클래스는 모든 인터페이스의 추상 메소드에 대해 실체 메소드를 작성해야한다.
- 만약 하나라도 없으면 추상 클래스로 선언해야한다.

```java
//인터넷을 검색할 수 있는 Searchable 인터페이스
// search()추상메소드는 매개값으로 url을받는다.

public interface Searchable {
	void search(String url);
}
```

- 만약 SmartTelevision이 인터넷 검색 기능도 제공한다면 RemoteControl과 Searchable을 모두 구현한 SmartTelevision 클래스를 작성한다.

```java
//SmartTelevision.java 다중 인터페이스 구현 클래스
public class SmartTelevision implements RemoteControl, Searchable {
	private int volume;

	public void turnOn() {
		System.out.println("TV를 켭니다");
	}
	public void turnOff() {
		System.out.println("TV를 끕니다");
	}
	public void setVolume(int volume) {
		if(volume>RemoteControl.MAX_VOLUME) {
			this.volume = RemoteControl.MAX_VOLUME;
		} else if(volume<RemoteControl.MIN_VOLUME) {
			this.volume = RemoteControl.MIN_VOLUME;
		} else {
			this.volume = volume;
		}
		System.out.println("현재 TV 볼륨: " + volume);
	}
	
	// RemoteContorl의 추상메소드에 대한 실체 메소드
	
	public void search(String url) {
		System.out.println(url + "을 검색합니다.");
	}
	//Searchaable의 추상 메소드에 대한 실체 메소드
}
```

## 8.4 인터페이스 사용

---

- 인터페이스로 구현 객체를 사용하려면 인터페이스 변수를 선언하고 구현 객체를 대입해야한다.

```java
인터페이스 변수;
변수 = 구현객체;
-------------------
인터페이스 변수 = 구현객체;
```

- 예를들어 RemoteControl 인터페이스로 구현 객체인 Television과 Audio를 사용하려면 RemoteControl 타입 변수 rc를 선언하고 구현 객체를 대입해야 한다.

```java

		RemoteControl  rc;
		rc = new Television();
		rc = new Audio();
```

- 개발 코드에서 인터페이스는 클래스의 필드, 생성자 또는 메소드의 매개 변수, 생성자 또는 메소드의 로컬 변수로 선언될 수 있다.

```java
publc class Myclass {
//필드
RemoteControl rc = new Television();

//생성자
MyClass (RemoteControl rc) {
	this.rc = rc;
}

//메소드
void methodA() {
	//로컬 변수
	RemoteControl rc = new Audio();
}

	void methodB(RemoteCotrol rc) {..}
}
```

### 8.4.1 추상 메소드 사용

- 구현 객체가 인터페이스 타입에 대입되면 인터페이스에 선언된 추상 메소드를 개발 코드에서 호출할 수 있게 된다.
- 개발 코드에서 RemoteControl의 변수 rc로 turnOn() 또는 turnOff() 메소드를 호출하면 구현 객체의 turnOn()과 turnOff() 메소드가 자동 실행된다.

```java
RemoteCotrol rc = new Telelvision();
rc.turnOn(); -> Television의 TurnOn()실행
rc.turnOff(); -> Television의 TurnOff()실행
```

```java
//RemoteCotrolExample.java 인터페이스 사용

public class RemoteCotrolExample {
	public static void main(String[] args) {
	
		RemoteControl rc = null;
		
		rc = new Television(); //인터페이스 변수 선언
		rc.turnOn();           //Television객체를 인터페이스 타입에 대입
		rc.turnOff();          //인터페이스의 turnOn(),turnOff()호출
		
		rc = new Audio();
		rc.turnOn();           //Audio 객체를 인터페이스 타입에 대입
		rc.turnOff();          //인터페이스의 turnOn(),turnOff()호출
```

### 8.4.2 디폴트 메소드 사용

- 디폴트 메소드는 인터페이스에서 선언되지만 인터페이스에서 바로 사용할 수 없다.
- 디폴트 메소드는 추상 메소드가 아닌 인스턴스 메소드이므로 구현 객체가 있어야 사용할 수 있다. 예를 들어 RemoteControl 인터페이스는 setMute()라는 디폴트 메소드를 가지고 있지만 이메소드를 다음과 같이 호출할수는 없다.

```java
RemoteControl.setMute(true);
```

- setMute()  메소드를 호출하려면  RemoteControl의 구현 객체가 필요한데, 다음과 같이 Television 객체를 인터페이스 변수에 대입하고 나서 setMute()를 호출할 수 있다.
- 비록 setMute()가 Television에 선언되지는 않았지만 Television 객체가 없다면 setMute도 호출할 수 없다.

```java
RemotoeControl rc = new Television();
rc.setMute(true);

```

- 디폴트 메소드는 인터페이스의 모든 구현 객체가 가지고 있는 기본 메소드라고 생각하면 된다.
- 그러나 어떤 구현 객체는 디폴트 메소드의 내용이 맞지 않아 수정이 필요할 수도 있다.
- 구현 클래스를 작성할 때 디폴트 메소드를 재정의(오버라이딩)해서 자신에게 맞게 수정하면 디폴트 메소드가 호출될 때 자신을 재정의한 메소드가 호출된다.

```java
//Audio는 디폴트 메소드를 재정의했다.
//Television과 Audio중 어떤 객체가 인터페이스에 대입되느냐에 따라서 setMute()
//디폴트의 실행 결과는 달라진다.

public class Audio implements RemoteControl{
	//필드
	private int volume;
	private boolean mute;
	
	//turnOn() 추상 메소드의 실체 메소드
	public void turnOn() {
		System.out.println("Audio를 켭니다");
	}
	//turnOff() 추상 메소드의 실체 메소드
	public void turnOff() {
		System.out.println("Audio를 끕니다");
	}
	//setVolume 추상 메소드의 실체 메소드
	public void setVolume(int volume) {
		if(volume>RemoteControl.MAX_VOLUME) {
			this.volume = RemoteControl.MAX_VOLUME;
		} else if(volume<RemoteControl.MIN_VOLUME) {
			this.volume = RemoteControl.MIN_VOLUME;
		} else {
			this.volume = volume;
		}
		System.out.println("현재 Audio 볼륨: " + volume);
	}
	
	@Override  //디폴트 메소드 재정의
	public void setMute(boolean mute) {
		this.mute = mute;
		if(mute) {
			System.out.println("Audio 무음 처리합니다.");
		} else {
			System.out.println("Audio 무음 해제합니다.");
		}
	}
}
```

```java
//RemoteContorlExample.java 디폴트 메소드 사용
public class RemoteCotrolExample {
	public static void main(String[] args) {
		RemoteControl rc = null;
		
		rc = new Television(); 
		rc.turnOn();           
		rc.setMute(true);        
		
		rc = new Audio();
		rc.turnOn();   
		rc.setMute(true);     
	}
}
```

### 8.4.3 정적 메소드 사용

- 인터페이스의 정적 메소드는 인터페이스로 바로 호출이 가능하다.

```java
//RemoteCotrol의 changeBattery() 정적 메소드를 호출한다
//RemoteCotrolExample.java 정적 메소드 사용

public class RemoteCotrolExample {
	public static void main(String[] args) {
		RemoteControl.changeBattery();
	}
}
```

## 8.5 타입 변환과 다양성

---

- 인터페이스도 다형성을 구현하는 기술이 사용된다.
- 오히려 요즘은 상속보다는 인터페이스를 통해서 다형성을 구현하는 경우가 많다
- 프로그램을 개발할 때 인터페이스를 사용해서 메소드를 호출하도록 코딩을 했다면 구현 객체를 교체하는것은 매우 손쉽고 빠르다.

### 8.5.3 자동 타입 변환

- 구현 객체가 인터페이스 타입으로 변환되는 것은 자동 타입 변환에 해당한다.
- 자동 타입 변환은 프로그램 도중에 자동적으로 타입 변환이 일어나는 것을 말한다.

```java
인터페이스 변수 = 구현 객체;
L------자동타입변환----
```

- 인터페이스 구현 클래스를 상속해서 자식 클래스를 만들었다면 자식 객체 역시 인터페이스 타입으로 자동 타입 변환 시킬 수 있다.
- 자동 타입 변환을 이용하면 필드의 다형성과 매개변수의 다형성을 구현할 수 있다.

### 8.5.2 필드의 다형성

- 한국 타이어와 금호 타이어는 공통적으로 인터페이스를 구현했기 때문에 모두 타이어 인터페이스에 있는 메소드를 가지고 있다.
- 따라서 타이어 인터페이스로 동일하게 사용할 수 있는 교체 가능한 객체에 해당한다.
- 자동차를 설계할 때 다음과 같이 필드 타입으로 타이어 인터페이스를 선언하게 되면 필드값으로 한국 타이어 또는 금호 타이어 객체를 대입할 수 있다.
- 자동 타입 변환이 일어나기 때문에 아무런 문제가 없다.

```java
public class Car {
	Tire frontLeftTire = new HankookTire();
	Tire frontRightTire = new HankookTire();
	Tire backLeftTire = new HankookTire();
	Tire backRightTire = new HankookTire();
```

- Car 객체를 생성한 후 초기값으로 대입한 구현 객체 대신 다른 구현  객체를 대입할 수도 있다. 이것이 타이어 교체에 해당한다.

```java
Car myCar = new Car();
myCar.frontLeftTire = new KumhoTire();
myCar.frontRightTire = new KumhoTire();
```

- frontLeftTire,backLeftTire 에 어떠한 타이어 구현 객체가 저장되어도 Car 객체는 타이어 인터페이스에 선언된 메소드만 사용하므로 전혀 문제가 되지 않는다.



```java
//Car 객체의 run() 메소드에서 타이어 인터페이스에 선언된 roll()메소드를 호출
void run() {
	frontLeftTire.roll();
	frontRightTire.roll();
	backLeftTire.roll();
	backRightTire.roll();
```

- frontRightTire와 backLeftTire를 교체하기 전에는 HankookTire 객체의 roll() 메소드가 호출되지만 KumhoTire로 교체된 후에는KumhoTire객체의 roll() 메소드가 호출된다.
- Car의 run() 메소드 수정 없이도 다양한 roll()  메소드의 실행 결과를 얻을 수 있다.

```java
//Tire.java 인터페이스
public interface Tire {
	public void roll(); // roll() 메소드 호출 방법 설명
}
```

```java
//HankookTire.java 구현 클래스

public class HankookTire implements Tire {
	@Override //Tire 인터페이스 구현
	public void roll() {
		System.out.println("한국 타이어가 굴러갑니다");
	}
}
```

```java
// KumhoTire.jav 구현 클래스
publi class KumhoTire implements Tire {
	@Override  //Tire  인터페이스 구현
	public void roll() {
		System.out.println("금호 타이어가 굴러갑니다");
	}
}
```

```java
//Car.java 필드의 다형성
public class Car { //인터페이스 타입 필드 선언과 초기 구현 객체 대입
	Tire frontLeftTire = new HankookTire();
	Tire frontRightTire = new HankookTire();
	Tire backLeftTire = new HankookTire();
	Tire backRightTire = new HankookTire();
	
	void run() { // 인터페이스에서 설명된 roll() 메소드 호출
		frontLeftTire.roll();
		frontRightTire.roll();
		backLeftTire.roll();
		backRightTire.roll();
	}
}
```

```java
//CarExample.java 필드의 다형성 테스트

public class CarExample {
	public static void mian(String[] args) {
		Car myCar = new Car();
		
		myCar.run();
		
		myCar.frontLeftTire = new KumhoTire();
		myCar.frontRightTire = new KumhoTire();
		
		myCar.run();
	}
}
		
```

### 8.5.3 인터페이스 배열로 구현 객체 관리

```java
Tire[] tires = {
	new HankookTire(),
	new HankookTire(),
	new HankookTire(),
	new HankookTire()
};
```

- 인터페이스 배열로 관리하면 인덱스 1을 이용해서 앞 오른쪽 타이어를 KumhoTire로 교체하기 위해 다음과 같이 작성한다.

```java
tires[1] = new KumhoTire();
```

- tires 배열의 각 항목은 Tire 인터페이스 타입이므로 구현 객체인 KumhoTire를 대입하면 자동 타입 변환이 발생하기 때문에 문제가 없다.

- 구현 객체들을 배열로 관리하면 제어문에서 가장 많이 혜택을 본다.
- 전체 타이어의 roll() 메소드를 호출하는 Car 클래스의 run() 메소드는 다음과 같이 for 문으로 작성할 수 있다.

```java
void run() {
	for(Tire tire : tires) {
		tire.roll();
	}
}
```

- CarExample 클래스도 수정 가능

```java
public class CarExample {
	public static void mian(String[] args) {
		Car myCar = new Car();
		
		myCar.run();
		
		myCar.tires[0] = new KumhoTire();
		myCar.tires[1] = new KumhoTire();
		
		myCar.run();
	}
}
```

### 8.5.4 매개 변수의 다형성

- 자동 타입 변환은 주로 메소드 호출할 때 많이 발생한다.
- 매개 값을 다양화하기 위해서 상속에서는 매개 변수를 부모 타입으로 선언하고 호출할 때에는 자식 객체를 대입했었다.
- 이번에 매개 변수를 인터페이스 타입으로 선언하고 호출할 때에는 구현 객체를 대입한다.

- Driver 클래스에는 dirve() 메소드가 정의되어 있는데 Vehicle 타입의 매개변수가 선언되어있다.

```java
public class Driver { 
	public void drive(Vehicle vehicle) {
		vehicle.run();
	}
}
```

- Vehicle을 다음과 같이 인터페이스 타입이라고 가정해보자

```java
public interface Vehicle {
	public void run();
}

Driver driver = new Driver();
Bus bus = new Bus();
driver.drive(bus);  //자동타입변환 발생 Vehicle vehicle = bus;
```

- 만약 Bus가 구현 클래스라면 다음과 같이 Driver의 drive() 메소드를 호출할 때 Bus 객체를 생성해서 매개값으로 줄 수 있다.
- drive() 메소드는 Vehicle 타입을 매개 변수로 선언했지만, Vehicle을 구현한 Bus 객체가 매개값으로 사용되면 자동타입변환이 발생한다.
- 매개변수 타입이 인터페이스일 경우 어떠한 구현 객체도 매개값으로 사용할 수 있고 어떤 구현 객체가 제공되느냐에 따라 실행 결과는 다양해질수있다.



```java
void drive(Vehicle vehicle) {  //vehicle 구현객체
	vehicle.run();  //구현 객체의 run() 메소드가 실됨
}
```

### 8.5.3 강제 타입 변환

- 구현 객체가 인터페이스 타입으로 자동변환 하면 인터페이스에 선언된 메소드만 사용가능하다는 제약 사항이 따른다.
- 예를 들어 인터페이스에는 세 개의 메소드가 선언되어 있고 클래스에는 다섯개의 메소드가 선언되어 있다면 인터페이스로 호출 가능한 메소드는 세개 뿐이다.
- 하지만 경우에 따라 구현 클래스에 선언된 필드와 메소드를 사용해야 할 경우도 발생한다.
- 이때 강제 타입 변환을 해서 다시 구현 클래스로 타입 변환한 다음 구현 클래스의 필드와 메소드를 사용할 수 있다.

```java
//Vehicle.java 인터페이스

public interface Vehicle {
	public void run();
}
```

```java
//Bus.java 구현 클래스
public class Bus implements Vehicle {
	@Override
	public void run() {
		System.out.println("버스가 달립니다");
	}
	
	public void checkFare() {
			System.out.println("승차요금을 체크합니다");
	}
}
```

```java
	//vehicleExample.java 강제 타입 변환
	
	public class VehicleExample {
		public static void main(String[] args) {
			Vehicle vehicle = new Bus();
			
			vehicle.run();
			//vehicle.checkFare();(x) Vehicle 인터페이스에는 checkFare()가 없음
			
			Bus bus = (Bus) vehicle; //강제타입변환
			
			bus.run();
			bus.checkFare(); //Bus 클래스에는 checkFare()가 있음
```

### 8.5.6 객체 타입 확인

- 강제 타입 변환은 구현 객체가 인터페이스 타입으로 변환되어 있는 상태에서 가능하다.
- instanceof 연산자는 인터페이스 타입에서도 사용할 수 있다.

```java
//Vehicle 인터페이스타입으로 변환된 객체가 Bus인지 확인
if(vehicle instanceof Bus) {
	Bus bus = (Bus) vehicle;
}
```

- 인터페이스 타입으로 자동 변환된 매개값을 메소드 내에서 다시 구현 클래스 타입으로 변환해야 한다면 반드시 매개 값이 어떤 객체인지 instanceof 연산자로 확인하고 안전하게 강제 타입 변환을 해야한다.

### 8.6 인터페이스 상속

- 인터페이스는 다른 인터페이스를 상속할 수 있다.
- 인터페이스는 클래스와 다르게 다중 상속을 허용한다.
- 다음과 같이 extends 키워드 뒤에 상속할 인터페이스들을 나열할 수 있다.

```java
public interface 하위인터페이스 extends 상위인터페이스1, 상위인터페이스2 {...}

```

- 하위 인터페이스를 구현하는 클래스는 하위 인터페이스의 메소드뿐만 아니라 상위 인터페이스의 모든 추상 메소드에 대한 실체 메소드를 가지고 있어야 한다.
- 그렇기 때문에 구현 클래스로부터 객체를 생성하고 나서 다음과 같이 하위 및 상위 인터페이스 타입으로 변환이 가능하다.

```java
하위인터페이스 변수 = new 구현클래스(...);
상위인터페이스1 변수 = new 구현클래스(...);
상위인터페이스2 변수 = new 구현클래스(...);
```

- 하위 인터페이스로 타입 변환이 되면 상.하위 인터페이스에 선언된 모든 메소드를 사용할 수 있으나, 상위 인터페이스로 타입 변환이되면 상위 인터페이스에 선언된 메소드만 사용 가능하고 하위 인터페이스에 선언된 메소드는 사용할 수 없다.

---

### 8.7 디폴트 메소드와 인터페이스 확장

- 디폴트 메소드는 인터페이스에 선언된 인스턴스 메소드이기 때문에 구현 객체가 있어야 사용할 수 있다.
- 선언은 인터페이스에서 하고, 사용은 구현 객체를 통해 한다는 것이 어색하다.
- 디폴트 메소드는 모든 구현 객체에서 공유하는 기본 메소드처럼 보이지만, 사실은 인터페이스에서 디폴트 메소드를 허용하는 이유가 따로 있다.

### 8.7.1 디폴트 메소드의 필요성

- 인터페이스에서 디폴트 메소드를 허용한 이유는 기존 인터페이스를 확장해서 새로운 기능을 추가하기 위해서이다. 기존 인터페이스의 이름과 추상 메소드의 변경 없이 디폴트 메소드만 추가할 수 있기 때문에 이전에 개발한 구현 클래스를 그대로 사용할 수 있으면서 새롭게 개발하는 클래스는 디폴트 메소드를 활용할 수 있다.
- MyInterface라는 인터페이스와 이에 작성된 추상 메서드를 구현한 MyClassA가 있다. 이후 MyInterface에 새로운 기능을 가진 추상 메소드를 추가 했는데 MyClassA에서 문제가 발생한다. 그 이유는 추상 메소드에 대한 실체 메소드가 MyClassA에서 구현되지 않았기 때문이다. 하지만 MyInterface에 디폴트로 메소드를 선언한다면 MyClassA 클래스에서는 실체 메소드를 작성할 필요가 없어진다.

### 8.7.2 디폴트 메소드가 있는 인터페이스 상속

- 부모 인터페이스에 디폴트 메소드가 정의되어 있을 경우, 자식 인터페이스에서 디폴트 메소드를 활용하는 세가지 방법
    - 디폴트 메소드를 단순히 상속만 받는다.
    - 디폴트 메소드를 재정의(Override)해서 실행 내용을 변경한다.
    - 디폴트 메소드를 추상 메소드로 재선언한다.
- 다음과 같이 추상 메소드와 디폴트 메소드가 선언된 ParentInterface가 있다고 가정해보자.

```java
public interface ParentInterface {
	public void method1();
	public default void method2() { /* 실행문 */ }
}
```

- 다음 ChildInterface1은 ParentInterface를 상속하고 자신의 추상 메소드인 method3()을 선언한다.

```java
public interface ChildInterface1 extends ParentInterface {
 public void method3();
}
```

- 이 경우에는 Childinterface1 인터페이스를 구현하는 클래스는 method1()과 method3()의 실체 메소드를 가지고 있어야 하며 ParentInterface의 method2()를 호출할 수 있다.

```java
ChildInterface1 ci1 = new ChildInterface1() {
@Override
public void method1() { /*실행문*/ }
@Override
public void method3() { /*실행문*/ }
};

ci1.method1();
ci1.method2();
ci1.method3();
```
