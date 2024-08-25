# 예외처리

### 10.1 예외와 예외 클래스

- 자바에서는 예외라고 부르는 오류가 있다. 예외란 사용자의 잘못된 조작 또는 개발자의 잘못된 코딩으로 인해 발생하는프로그램 오류를 말한다.
- 예외가 발생되면 프로그램은 곧바로 종료된다.
- 하지만, 예외 처리를 통해 프로그램을 종료되지 않도록 할 수 있다.

**예외 종류**

- 일반 예외(Exception)
    - 자바 소스를 컴파일하는 과정에서 예외 처리 코드가 필요한지 검사하기 때문에 컴파일러 체크 예외라고도 한다.
    - 만약 예외 처리 코드가 없다면 컴파일 오류가 발생한다.
- 실행 예외(Runtime Exception )
    - 컴파일하는 과정에서 예외처리 코드를 검사하지 않는 예외를 말한다.

- 자바에서는 예외를 클래스로 관리한다.
- JVM은 프로그램을 실행하는 중 예외가 발생하면 해당 예외 클래스로 객체를 생성한다. 이후 예외 처리 코드에서 예외 객체를 이용할 수 있도록 한다.
- 모든 예외 클래스들은 java.lang.Exception 클래스을 상속받는다.

**일반 예외와 실행 예외 클래스 구별 방법**

- 일반 예외는 Exception을 상속 받지만 Runtime Exception은 상속 받지 않는 클래스들이고 실행 예외는 RuntimeException을 상속받는 클래스들이다.
- RuntimException 또한 Exception을 상속받지만, JVM은 RuntimeException을 상속했는지를 보고 구별한다.

---

### 10.2 실행 예외

- 실행 예외는 자바 컴파일러가 체크를 하지 않기 때문에 오로지 개발자의 경험에 의해 예외 처리 코드를 삽입해야한다.
- 개발자가 예외처리 코드를 넣지 않을 경우, 해당 예외가 발생할 경우엔 프로그램이 곧바로 종료되다.

**자바에서 자주 발생되는 실행 예외**

10.2.1 NullPointerException

- 자바 프로그램에서 가장 빈번하게 발생하는 실행 예외이다.
- 이것을 객체 참조가 없는 상태, null 값을 갖는 참조 변수로 객체 접근 연산자인 도트(.)를 사용했을 때 발생한다.
- 즉 객체가 없는 상태에서 객체를 사용하려 하기 때문에 예외가 발생하는 것이다.

```java
public class NullPointerExceptionExample {
	public static void main(String[] args) {
		String data = null;
		System.out.println(data.toString());
	}
}
```

- 위 코드를 실행하면 아래와 같이 Console 뷰에 예외 메시지가 출력되면서 프로그램이 종료된다.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ab7c5a35-a74c-4b21-b9ec-fc4a1a70931b/b2576189-3b02-4a5d-a85e-1f8249fe7b73/image.png)

- 위 예시 사진의 경우 [NullPointerExceptionExample.java](http://NullPointerExceptionExample.java) 소스의 4번째 코드에서 예외가 발생했음을 알 수 있다.

10.2.2 ArrayIndexOutOfBoundsException

- 배열에서 인덱스 범위를 초과하여 사용할 경우 실행 예외인 java.lang.ArrayIndexOutOf-BoundsException이 발생한다.
- 예를 들어 길이가 3인 int[] arr = new int[3] 배열을 선언하면, 배열 항목을 지정하기 위해 arr[0]~arr[2]를 사용할 수 있다. 하지만 arr[3]을 사용하면 인덱스 범위를 초과하기 때문에 ArrayIndexOutOfBoundsException이 발생한다.

10.2.3 NumberFormatException

- 문자열로 되어 있는 데이터를 숫자로 변경하는 경우가 자주 발생한다.
- 문자열을 숫자로 변환하는 방법은 여러 가지가 있지만 가장 많이 사용되는 코드는 다음과 같다.

| 반환 타입 | 메소드명(매개 변수) | 설명 |
| --- | --- | --- |
| int | Integer.parseInt(String s) | 주어진 문자열을 정수로 변환해서 리턴 |
| double | Double.parseDouble(String s) | 주어진 문자열을 실수로 변환해서 리턴 |
- Integer와 Double은 포장 클래스라고 한다.
- 이 클래스의 정적 메소드인 parseXXX() 메소드를 이용하면 문자열을 숫자로 변환할 수 있다.
- 이 메소드들은 매개값인 문자열이 숫자로 변환될 수 있다면 숫자를 리턴하지만, 숫자로 변환될 수 없는 문자가 포함되어 있다면 java.lang.NumberFormatException을 발생시킨다.

10.2.4 ClassCastException

- 타입 변환(Casting)은 상위 클래스와 하위 클래스 간에 발생하고 구현 클래스와 인터페이스 간에도 발생한다.
- 이러한 관계가 아니라면 클래스는 다른 클래스로 타입 변환할수 없다.
- 억지로 타입 변환을 시도할 경우 ClassCastException이 발생한다.

```java
Animal animal = new Dog();
Dog dog = (Dog) animal;

RemoteControl rc = new Television();
Television tc = (Television) rc;
```

- 위 코드의 경우에는 타입 변환에 문제가 없다.

```java
Animal aimal = new Dog();
Cat cat = (Cat) animal;

RemoteControl rc = new Television();
Audio audio = (Audio) rc;
```

- 위의 경우는 대입된 객체가 아닌 다른 클래스 타입으로 타입 변환했기 때문에 ClassCastException이 발생한다.

---

### 10.3 예외 처리 코드

- 프로그램에서 예외가 발생했을 경우 프로그램의 갑작스러운 종료를 막고, 정상 실행을 유지할 수 있도록 처리하는 코드를 예외 처리 코드라고 한다.
- 자바 컴파일러는 소스 파일을 컴파일할 때 일반 예외가 발생할 가능성이 있는 코드를 발견하면 컴파일 오류를 발생시켜 개발자로 하여금 강제적으로 예외 처리 코드를 작성하도록 요구한다.
- 하지만 실행 예외는 컴파일러가 체크해주지 않기 때문에 예외 처리 코드를 개발자의 경험을 바탕으로 작성해야 한다.
- try-catch-finally 블록을 이용하여 예외 처리를 한다.

**try-catch-finally**

- 생성자 내부와 메소드 내부에서 작성되어 일반 예외와 실행 예외가 발생할 경우 예외 처리를 할 수 있도록 해준다.

```java
try {
	//예외 발생 가능 코드
} catch(예외클래스 e) {
	예외 처리
} finally {
	항상 실행;
}
```

- try 블록에는 예외 발생 가능 코드가 위치한다.
- try 블록의 코드가 예외 발생 없이 실행되면 catch 블록의 코드는 실행되지 않고 finally 블록의 코드를 실행한다.
- 만약 try 블록의 코드에서 예외가 발생하면 즉시 실행을 멈추고 catch 블록으로 이동하여 예외 처리 코드를 실행한 뒤 finally 블록의 코드를 실행한다.
- finally 블록은 생략이 가능하다. 예외 발생 여부와 상관없이 항상 실행할 내용이 있을 경우에만 finally 블록을 작성하면 된다.

---

### 10.4 예외 종류에 따른 처리 코드

10.4.1 다중 catch

- try 블록 내부는 다양한 종류의 예외가 발생할 수 있다.
- 이 경우, 발생되는 예외 별로 예외 처리 코드를 다르게 하려면 다중 catch 블록을 작성하면 된다.
- catch 블록의 예외 클래스 타입은 try 블록에서 발생된 예외의 종류를 말하는데, try 블록에서 해당 타입의 예외가 발생하면 catch 블록을 실행하도록 되어있다.

```java
try {
	ArrayIndexOutOfBoundsException 발생
	
	NumberFormatException 발생

} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리1
} catch(NumberFormatException e) {
	예외 처리2
}
```

- catch 블록이 여러 개라도 하나의 catch 블록만 실행된다.
- try 블록에서 동시 다발적으로 예외가 발생하지 않고, 하나의 예외가 발생하면 즉시 실행을 멈추고 해당 catch 블록으로 이동하기 때문이다.

10.4.2 catch 순서

- 다중 catch 블록을 작성할 때 주의 점은 상위 예외 클래스가 하위 예외 클래스보다 아래쪽에 위치해야 한다는 것이다.
- try 블록에서 예외가 발생했을 때, 예외를 처리해줄 catch 블록은 위에서부터 차례대로 검색된다. 만약 상위 예외 클래스의 catch 블록이 위에 있다면, 하위 예외 클래스의 catch 블록은 상위 예외를 상속했기 때문에 실행되지 않는다.

```java
try {
	ArrayIndexOutOfBoundsException 발생
	
	NumberFormatException 발생

} catch(Exception e) {
	예외 처리1
} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리2
}
```

- 위 코드의 상위 예외 클래스가 위에 있기 때문에 예외 처리2는 실행되지 않는다. 따라서 아래와 같이 작성해주어야 한다.

```java
try {
	ArrayIndexOutOfBoundsException 발생
	
	NumberFormatException 발생

} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리1
} catch(Exception e) {
	예외 처리2
}
```

10.4.3 멀티 catch

- 자바 7부터 하나의 catch 블록에서 여러 개의 예외를 처리할 수 있도록 멀티(multi) catch 기능을 추가했다.
- catch 괄호() 안에 동일하게 처리하고 싶은 예외를 | 로 연결하면 된다.

```java
try {
	ArrayIndexOutOfBoundsException 또는 NumberFormatException 발생

} catch(ArrayIndexOutOfBoundsException | NumberFormatException e) {
	예외 처리1
} catch(Exception e) {
	예외 처리2
}
```

## 10.4.2 catch 순서

- 다중 catch 블록을 작성할 때 주의할 점
    - 상위 예외 클래스가 하위 예외 클래스보다 아래쪽에 위치해야한다.
- try  블록에서 예외가 발생했을 때, 예외를 처리해줄 catch 블록은 위에서부터 차례대로 검색된다.
- 만약 상위 예외 클래스의 catch 블록이 위에 있다면 하위 예외 클래스의 catch  블록은 실행되지 않는다.
- 왜냐하면 하위 예외는 상위 예외를 상속했기 때문에 상위 예외 타입도 되기 때문이다.

```java
try {

	ArrayIndexOutOfBoundsException 발생

	NumberFormatException 발생

} catch(Exception e) {
	예외 처리 1
} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리 2
}

// ArrayIndexOutOfBoundsException 과 NumberFormatException 은 모두 Exception을
//상속받기 때문에 첫 번째 catch 블록만 선택되어 실행된다. 두번째는 실행이 안됨

try {

	ArrayIndexOutOfBoundsException 발생

	NumberFormatException 발생

} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리 1
} catch(Exception e) {
	예외 처리 2
}

//try 블록에서 ArrayIndexOutOfBoundsException이 발생하면 첫번째 catch 블록을 실행
//그 밖의 다른 예외 발생시 두 번째 catch 블록 실행
```

## 10.4.3 멀티 catch

- 자바 7부터 하나의 catch 블록에서 여러개의 예외 처리를 할 수 있도록 멀티 catch 기능을 추가했다.
- catch() 괄호 안에 동일하게 처리하고 싶은 예외를 | 로 연결하면 된다.

```java
try {

	ArrayIndexOutOfBoundsException 또는 NumberFormatException 발생
	
	다른 Exception 발생

} catch(ArrayIndexOutOfBoundsException | NumberFormatException  e) {
	예외 처리 1
} catch(Exception e) {
	예외 처리 2
}
```

# 10.5 자동 리소스 닫기

---

- 자바 7에서 추가된 try-with-resources를 사용하면 예외 발생 여부와 상관없이 사용했던 리소스 객체(각종 입출력 스트림, 서버 소켓, 소켓, 각종 채널)의 close() 메소드를 호출해서 안전하게 리소스를 닫아준다
    - 리소스란 여러가지 의미가 있지만 여기서는 데이터를 읽고 쓰는 객체라고 생각

```java
//자바 6이전까지 사용했던 코드
// finally 블록에서 다시 try-catch를 사용해서 close() 메소드를 예외처리해야하므로 복잡

FileInputStream fis = null;
try {
	fis = new FileInputStream("file.txt");
	...
} catch(IOException e) {
...
} finally {
	if(fis != null)
		try {
			fis.close();
		} catch (IOException e) {}
	}
}
```

- try-with-resources를 사용하면 다음과 같아진다.

```java
try(FileInputStream fis = new FileInputStream("file.txt")){
	...
} catch(IOException e) {
	...
}
```

- 어디를 봐도 close()를 명시적으로 호출한 곳이 없다.
- try  블록이 정상적으로 실행을 완료했거나 도중에 예외가 발생하면 자동으로 FileOutputStream의 close() 메소드가 호출된다.
- try {}에서 예외가 발생하면 우선 close()로 리소스를 닫고 catch 블록이 실행한다.

```java
//복수 개의 리소스를 사용할 경우
try(
	FileInputStream fis = new FileInputStream("file.txt");
	FileOutputStream fos = new FileOutputStream("file2.txt");
){
	...
} catch(IOException e) {
	...
}
```

- try-with-resource를 사용하기 위해서 조건이 있다.
- 리소스 객체는 java.lang.AutoCloseable 인터페이스를 구현하고 있어야한다.
- AutoCloseable에는 close() 메소드가 정의되어 있는데 try-with-resources는 이 close() 메소드를 자동 호출한다.
- API 도큐먼트에서 AutoCloseable 인터페이스를 찾아 “All Known Implementing Classes:”를 보면 try-with-resources와 함께 사용할 수 있는 리소스가 어떤 것이 있는지 알 수 있다.

- 직접 AutoCloseable을 구현해서 FileInputStream 클래스를 작성
- TryWithResourceExample 클래스의 main() 메소드에서 try-with-resources를 사용하면 예외가 발생하는 즉시 자동으로 FileInputStream의 close()가 호출되는 것을 볼 수 있다.

```java
//FileInputStream.java 
//AutoCloseable 구현 클래스

public class FileInputStream implements AutoCloseable {
	private String file;
	
	public FileInputStream(String file) {
		this.file = file;
		}
		
		public void read() {
			System.out.println(file + "을 읽습니다.");
		}
		
		@Override
		public void close() throws Exception {
			System.out.println(file + "을 닫습니다.");
		}
	}
```

```java
//TryWithResourceExample.java 
//AutoCloseable 구현 클래스

public class TryWithResourceExample {
	public static void main(String[] args) {
		try (FileInputStream fis = new FileInputStream("file.txt")) {
			fis.read();
			throw new Exception(); //강제적으로 예외 발생시킴
		} cath(Exception e) {
			System.out.println("예외 처리 코드가 실행되었습니다.");
		}
	}
}
```

<aside>
💡 test.txt 을 읽습니다.
test.txt 을 닫습니다.
예외 처리 코드가 실행되었습니다.

</aside>

# 10.6 예외 떠넘기기

---

- 메소드 내부에서 예외가 발생할 수 있는 코드를 작성할 때 try-catch 블록으로 예외를 처리하는 것이 기본이지만 경우에 따라서는 메소드를 호출한 곳으로 예외를 떠넘길 수도 있다.
- 이때 사용하는 키워드가 throws이다.
- throws 키워드는 메소드 선언부 끝에 작성되어 메소드에서 처리하지 않은 예외를 호출한 곳으로 떠넘기는 역할을 한다.
- throw 키워드 뒤에는 떠넘길 예외 클래스를 쉼표로 구분해서 나열해주면 된다.

```java
리턴타입 메소드명(매개변수, ...) throws 예외클래스1, 예외클래스2 ...{
}
```

- 발생할 수 있는 예외의 종류별로 throws 뒤에 나열하는 것이 일반적이지만 다음과 같이 throws Exception만으로 모든 예외를 간단히 떠넘길 수도 있다.

```java
리턴타입 메소드명(매개변수,...) throws Exception {
}
```

- throws 키워드가 붙어있는 메소드는 반드시 try 블록 내에서 호출되어야 한다.
- 그리고 catch  블록에서 떠넘겨 받은 예외를 처리해야 한다.
- 다음코드는 throws 키워드가 있는 method2()를 method1()에서 호출하는 방법을 보여준다.

```java
public void method1() {
	try {
		method2();
	} catch(ClassNotFoundException e) {
		//예외 처리 코드
		System.out.println("클래스가 존재하지 않습니다.");
	}
}

public void method2() throws ClassNotFoundException {
	Class clazz = Class.forName("java.lang.String2");
}
```

- method1() 에서도 try-catch 블록으로 예외를 처리하지 않고 throws 키워드로 다시 예외를 떠넘길 수 있다.
- 그러면 method1()을 호출하는 곳에서 결국 try-catch 블록을 사용해서 예외를 처리해야 한다.

```java
public void method1() throws ClassNotFoundException {
	method2();
}
```

- 자바 API 도큐먼트를 보면 클래스 생성자와 메소드 선언부에 throws 키워드가 붙어있는 것을 흔히 볼 수 있다.
- 이러한 생성자와 메소드를 사용하고 싶다면 반드시 try-catch 블록으로 예외 처리를 해야한다.
- 아니면 throws를 다시 사용해서 예외를 호출한 곳으로 떠넘겨야 한다.
- 그렇지 않으면 컴파일 오류가 발생한다.
- 예를 들어 Class 의 forName() 메소드를 자바 API 도큐먼트에서 보면 다음과 같다.

<aside>
💡 forName

public static Class<?> forName(String className)
throws ClassNotFoundException

</aside>

- forName() 메소드 선언부 뒤에 throws ClassNotFoundException이 붙어 있기 때문에 forName() 메소드를 호출할 때 try-catch 블록으로 예외를 처리하거나, throws로 예외를 떠넘겨야한다.
- 다음 예제에서 Class.forName() 메소드를 사용하는 findClass() 메소드는 예외를 떠넘겼고, findClass()를 호출하는 main() 메소드에서 try-catch 블록을 사용해서 예외 처리를 했다.

```java
//ThrowsExample.java
//예외 처리 떠넘기기

public class ThrowsExample {
	public static void mian(String[] args) {
		try {
			findClass();
		} catch(ClassNotFoundException e) {
			System.out.println("클래스가 존재하지 않습니다.");
		}
	}

	public static void findClass() throws ClassNotFoundException {
		Class clazz = Class.forName("java.lang.String2");
	}
}
```

- main() 메소드에서도 throws 키워드르 사용해서 예외를 떠넘길 수 있는데 결국 JVM이 최종적으로 예외 처리를 하게된다. JVM은 예외의 내용을 콘솔에 출력하는 것으로 예외 처리를 한다.

```java
public static void main(String[] args) throws ClassNotFoundException {
	findClass();
}
```

- main() 메소드에서 throws Exception을 붙이는 것은 좋지 못한 예외 처리 방법이다.
- 프로그램 사용자는 프로그램이 알 수 없는 예외 내용을 출력하고 종료되는 것을 좋아하지 않는다.
- 그렇기 때문에 main()에서 try-catch 블록으로 예외를 최종 처리하는 것이 바람직하다.

# 10.7 사용자 정의 예외와 예외 발생

---

- 프로그램을 개발하다 보면 자바 표준 API에서 제공하는 예외 클래스만으로는 다양한 종류의 예외를 표현 할 수 없다.
- 애플리케이션 서비스와 관련된 예외를 애플리케이션 예외라고 하고 이는 개발자가 직접 정의해서 만들어야 하므로 사용자 정의 예외라고도 한다.

## 10.7.1 사용자 정의 예외 클래스 선언

- 사용자 정의 예외 클래스는 컴파일러가 체크하는 일반 예외로 선언할 수도 있고, 컴파일러가 체크하지 않는 실행 예외로 선언할 수도 있다.
- 일반 예외로 선언할 경우 Exception을 상속하면 되고, 실행 예외로 선언할 경우에는 RuntimeException을 상속하면 된다.

```java
public class XXXException extends [ Exception | RuntimeException [ {
	public XXXException() { }
	public XXXException(String message) { super(message); }
}
```

- 사용자 정의 예외 클래스 이름은 Exception으로 끝나는 것이 좋다.
- 사용자 정의 예외 클래스도 필드, 생성자, 메소드 선언들을 포함할 수 있지만 대부분 생성자 선언만을 포함한다.
- 생성자는 두 개를 선언하는 것이 일반적인데 하나는 매개변수가 없는 기본생성자, 다른 하나는 예외 발생 원인(예외 메시지)을 전달하기 위해 String 타입의 매개 변수를 갖는 생성자이다.
- String 타입의 매개 변수를 갖는 생성자는 상위 클래스의 생성자를 호출하여 예외 메시지를 넘겨준다.
- 예외 메시지의 용도는 catch{} 블록의 예외 처리 코드에서 이용하기 위해서다.

```java
//BalanceInsufficientException.java 사용자 정의 예외 클래스

public class BalanceInsufficientException extends Exception {
	public BalanceInsufficientException() {}
	public BalanceInsufficientException(String message) {
		super(message);
	}
}
```

- BalanceInsufficientException은 Exception을 상속하기 때문에 컴파일러에 의해 체크되는 예외가 된다.
- 그래서 소스 작성시 try-catch 블록으로 예외 처리가 필요하다.

## 10.7.2 예외 발생시키기

- 사용자 정의 예외 또는 자바 표준 예외를 여러분의 코드에서 발생시키는 방법을 알아보자
- 코드에서 예외를 발생시키는 방법은 다음과 같다.

```java
throw new XXXException()
throw new XXXException("메시지");
```

- 예외 객체를 생성할 때는 기본 생성자 또는 예외 메시지를 갖는 생성자 중 어떤 것을 사용해도 된다.
- 만약 catch 블록에서 예외 메시지가 필요하다면 예외 메시지를 갖는 생성자를 이용해야 한다.
- 예외 발생 코드를 가지고 있는 메소드는 내부에서 try-catch 블록으로 예외를 처리할 수 있지만, 대부분은 자신을 호출한 곳에서 예외를 처리하도록 throws 키워드로 예외를 떠넘긴다.

```java
public void method() throws XXXException {
	throw new XXXException("메시지");
}
```

- 그렇기 때문에 throws 키워드를 포함하고 있는 메소드는 호출한 곳에서 다음과 같이 예외 처리를 해주어야한다.

```java
try {
	method();
} catch(XXXExcetpion e) {
	//예외 처리
}
```

- 다음 예제는 은행계좌 클래스를 작성한 것이다.
- 출금(withdraw) 메소드에서 잔고(balance) 필드와 출금액을 비교해서 잔고가 부족하면 BalanceInsufficientException 을 발생시키도록했다.

```java
//Account.java 사용자 정의 예외 발생시키기

public class Account {
	private long balance;
	
	public Account() {}
	
	public long getBalance(){
		return balance;
	}
	public void deposit(int money) {
		balance += money;
	}
	public void withdraw(int money) throws BalanceInsufficientException {
		if(balance < money {
			throw new BalanceInsufficientException("잔고부족:"+(money-balance)+"모자람");
		}
		balance -= money;
	}
}
		
```

# 10.8 예외 정보 얻기

---

- try 블록에서 예외가 발생되면 예외 객체는 catch 블록의 매개 변수에서 참조하게 되므로 매개 변수를 이용하면 예외 객체의 정보를 알 수 있다.
- 모든 예외 객체는 Exception 클래스를 상속하기 때문에 Exception이 가지고 있는 메소드들을 모든 예외 객체에서 호출할 수 있다.
- 그중에서도 가장 많이 사용되는 메소드 getMessage()와 printStackTrace()이다.
- 예외를 발생시킬 때 다음과 같이 String 타입의 메시지를 갖는 생성자를 이용하였다면 메시지는 자동적으로 예외 객체 내부에 저장된다.

```java
throw new XXXException("예외 메시지");
```

- 예외 메시지의 내용에는 왜 예외가 발생했는지에 대한 간단한 설명이 포함된다.
- 좀 더 상세한 원인을 세분화하기 위해 예외 코드를 포함하기도 하는데
- 예를들어 데이터베이스에서 발생한 오류들은 예외 코드가 예외 메시지로 전달된다.
- 이와 같은 예외 메시지는 다음과 같이 catch 블록에서 getMessage() 메소드의 리턴값으로 얻을 수 있다.

```java
} catch(Exception e) {
	String message = e.getMessage();
}
```

- printStackTrace()는 메소드 이름에서도 알 수 있듯이 예외 발생 코드를 추적해서 모두 콘솔에 출력한다.
- 어떤 예외가 어디에서 발생했는지 상세하게 출력해주기 때문에 프로그램을 테스트하면서 오류를 찾을 때 활용된다.

```java
try  {

} catch (예외클래스 e){
	//예외가 가지고 있는 Message 얻기
	String message = e.getMessage();
	
	//예외의 발생 경로를 추적
	e.printStackTrace();
}
```

- AccountExample 클래스는 Account 클래스를 이용해서 예금과 출금을 한다.
- 출금할 때 withdraw() 메소드를 사용하므로 예외 처리가 꼭 필요하다.
- 예외 처리 코드에서 BalanceInsufficientException 객체의 getMessage() 메소드와 printStackTrace() 메소드로 예외에 대한 정보를 얻어내고 있다.

```java
//AccountExample.java  사용자 정의 예외 발생시키기

public class AccountExample  {
	public static void main(String[] args) {
		Account account = new Account();
		//예금하기
		account.deposit(10000);
		System.out.println("예금액:"+account.getBalance());
		//출금하기
		try {
			account.withdraw(30000);
		} catch(BalanceInsufficientException e) { //예외메시지 얻기
			String message = e.getMessage();
			System.out.println(message);
			System.out.println(); //예외 추적후 출력
			e.printStackTrace();
		}
	}
}
```

<aside>
💡 예금액: 10000
잔고부족: 20000 모자람

BalanceInsufficientException : 잔고부족: 20000 모자람
at Account.withdraw(Account.java:16)
at Account.withdraw(Account.AccountExample.java:9)

</aside>

<aside>
💡 예금액: 10000
잔고부족: 20000 모자람

BalanceInsufficientException : 잔고부족: 20000 모자람
at Account.withdraw(Account.java:16)
at Account.withdraw(Account.AccountExample.java:9)

</aside>

- AccountExample 클래스 실행시 콘솔
- “잔고부족: 20000 모자람”은 getMessage()메소드의 리턴값을 출력한 것이다.
- printStackTrace() 메소드에 의해 출력된 내용을 보면 [Account.java](http://Account.java) 16라인에서 최초로 예외가 발생되어 [AccountExample.java](http://AccountExample.java) 9라인 메소드 호출 위치로 예외가 떠넘겨졌음을 알 수 있다.