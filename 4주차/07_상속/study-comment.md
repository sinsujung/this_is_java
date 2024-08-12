# 상속

### 7.1 상속 개념

- 객체 지향 프로그램에서는 부모 클래스의 멤버를 자식 클래스에게 물려줄 수 있다.
- 부모 클래스를 상위클래스라고 부를 수 있고, 자식 클래스를 하위 클래스, 또는 파생 클래스라고 부른다.
- 상속은 클래스를 재사용하기 때문에 코드의 중복을 줄여준다.
- 상속을 한다고 부모 클래스의 모든 필드와 메소드를 물려받는 것은 아니다.
- 부모 클래스에서 private 접근 제한을 갖는 필드와 메소드는 상속 대상에서 제외된다.
- 상속을 이용하면 클래스의 수정을 최소화시켜 유지 보수 시간을 줄일 수 있다.
    - 예를 들어 클래스 B, C가 클래스 A를 상속할 경우 A의 필드와 메소드를 수정하여 B, C를 수정하지 않아도 된다.

---

### 7.2 클래스 상속

- 프로그램에서는 자식 클래스가 부모 클래스를 선택한다.
- 자식 클래스 선언 시 어떤 부모 클래스를 상속 받을지 결정하고 선택된 부모 클래스는 아래와 같이 extends 뒤에 기술한다.

```java
class Sports extends Car {
	//필드
	//생성자
	//메소드
}
```

- 자바는 다른 언어들과 다르게 다중 상속을 할 수 없기 때문에 extends 뒤에는 하나의 부모 클래스만 올 수 있다.

```java
public class CellPhone {
	//필드
	String model;
	String color;
	
	//메소드
	void powerOn() { System.out.println("전원을 켭니다."); }
	void powerOff() { System.out.println("전원을 끕니다."); }
	void bell() { System.out.println("벨이 울립니다."); }
	void sendVoice(String message) { System.out.println("자기: " + message); }
	void receiveVoice(String message) { System.out.println("자기: " + message); }
	void hangUp() { System.out.println("전화를 끊습니다."); }
}

```

```java
public class DmbCellPhone extends CellPhone {
	//필드
	int channel;
	
	//생성자
	DmbCellPhone(String model, String color, int channel) {
		this.model = model;
		this.color = color;
		this.channel = channel;
	}
	
	//메소드
	void turnOnDmb() {
		System.out.println("채널 " + channel + "번 DMB 방송 수신을 시작합니다.");
	}
	
	void changeChannelDmb(int channel) {
		this.channel = channel;
		System.out.println("채널 " + channel + "번으로 바꿉니다.");
	}
	
	void turnOffDmb() {
		System.out.println("DMB 방송 수신을 멈춥니다.")
	}
}

```

```java
public class DmbCellPhoneExample {
	public static void main(String[] args) {
		//DmbCellPhone 객체 생성
		DmbCellPhone dmbCellPhone = new DmbCellPhone("자바폰", "검정", 10);
		
		//CellPhone으로부터 상속받은 필드
		System.out.println("모델 " + dmbCellPhone.model);
		System.out.println("색상 " + dmbCellPhone.color);
				
		//DmbCellPhone의 필드
		System.out.println("채널 " + dmbCellPhone.channel);
		
		//CellPhone으로부터 상속받은 메소드 호출
		dmbCellPhone.powerOn();
		dmbCellPhone.bell();
		
		//DmbCellPhone의 메소드 호출
		dmbCellPhone.turnOnDmb();
		dmbCellPhone.changeChannelDmb(12);
		
}
```

---

### 7.3 부모 생성자 호출

- 자식 객체를 생성하면, 부모 객체가 먼저 생성되고 자식 객체가 그 다음에 생성된다.
- 모든 객체는 클래스의 생성자를 호출해야만 생성된다.
- 부모 객체도 예외는 없다. 부모 객체를 생성하기 위해 부모 생성자를 어디서 호출한 것일까?
    - 부모 생성자는 자식 생성자의 맨 첫 줄에서 호출된다.
    - 예를 들어 DmbCellPhone의 생성자가 명시적으로 선언되지 않았다면 컴파일러는 다음과 같은 기본 생성자를 생성한다.

    ```java
    public DmbCellPhone() {
    	super();
    }
    
    ```

    - super()는 부모의 기본 생성자를 호출한다. 즉 CellPhone 클래스의 다음 생성자를 호출한다.

    ```java
    public CellPhone() {
    ...
    }
    
    ```


- 만약 직접 자식 생성자를 선언하고 명시적으로 부모 생성자를 호출하고자 하면 다음과 같이 작성하면 된다.

```java
자식클래스(매개변수선언...) {
	super(매개값, ...);
...
}

```

- super(매개값, …)는 매개값의 타입과 일치하는 부모 생성자를 호출한다.
- 매개값의 타입과 일치하는 부모생성자가 없을 경우 컴파일 오류 발생
- 부모 클래스에 기본 생성자가 없고 매개 변수가 이쓴 생성자만 있다면 자식 생성자에서는 반드시 부모 생성자 호출을 위해 super(매개값, …)를 명시적으로 호출해야 한다.(super(매개값, …)의 위치는 반드시 자식 생성자 첫 줄에 위치해야함)

---

### 7.4 메소드 재정의

- 부모 클래스의 모든 메소드가 자식 클래스에 맞게 설계되어 있다면 가장 이상적인 상속이지만, 어떤 메소드는 자식 클래스가 사용하기에 적합하지 않을 수도 있다. 이 경우 상속된 일부 메소드는 자식 클래스에서 다시 수정하여 사용해야 함. 이러한 경우를 위해 메소드 오버라이딩(Overriding) 기능을 제공

### 7.4.1 메소드 재정의(@Override)

- 메소드 오버라이딩은 상속된 메소드의 내용이 자식  클래스에 맞지 않을 경우, 자식 클래스에서 동일한 메소드를 재정의하는 것을 말한다.
- 메소드가 오버라이딩되면 부모 객체의 메소드는 숨겨지기 때문에, 자식 객체에서 메소드를 호출하면 오버라이딩된 자식 메소드가 호출된다.

`메소드 오버라이딩 규칙`

1. 부모의 메소드와 동일한 시그너처(리턴 타입, 메소드 이름, 매개 변수 리스트)를 가져야 한다.
2. 접근 제한을 더 강하게 오버라이딩할 수 없다.
3. 새로운 예외(Exception)를  throws 할 수 없다(예외는 10장에서 학습한다).

- 접근 제한을 더 강하게 오버라이딩할 수 없다는 것은 부모 메소드가 public 접근 제한을 가지고 있을 경우 오버라이딩하는 자식 메소드는 default나 private 접근 제한으로 수정할 수 없다는 뜻이다. (반대는 가능)

### 7.4.2 부모 메소드 호출(super)

- 자식 클래스에서 부모클래스의 메소드를 오버라이딩하면, 부모 클래스의 메소드는 숨겨지고 오버라이딩된 자식 메소드만 사용된다. 그러나 자식 클래스 내부에서 오버라이딩된 부모  클래스의 메소드를 호출해야하는 상황 발생 시 명시적으로 super 키워드를 붙여 부모 메소드를 호출할 수 있다.

```java
super.부모메소드();
```

- Airplane 클래스를 상속해서 SupersonicAirplane 클래스를 만들 었을 때 Airplane의 fly() 메소드는 일반 비행이지만 SupersonicAirplane의 fly()는 초음속 비행 모드와 일반 비행 모드 두 가지로 동작이 가능

```java
public class Airplan {
	public void land() {
		System.out.println("착륙합니다.");
	}
	
	public void fly() {
		System.out.println("일반비행합니다.");
	}
	
	public void takeOff() {
		System.out.println("이륙합니다.");
	}
}
```

```java
public class SupersonicAirplane extends Airplane {
	public static final int NORMAL = 1;
	public static final int SUPERSONIC = 2;
	
	public int flyMode = NORMAL;
	
	@Override
	public void fly() {
		if(flyMode == SUPERSONIC) {
			System.out.println("초음속 비행합니다.");
		} else {
			super.fly();
		}
}
```

- 2~3라인은 상수 선언, 즉 자주 사용되는 고정값들을 사용하여 가독성을 높임
- fly() 메소드는 오버라이딩되었다. flyMode가 SUPERSONIC 상수값을 가질 경우 “초음속비행” 출력 / 그렇지 않을 경우엔 super.fly() 사용

---

### 7.5 final 클래스와 final 메소드

- final 키워드는 클래스, 필드, 메소드 선언 시에 사용할 수 있다.
- final 키워드는 해당 선언이 최종 상태이고, 결코 수정될 수 없다.

### 7.5.1 상속할 수 없는 final 클래스

- 클래스 선언 시 final 키워드를 class 앞에 붙이면 이 클래스는 최종적인 클래스이므로 상속할 수 없는 클래스가 된다.
- final 클래스의 대표적인 예는 자바 표준 API인 String 클래스이다.

```java
public final class String {..}
```

- 따라서 아래와 같이 자식 클래스를 만들 수 없다.

```java
public class NewString extend String {..}
```

### 7.5.2 오버라이딩할 수 없는 final 메소드

- 메소드 선언 시 final 키워드를 붙이면 이 메소드는 최종적인 메소드이기 때문에 오버라이딩(Overriding)할 수 없는 메소드가 되는 것이다.
- 즉 부모 클래스를 상속해서 자식 클래스를 선언할 때 부모 클래스에 선언된 final 메소드는 자식 클래스에서 재정의가 불가능하다.

---

### 7.6 protected 접근 제한자

- 접근 제한자는 public, protected, default, private와 같이 네 가지 종류가 있다.

| 접근 제한 | 적용할 내용 | 접근할 수 없는 클래스 |
| --- | --- | --- |
| public | 클래스, 필드, 생성자, 메소드 | 없음 |
| protected | 필드, 생성자, 메소드 | 자식 클래스가 아닌 다른 패키지에 소속된 클래스 |
| default | 클래스, 필드, 생성자, 메소드 | 다른 패키지에 소속된 클래스 |
| private | 필드, 생성자, 메소드 | 모든 외부 클래스 |

---

### 7.7 타입 변환과 다형성

- 다형성은 같은 타입이지만 실행 결과가 다양한 객체를 이용할 수 있는 성질을 말한다.
- 코드 측면에서 보면 다형성은 하나의 타입에 여러 객체를 대입함으로써 다양한 기능을 이용할 수 있도록 해준다.
- 다형성을 위해 자바는 부모 클래스로 타입 변환을 허용한다. 즉, 부모 타입에 모든 자식 객체가 대입될 수 있다.
- 이것을 이용하면 객체는 부품화가 가능하다. 예를 들어 자동차를 설계할 때 타이어 클래스 타입을 적용했다면 이 클래스를 상속한 실제 타이어들은 어떤 것이든 상관 없이 대입이 가능하다.

```java
public class Car {
	Tire t1 = new HankookTire();
	Tire t2 = new KumhoTire();
}

```

- 타입 변환이란 데이터 타입을 다른 데이터 타입으로 변환하는 행위를 말한다.
- 클래스 타입의 변환은 상속 관계에 있는 클래스 사이에서 발생한다.
- 자식 타입은 부모 타입으로 자동 타입 변환이 가능하다.

### 7.7.1 자동 타입 변환(Promotion)

- 프로그램 실행 도중에 자동적으로 타입 변환이 일어나는 것
- 자식은 부모의 특징과 기능을 상속받기 때문에 부모와 동일하게 취급될 수 있다. 예를 들어 고양이는 동물의 특징과 기능을 상속받았다. 따라서 “고양이는 동물이다.”가 성립 한다.
- Animal과 Cat 클래스가 다음과 같이 상속 관계에 있다고 보자

```java
class Animal {
	...
}
```

```java
class Cat extends Animal {
	...
}
```

- Cat 클래스로부터 Cat 객체를 생성하고 이것을 Animal 변수에 대입하면 자동 타입 변환이 일어난다.

```java
Cat cat = new Cat();
Animal animal = cat;
```

고생했다 수딱지

# 7.7.2 필드의 다형성

- 자동 변환 타입이 필요한 이유?
- 그냥 자식 타입으로 사용하면 되는데 부모 타입으로 변환해 사용하는 이유가 뭘까?
- 다형성을 구현하는 기술적인 방법 때문이다.
    - 다형성 = 동일한 타입을 사용하지만 다양한 결과가 나오는 성질
    - 필드의 값을 다양화함으로써 실행 결과가 다르게 나오도록 구현하는데, 필드의 타입은 변함이 없지만 실행 도중에 어떤 객체를 필드에 저장하느냐에 따라 실행 결과가 달라질 수 있다 ( = 필드의 다형성)
- 부모 클래스를 상속하는 자식 클래스는 부모가 가지고 있는 필드와 메소드를 가지고 있으니 사용 방법이 동일할 것이고, 자식 클래스는 부모의 메소드를 오버라이딩(재정의) 해서 메소드의 실행 내용을 변경함으로써 더 우수한 실행 결과가 나오게 할 수 있다.
- 그리고 자식 타입을 부모 타입으로 변환할 수 있다.

```java
class Car {
	//필드
	Tire frontLeftTire = new tire();
	Tire frontRightTire = new tire();
	Tire backLeftTire = new tire();
	Tire backRigtTire = new tire();
	
//메소드
void run() { ... }
```

- Car 클래스는 4개의 Tire 필드를 가지고 있다.
- Car 클래스로부터 Car 객체를 생성하려면 4개의 Tire 필드에 각각 하나씩 Tire 객체가 들어가게 된다.
- 그런데 frontRightTire와 backLeftTire를 HanKookTire와 KumhoTire로 교체하려면

```java
Car myCar = new Car();
myCar.frontRightTire = new HankookTire();
myCar.backLeftTire = new KumhoTire();
myCar.run();
```

- Tire 클래스 타입인 frontRightTire와 backLeftTire는 원래 Tire 객체가 저장되어야 하지만, Tire의 자식 객체가 저장되어도 문제가 없다.
- 왜냐하면 자식 타입은 부모 타입으로 자동 타입변환이 되기 때문이다.
- frontRightTire와 backLeftTire에 Tire 자식 객체가 저장되어도 Car 객체는 Tire클래스에 선언된 필드와 메소드만 사용하므로 문제가 되지 않는다.
- HankookTire와 KumhoTire는 부모인 Tire의 필드와 메소드를 가지고 있기 때문이다.

- Car 객체에 run() 메소드가 있고 run() 메소드는 각 Tire 객체의 roll() 메소드를 다음과 같이 호출한다.

```java
void run() {
	frontLeftTire.roll();
	frontRightTire.roll();
	backLeftTire.roll();
	backRightTire.roll();
}
```

- frontRightTIre와 backLeftTIre를 교체하기 전에는 Tire 객체의 roll() 메소드가 호출되지만 HankookTire와 KumhoTire로 교체된 후에는 HankookTire와 KumhoTire 객체의 roll() 메소드가 호출된다.
- 이와같이 자동 타입 변환을 통해서 Tire 필드값을 교체함으로써 Car의 run() 메소드 수정 없이도 다양한 roll() 메소드의 실행 결과를 얻게된다 ( = 필드의 다형성 )

# 7.7.3 하나의 배열로 객체 관리

- Car 클래스에 4개의 타이어 객체를 4개의 필드로 각각 저장했다.
- 동일한 타입의 값들은 배열로 관리하는 것이 유리한 거처럼 타이어 객체들도 타이어 배열로 관리하는 것이 깔끔하다.

```java
class Car {
	Tire frontLeftTire = new tire("앞왼쪽",6);
	Tire frontRightTire = new tire("앞오른쪽",3);
	Tire backLeftTire = new tire("뒤왼쪽",3);
	Tire backRigtTire = new tire("뒤오른쪽",4);
}

//배열
	
class Car {
	Tire[] tires = {
		new tire("앞왼쪽",6);
	  new tire("앞오른쪽",3);
		new tire("뒤왼쪽",3);
		new tire("뒤오른쪽",4);
	};
}
```

- frontLeftTire는 tires[0], frontRightTire는 tires[1], backLeftTire는 tires[2], backRightTire는 tires[3]과 같이 인덱스로 표현되므로 대입이나 제어문에서 활용하기 쉽다.
- 예를들어 인덱스 1을 이용해서 앞 오른쪽 타이어를 KumhoTire로 교체하기

```java
tires[1] = new KumhoTire("앞오른쪽",13);
```

- tire 배열의 각 항목은 Tire 타입이므로 자식 객체인 KumhoTire를 대입하면 자동 타입 변환이 발생하기 때문에 문제가 없다.
- 배열의 타입은 Tire이지만 실제 저장 항목이 Tire의 자식 객체라면 모두 가능하다.
- 상속 관계에 있는 객체들을 배열로 관리하면 제어문에서 가장 많이 혜택을 본다.
- 전체 타이어의 roll()  메소드를 호출하는 Car 클래스의 run() 메소드는 다음과 같이 for문으로 작성할 수 있다.

```java
int run() {
	System.out.println("[자동차가 달립니다.]");
	for(int i=0; i<tires.length; i++;) {
		if(tires[i].roll()==false) {
			stop();
			return (i+1);
		}
	}
	return 0;
}

```

- 다음은 이전 예제에서 작성한 Car  클래스의 타이어 필드를 배열로 수정한 전체 내용

```java
public class Car {
	//필드
	Tire[] tires = {
		new tire("앞왼쪽",6);
	  new tire("앞오른쪽",3);
		new tire("뒤왼쪽",3);
		new tire("뒤오른쪽",4);
	};
	
	//메소드
	int run() {
		System.out.println("[자동차가 달립니다.]");
		
```

# 7.7.4 매개 변수의 다형성

- 자동 타입 변환은 필드의 값을 대입할 때에도 발생하지만 주로 메소드 호출할 때 많이 발생한다.
- 메소드를 호출할 때에는 매개 변수의 타입과 동일한 매개값을 지정하는 것이 정석이지만 매개값을 다양화하기 위해 매개 변수에 자식 타입 객체를 지정할 수도 있다.
- Driver 클래스에는 drive() 메소드가 정의되어 있는데 Vehicle 타입의 매개 변수가 선언되어있다.

```java
class Driver {
	void drive(Vehicle vehicle) {
		vehicle.run();
	}
}
```

- drive 메소드를 정상적으로 호출한다면 다음과 같다.

```java
Driver drive = new Driver();
Vehicle vehicle = new Vehicle();
dirve.drive(vehicle);
```

- Vehicle의 자식 클래스인 Bus 객체를 drive() 메소드의 매개값으로 넘겨준다면 어떻게 될까?
- drive() 메소드는 Vehicle 타입을 매개변수로 선언했지만, Vehicle을 상속받는 Bus 객체가 매개값으로 사용되면 자동 타입 변환이 발생한다.

```java
Vehicle vehicle = bus;
				//--------자동타입변환
```

- 매개 변수의 타입이 클래스일 경우 해당 클래스의 객체뿐만 아니라 자식 객체까지도 매개값으로 사용할 수 있다.
- 매개값으로 어떤 자식 객체가 제공되느냐에 따라 메소드의 실행 결과는 다양해질 수 있다.
- 자식 개체가 부모의 메소드를 재정의(오버라이딩)했다면 메소드 내부에서 오버라이딩 메소드를 호출함으로써 메소드의 실행 결과는 다양해진다.

```java
           //자식객체				
void dirve(Vehicle vehicle) {
	vehicle();  //자식 개체가 재정의한 run()메소드 실행
}
```

- 예제를 작성해보면서 지금까지 설명했던 내용을 눈으로 확인해보자

```java
//Vehicle 클래스가 다음과 같이 작성되었다고 가정해보자
// Vehicle.java 부모 클래스

public class Vehicle {
	public void run() {
		System.out.println("차량이 달립니다.");
	}
}
```

- Driver 클래스  drive() 메소드에서 Vehicle 타입의 매개값을 받아서 run() 메소드를 호출한다.

```java
//Driver.java 
//Vehicle을 이용하는 클래스

public class Driver {
	public void drive(Vehicle vehicle) {
		vehicle.run();
	}
}
```

- 다음은 Bus 클래스와  Taxi 클래스인데, Vehicle 클래스를 상속받아 run() 메소드를 오버라이딩하고있다.

```java
//Bus.java
//자식클래스

public class Bus extends Vehicle {
	@Override
	public void run() {
		System.out.println("버스가 달립니다.");
	}
}
```

```java
//Taxi.java
//자식 클래스

public class Taxi extends Vehicle {
	@Override
	public void run() {
		System.out.println("택시가 달립니다.");
	}
}
```

- Vehicle,Driver,Bus,Taxi 클래스를 이용해서 실행하는 DriverExample 클래스를 보자

```java
public class DriverExample {
	public static void main(String[] args) {
		Driver driver = new Driver();
		
		Bus bus = new Bus();
		Taxi taxi = new Taxi();
		
		driver.drive(bus);  //자동타입 변환 : Vehicle vehicle = bus;  8라인
		driver.drive(tax);  //자동타입 변환 : Vehicle vehicle = taxi; 9라인
```

- 먼저 Driver 객체와 Bus, Taxi 객체를 생성하고 Driver 객체의 drive() 메소드를 호출할 때 Bus 객체와 Taxi 객체를 제공했다.
- DriverExample 클래스를 실행해보면 8라인의 출력 내용은 Bus 객체의 run() 메소드의 실행 결과, 9라인의 출력 내용은 Taxi 객체의 run() 실행 결과이다.
- 이와 같이 매개값의 자동 타입 변환과 메소드 오버라이딩을 이용해서 매개 변수의 다형성을 구현할 수 있다.

# 7.7.5 강제 타입 변환(Casting)

- 강제 타입변환은 부모타입을 자식 타입으로 변환하는 것을 말한다.
- 모든 부모타입을 자식 클래스 타입으로 강제 변환 할 수 있는 것은 아니다.
- 자식 타입이 부모 타입으로 자동 변환한 후, 다시 자식 타입으로 변환할 때 강제 타입 변환을 사용할 수 있다.

```java
자식 클래스 변수 = (자식 클래스) 부모클래스 타입;
				ㄴ---------------------_______________자식 타입이 부모 타입으로 변환된 상태
```

- 자식 타입이 부모 타입으로 자동 변환하면 부모 타입에 선언된 필드와 메소드만 사용가능하다는 제약 사항이 따른다.
- 만약 자식 타입에 선언된 필드와 메소드를 꼭 사용해야 한다면 강제 타입 변환을 해서 다시 자식 타입으로 변환한 다음 자식 타입의 필드와 메소드를 사용하면 된다.

```java
//부모 클래스
class Parent {
	String field1;
	void method() {...}
	void method() {...}
}	
```

```java
//Class Parents를 상속

class Child extends Parents {
	String field2;
	void method3() {...}
}
```

```java
class ChildExampele {
	public static void main(String[] args) {
		Parent parent = new Child();
		parent.field1 "xxx";
		parent.method1();
		parent.method2();
		parent.field2 = "yyy"; //(불가능)
		parent.mehtod3();      //(불가능)
		
		Child child = (Child) parent;
		child.field2 = "yyy"; //(가능)
		child.method3();      //(가능)
	}
}
```

- field2 필드와 method3() 메소드는 Child 타입에만 선언되어 있으므로 Parent 타입으로 자동 타입 변환하면 사용할 수 없다 field2 필드와 method3() 메소드를 사용하고 싶다면 다시 Child 타입으로 강제 타입 변환을 해야한다.

```java
//Parent.java 부모 클래스

public class Parent {
	public String field1;
	
	public void method1() {
		System.out.println("Parent-method1()");
	}
	
	public void method2() {
		System.out.println("Parent-method2()");
	}
}
```

```java
//Child.java 자식 클래스

public class Child extends Parent {
	public String field2;
	public void method3() {
		System.out.println("Child-method3()");
	}
}
```

```java
//ChildExample.java 강제 타입 변환(캐스팅)

public class ChildExample {
	public static void main(String[] args) {
		Parent.field1 = "data";
		Parent.method1();
		Parent.method2();
		
		/*
		parent.field2 = "data2";  //불가능
		parent.mnethod3();        //불가능
		*/
		
		Child child = (Child) parent;
		child.field2 = "yyy";  //가능
		child.method3();       //가능		
	}
}
```

# 7.7.6 객체 타입 확인(instanceof)

- 강제 타입 변환은 자식 타입이 부모 타입으로 변환되어 있는 상태에서만 가능하기 때문에 다음과 같이 부모 타입의 변수가 부모 객체를 참조할 경우 자식 타입으로 변환할 수 없다.

```java
Parent parent = new Parent();
Child child = (Child) parent; //강제 타입 변환을 할 수 없다.
```

- 그렇다면 부모 변수가 참조하는 객체가 부모 객체인지 자식 객체인지 확인하는 방법은 없을까?
- 어떤 객체가 어떤 클래스의 인스턴스인지 확인하려면 instanceof 연산자를 사용할 수 있다.
- instanceof 연산자의 좌항은 객체가 오고, 우항은 타입이 오는데, 좌항의 객체가 우항의 인스턴스이면 즉 우항의 타입으로 객체가 생성되엇다면 true를 산출하고 그렇지 않으면 false를 산출한다.,

```java
boolean result = 좌항(객체) instanceof 우항(타입)
```

- instanceof 연산자는 매개값의 타입을 조사할 때 주로 사용된다.
- 메소드 내에서 강제 타입 변환이 필요할 경우 반드시 매개값이 어떤 객체인지 instanceof 연산자로 확인하고 안전하게 강제 타입 변환을 해야한다.
- 만약 타입을 확인하지 않고 강제 타입 변환을 시도한다면 ClassCastException 예외가 발생할 수 있다.

# 7.8 추상 클래스

---

## 7.8.1 추상 클래스의 개념

- 추상은 실체간에 공통되는 특성을 추출한 것을 말한다.
- 객체를 직접 생성할 수 있는 클래스를 실체 클래스
- 이 클래스들의 공통적인 특성을 추출해서 선언한 클래스를 추상 클래스
    - 추상 클래스와 실체 클래스는 상속의 관계
- 추상 클래스가 부모, 실체 클래스가 자식으로 구현되어 실체 클래스는 추상 클래스의 모든 특성을 물려받고, 추가적인 특성을 가질 수 있다.
    - 여기서 특성이란 필드와 메소드
    - Bird.class, Insect.class, Fish.class 등의 실체 클래스에서 공통되는 필드와 메소드를 따로 선언한 Animal.class를 만들 수 있다 = 추상 클래스
- 추상 클래스는 실체 클래스의 공통되는 필드와 메소드를 추출해서 만들었기 때문에 객체를 직접 생성해서 사용할 수 없다.
    - 다시말해 추상 클래스는 new  연산자를 사용해서 인스턴스를 생성시키지 못한다

```java
Animal animal = new Animal();  //(x)
```

- 추상 클래스는 새로운 실체 클래스를 만들기 위해 부모 클래스로만 사용된다.
- 코드로 설명하면 추상 클래스는 extends 뒤에만 올 수 잇는 클래스
    - 예를들어 Ant  클래스를 만들기 위한 Animal 클래스는 다음과 같이 사용할수있다.

    ```java
    class Ant extends Animal {...} //(o)
    ```


## 7.8.2 추상 클래스의 용도

- 실체 클래스들의 공통적인 특성 (필드, 메소드)을 뽑아내어 추상 클래스로 만드는 이유는?

1. 첫번째 실체 클래스들의 공통된 필드와 메소드의 이름을 통일할 목적
    1. 실체 클래스를 설계하는 사람이 여러 사람일 경우 실체 클래스마다 필드와 메소드가 제각기 다른 이름을 가질 수 있다.
    2. 동일한 데이터와 기능임에도 불구하고 이름이 다르다보니 객체마다 사용방법이 달라진다.
    3. 이것보다는 Phone 이라는 추상 클래스에 소유자인 owner 필드와 turnOn() 메소드를 선언하고 Telephone과 SmartPhone은 Phone을 상속함으로써 필드와 메소드 이름을 통일시킬 수 있다.
2. 실체 클래스를 작성할 때 시간을 절약
    1. 공통적인 필드와 메소드는 추상 클래스인 Phone에 모두 선언해두고 실체 클래스마다 다른 점만 실체 클래스에 선언하게 되면 실체 클래스를 작성하는데 시간을 절약할 수 있다.

## 7.8.3 추상 클래스 선언

- 추상 클래스를 선언할 때에는 선언에 abstract 키워드를 붙여야한다.
- abstract를 붙이게 되면  new 연산자를 이용해서 객체를 만들지 못하고 상속을 통해 자식 클래스만 만들 수 있다.

```java
public abstract class 클래스 {
	//필드
	//생성자
	//메소드
}
```

- 추상 클래스도 일반 클래스와 마찬가지로 필드 생성자, 메소드 선언을 할 수 있다.
- new 연산자로 직접 생성자를 호출할 수는 없지만 자식 객체가 생성될 때 super(…)을 호출해서 추상 클래스 객체를 생성하므로 추상 클래스도 생성자가 반드시 있어야한다.

```java
//Phone 클래스를 추상 클래스로 선언
//Phone.java 추상 클래스

public abstract class Phone {
	//필드
	public String owner;
	
	//생성자
	public Phone(String owner) {
		this.owner = owner;
	}

	//메소드
	public void turnOn() {
		System.out.println("폰 전원을 켭니다");	
	}
	
	public void turnOff() {
		System.out.println("폰 전원을 끕니다");
	}
}
```

- Phone 추상 클래스를 상속해서 SmartPhone 자식 클래스를 정의한 것이다.
- SmartPhone 클래스의 생성자를 보면 super(owner); 코드로 Phone의 생성자를 호출하고있다.

```java
//SmartPhone.java 실체클래스

public class SmartPhone extends Phone {
	//생성자
	public SmartPhone(String owner) {
		super(owner);
	}
	//메소드
	public void internetSearch() {
		System.out.println("인터넷 검색을 합니다.");
	}
}
```

- 다음 PhoneExample 클래스는 Phone의 생성자를 호출해서 객체를 생성할 수 없음을 보여준다.
- 대신 자식 클래스인 SmartPhone으로 객체를 생성해서 Phone의 메소드인 turnOn(), turnOff() 메솓드를 사용할 수 있음을 보여준다.

```java
//PhoneExample.java 추상클래스

public class PhoneExample {
	public static void main(String[] args) {
		//Phone phone = new Phone();
		
		SmartPhone smartPhone = new SmartPhone("홍길동");
		
		smartPhone.turnOn();           //Phone의 메소드
		smartPhone.internetSearch();
		smartPhone.turnOff();         //Phone의 메소드  
	}
}
```

## 7.8.4 추상 메소드와 오버라이딩

- 추상 클래스는 실체 클래스가 공통적으로 가져야 할 필드와 메소드들을 정의해 놓은 추상적인 클래스이므로 실체 클래스의 멤버(필드,메소드)를 통일화하는데 목적이 있다.
- 모든 실체들이 가지고 있는 메소드의 실행내용이 동일하다면 추상 클래스에 메소드를 작성하는 것이 좋다.
- 하지만 메소드의 선언만 통일화하고 실행 내용은 실체 클래스마다 달라야 하는 경우가 있다.
    - 동물은 소리를 내서 추상 클래스에 sound()메소드 정의
    - 동물은 다양한 소리를 내기 때문에 추상 클래스에 통일적으로 작성할 수 없다.
    - 실체에 작성하도록 하면 sound () 메소드를 잊어버려 작성 안할수도있다.
- 이런 경우 추상 클래스는 추상 메소드를 선언할 수 있다.
- 추상 메소드는 추상 클래스에서만 선언할 수 있는데 메소드의 선언부만 있고 메소드 실행 내용인 중괄호{}가 없는 메소드를 말한다.
- 추상 클래스를 설계할 때, 하위 클래스가 반드시 실행 내용을 채우도록 강요하고 싶은 메소드가 있을 경우 해당 메소드를 추상 메소드로 선언하면 된다.
- 자식 클래스는 반드시 추상 메소드를 재정의(오버라이딩)해서 실행 내용을 작성해야하고 그렇지 않으면 컴파일 에러가 발생

```java
//추상 메소드를 선언하는 방법

[public | protected] abstract 리턴타입 메소드명(매개변수, ...);
```

- 일반 메소드 선언과 차이점은 abstract 키워드가 붙어 있고 메소드 중괄호{}가 없다.

```java
//Animal 클래스를 추상 클래스로 선언하고  sound() 메소드를 추상 메소드로 선언

public abstract class Animal {
	public abstract void sound();
}
```

- Animal 클래스를 상속하는 하위 클래스는 고유한 소리를 내도록 sound() 메소드를 재정의해아한다.

```java
//Animal 클래스를 추상 클래스로 선언하고 sound()  메소드를 추상 메소드로 선언
//Animal.java 추상메소드 선언

public abstract class Animal { //추상클래스
	public String kind;
	
	public void breath() {
		System.out.println("숨을 쉽니다");
	}
	
	punlic abstract void sound();  //추상 메소드
}
```

```java
//Dog 클래스는 추상 클래스인 Animal를 상속하고 추상 메소드인 sound()를 재정의
//Dog.java 추상 메소드 오버라이딩

public class Dog extends Animal {
	public Dog() {
		this.kind = "포유류";
	}
	
	//추상 메소드 정의 부분 없으면 컴파일 에러
	@Override
	public void sound() {
		System.out.println("멍멍");
	}
}
```

- AnimalExample 클래스는 Dog와 Cat 객체를 생성해서 sound() 메소드를 호출했다.
- sound() 메소드를 호출하는 방법 3가지
    1. 일반적으로 Dog와 Cat  변수로 호출
    2. Animal 변수로 타입 변환해서 sound() 메소드를 호출
        1. 자식 타입은 부모 타입으로 자동 타입 변환이 될 수 있고
        2. 메소드가 재정의 되어있을 경우 재정의된 자식 메소드가 호출되는 상속의 특징이 그대로 적용된다.
    3. 부모 타입의 매개 변수에 자식 객체를 대입해서 메소드의 다형성을 적용했다.
        1. 두 번째와 같은 원리로 자식 객체가 부모 타입으로 자동 타입 변환이 되어 재정의된 sound() 메소드가 호출된다.

```java
//AnimalExample.java 실행 클래스

public class AnimalExample {
	public static void main(String[] args) {
		Dog dog = new Dog();
		Cat cat = new Cat();
		dog.sound();
		cat.sound();
		System.out.println("----");
		
		//변수의 자동 타입 변환
		Animal animal = null;
		animal = new Dog();      //자동 타입 변환
		animal.sound();          // 재정의된 메소드 호출
		animal = new Cat();      //자동 타입 변환
		animal.sound();          // 재정의된 메소드 호출
		System.out.println("----");
		
		//메소드의 다형성
		animalSound(new Dog());  //자동 타입 변환
		animalSound(new Cat());  //자동 타입 변환
	}	
	
	public static void animalSound(Animal animal) {
		animal.sound();  //재정의된 메소드 호출                             
	}
}	
