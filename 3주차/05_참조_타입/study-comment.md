[https://mblogthumb-phinf.pstatic.net/20160417_168/jo759515_14608811219679E1FE_PNG/ĸó.PNG?type=w800](https://mblogthumb-phinf.pstatic.net/20160417_168/jo759515_14608811219679E1FE_PNG/%C4%B8%C3%B3.PNG?type=w800)

- 변수가 스택 영역에 생성되고 객체는 힙 영역에 생성된다.
- String 클래스 변수인  name과 hobby는 힙 영역의 string 객체 주소 값을 가지고 있다.
- 주소를 통해 객체를 참조한다는 뜻에서 string 클래스 변수를 참조 타입 변수라고 한다.

## 메모리 사용 영역

- JVM은 운영체제에서 할당받은 메모리 영역을 다음과 같이 세부 영역으로 구분해서 사용한다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/de4e3c9d-6400-429e-87f8-eceb13c4cb90/ae1ad82b-ce05-4d2c-9b5a-790f8553ae9b/Untitled.png)

https://blog.kakaocdn.net/dn/RXYdG/btquNFyLDwm/2LEFwdS8fUPedHRUdk5Xjk/img.png

## 메소드 영역

- 메소드 영역에는 코드에서 사용되는 클래스들을 클래스 로더로 읽어 클래스별로 런타임 상수풀, 필드 데이터, 메소드 데이터, 메소드 코드, 생성자 코드 등을 분류해서 저장한다.
- 메소드 영역은  JVM이 시작할 때 생성되고 모든 스레드가 공유하는 영역이다.

## 힙 영역

- 객체와 배열이 생성되는 영역이다.
- 힙 영역에 생성된 객체와 배열은 JVM 스택  영역의 변수나 다른 객체의 필드에서 참조한다.
- 참조하는 변수나 필드가 없다면 의미 없는 객체가 되기 때문에 이것을 쓰레기 취급하고 JVM은 쓰레기 수집기를 실행시켜 쓰레기 객체를 힙 영역에서 자동으로 제거한다.

## JVM 스택 영역

- JVM 스택 영역은 각 스레드마다 하나씩 존재하며 스레드가 시작 될 때 할당된다.
- 자바 프로그램에서 추가적으로 스레드를 생성하지 않았다면 main 스레드만 존재함으로 JVM 스택도 하나이다.
- JVM 스택은 메소드를 호출할 때마다 프레임을 추가하고 메소드가 종료되면 해당 프레임을 제거하는 동작을 수행한다.
- 예외 발생 시 printStackTrace() 메소드로 보여주는 Stack Trace의 각 라인은 하나의 프레임을 표현한다.
- printStackTrace() 메소드는 예외 처리에서 설명한다.
- 프레임 내부에는 로컬 변수 스택이 있는데 기본 타입 변수와 참조 타입 변수가 추가 되거나 제거된다.
- 변수가 이 영역에 생성되는 시점은 초기화가 될 때 즉, 최초로 변수에 값이 저장될 때이다.
- 변수는 선언된 블록 안에서만 스택에 존재하고 블록을 벗어나면 스택에서 제거된다.

# 참조 변수의 ==, ≠ 연산

---

- 참조 타입 변수들 간의 == ≠ 연산은 동일한 객체를 참조하는지 다른 객체를 참조하는지 알아 볼 때 사용한다.
- 참조 타입의 변수 값은 힙 영역의 객체 주소이므로 결국 주소 값을 비교하는 것이 된다.
    - 동일한 주소 값을 가지고 있다 = 동일한 객체를 가지고 있다.
- ==,≠연산자를 객체로 비교하는 코드는 if문에서 많이 사용된다.

```java
 if (refVar2 == refVar3 ) {...}
```

# null과 NullPointException

---

- 참조 타입 변수는 힙 영역의 객체를 참조하지 않는다는 뜻으로 null을 가질 수 있다.
- null 값도 초기값으로 사용할 수 있기 때문에 null로 초기화된 참조 변수는 스택 영역에 생성된다.

- 참조타입 변수가 null 값을 가지는지 확인하려면 다음과 같이 ==,≠ 연산을 수행하면 된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/de4e3c9d-6400-429e-87f8-eceb13c4cb90/540631ea-fcbe-44e0-b5c7-82b69afddc3b/Untitled.png)

https://velog.velcdn.com/images/y55nms/post/f7937e41-ff84-477e-9fa4-69aa85a4bc2e/image.png

```java
var1 == null 결과:false
var1 != null 결과: true

var2 == null 결과:true
var2 != null 결과:false
```

- 참조 변수를 사용하면서 가장 많이 발생하는 예외 중 하나는 NullPointerException이 있다.
- 참조 타입 변수를 잘못 사용하면 발생한다.
- 참조 타입 변수가 null을 가지고 있을 경우 참조 타입 변수는 사용할 수 없다.
- 참조 타입 변수를 사용하는 것은 곧 객체를 사용하는 것을 의미하는데 참조할 객체가 없으므로 사용할 수 없는 것이다.

```java
int[] intArray = null;
intArray[0] = 10;  //NullPointException

//int Array 변수가 참조하는 배열 객체가 없기 때문에 

String str = null;
System.out.println ("총 문자수: " + str.length()); //NullPointException

// 참조하는 String 객체가 없기 때문이다.
```

# String 타입

---

```java
String name;
name = "신용권";

String hobby = "자바";
```

- 문자열은 String 객체로 생성되고 변수는 String 객체를 참조한다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/de4e3c9d-6400-429e-87f8-eceb13c4cb90/c26c86ee-97a3-4209-99cc-74235ccf129a/Untitled.png)

[https://mblogthumb-phinf.pstatic.net/20160417_168/jo759515_14608811219679E1FE_PNG/ĸó.PNG?type=w800](https://mblogthumb-phinf.pstatic.net/20160417_168/jo759515_14608811219679E1FE_PNG/%C4%B8%C3%B3.PNG?type=w800)

- name 변수와 hobby 변수는 스택 영역에 생성되고 문자열 리터럴인 참남자와 컴퓨터는 힙 영역에 String 객체로 생성된다. 그리고 name 변수와 hobby 변수에는 String 객체의 주소 값이 저장된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/de4e3c9d-6400-429e-87f8-eceb13c4cb90/daa296d2-d18e-4121-8572-782bad4f85da/Untitled.png)

https://blog.kakaocdn.net/dn/lBndH/btrqHTVdRHr/22HxDweiHk9RG3347KUhY0/img.png

- 자바는 문자열 리터럴이 동일하다면 String 객체를 공유하도록 되어있으 동일한 문자열 리터럴인 “KIM”을 참조할 경우  name1과 name2는 동일한 String 객체를 참조하게 된다.

- 일반적으로 변수에 문자열을 저장할 경우에는 문자열 리터럴을 사용하지만 new 연산자를 사용해서 직접 String 객체를 생성시킬 수도 있다.
- new 연산자는 힙영역에 새로운 객체를 만들 때 사용하는 연산자로 객체 생성 연산자라고한다.



```java
String name = new String("신용권");
String name = new String("신용권"); 
```

- 이경우 name1과 name2는 서로 다른 String 객체를 참조한다.
- 문자열 리터럴로 생성하느냐에 따라 비교 연산자의 결과가 달라질 수 있다.
- 이러한 문자열 리터럴로 String 객체를 생성했을 경우 == 연산의 결과는 true가 나오지만 new 연산자로 String 객체를 생성했을 경우 == 연산의 결과는 false가 나온다.
- 동일한 String 객체이건 다른 객체이건 상관없이 문자열만을 비교할 때에는 String 객체의 equals()메소드를 사용해야한다.

# 배열 타입

---

## 배열이란?

- 같은 타입의 많은양의 데이터를 다루는 방법이 배열이다.
- 배열은 같은 타입의 데이터를 연속된 공간에 나열시키고 각 데이터에 인덱스를 부여해 놓은 자료구조이다.



```java
score[인덱스]
int sum = 0;
for (int i=0; i<30; i++) {
	sum += score[i];
}
int avg = sum / 30
```

- 이렇게 하면  for 문이 30번 반복 실행되면서 많은 양의 데이터를 적은 코드로 손쉽게 처리할 수 있다.
- 배열은 같은 타입의 데이터만 저장할 수 있고 선언과 동시에 저장할 수 있는 데이터 타입이 결정된다.
    - 다른 타입의 값을 저장하려고 하면 타입 불일치 컴파일 오류가 난다.
- 한 번 생성된 배열은 길이를 늘리거나 줄일 수 없다.



## 배열 선언

- 배열의 선언은 두 가지가 있다.

```java
//1
타입[] 변수;

int[] intArray;
double[] doubleArray;
String[] strArray;

//2
타입 변수 [];

int intArray;
double doubleArray[];
String strArray[];
```

- 배열 변수는 참조 변수에 속한다.
- 배열도 객체이므로 힙영역에 생성되고 배열 변수는 힙 영역의 객체를 참조하게 된다 참조할 배열 객체가 없다면 배열 변수는 null 값으로 초기화될 수있다.(하지만 NullPointerException)

## 값 목록으로 배열 생성

```java
데이터타입[] 변수 = {값0, 값1, 값2, 값3 ... };
```

스택                          |            힙

변수                                변수[0]  변수[1]   변수[2]   변수[3]

5번지      —참조→           값0         값1          값2          값3

                                     5번지

- {} 중괄호는 주어진 값들을 항목으로 가지는 배열 객체를 힙에 생성하고 배열 객체의 번지를 리턴한다.

```java
String[] names = {"신용권", "홍길동", "감자바"};

name[1] = "홍삼원"
```

- 배열 변수를 이미 선언한 후에 다른 실행문에서 중괄호를 사용한 배열 생성은 허용되지 않는다.
- 배열 변수를 선언 후, 값 목록들이 나중에 결정되는 상황이라면 new 연산자를 사용해서 값 목록을 지정해주면 된다.

```java
String[] names = null;
names = new String[] {"신용권", "홍길동", "감자바"};
```

- 메소드의 매개값이 배열일 경우도 마찬가지다.

```java
int add(int[] scores) {...}

int result = add( {95, 85, 90}); //컴파일 에러
int result = add( new int[] {95, 85, 90} );
```

## new 연산자로 배열 생성

- 값의 목록을 가지고 있지 않지만 향후 값들을 저장할 배열을 미리 만들고 싶다면 new 연산자로 다음과 같이 배열 객체를 생성시킬 수 있다.

```java
타입[] 변수 = new 타입[길];

타입[] 변수 = null;
변수 = new 타입[길이];

int[] intArray = new int[5] //길이 5인 int[] 배열을 생성한다.
```

- intArray[0]~[4]까지의 값이 저장될 수 있는 공간을 확보하고 배열의 생성 번지를 리턴한다.
- 리턴된 번지는 intArray 변수에 저장된다.
- new 연산자로 배열을 처음 생성할 경우 배열은 자동으로 기본값으로 초기화된다.

```java
int scores = new int[30]  // scores[0]~[29]까지 모두 기본값 0으로 초기화된다.
```

- String 배열을 생성했다면 names[0]~[29]까지 모두 null값으로 초기화된다.

```java
String[] names = new String[30];
```

타입별로 배열의 초기값

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/de4e3c9d-6400-429e-87f8-eceb13c4cb90/6fed3dc4-ce1e-4a4d-a5a8-d15341bc91f7/Untitled.png)

https://velog.velcdn.com/images%2Fmmy789%2Fpost%2F95e9e52f-359e-411e-b2ab-911f590d85cf%2Fimage.png

```java
int[] scores = new int[3];
scores[0] = 83;
scores[1] = 90;
scores[2] = 75;
```

## 배열 길이

- 배열의 길이란 배열에 저장할 수 있는 전체 항목 수를 말한다.

```java
배열변수.length;

int[] intArray = {10, 20, 30};
int num = intArray.length;

//length 필드는 읽기 전용이라 수정이 안됨
 intArray.length = 10; //잘못된 코드
```

- length 필드는 for문을 사용해서 배열 전체를 루핑할 때 유리

```java
public class ArrayLengthExample {
	public static void main(String[] args) {
		int[] socres = {83, 90, 87};
		
		in sum = 0;
		for (int i=0; i<score.length; i++){
...

double avg = (double) sum /scores.length;
```

## 커맨드 라인 입력

- main()메소드의 매개값인 String[] args가 왜 필요할까?

```java
public static void main(String[] args) {...}
```

java 클래스로 프로그램을 실행하면  JVM은 길이가 0인 String 배열을 먼저 생성하고 main() 메소드를 호출할 때 매개값으로 전달한다.

```java
String[] args = {};

public static void main(String[] args)
```

-

## 다차원 배열

- 다차원 배열은 행과 열로 구성된 배열이고 가로 인덱스와 새로 인덱스를 사용한다.

```java
scores.length //2 배열 A의 길이
scores[0].length // 3 배열 B의 길이
scores[1].length //3 배열 C의 길이
```

- scores[0][1]은 배열 B의 인덱스 1 값을 뜻한다.
- socres[1][0]은 배열C의 인덱스 0 값을 뜻한다.

```java
int[][] socres = new int[2][];
socres[0] = new int[2]    oo
scores[1] = new int[3]    ooo
```

- 이런 형태의 배열에서 주의할 점은 정확한 배열의 길이를 알고 인덱스를 사용해야 한다.
- scores[0][2] ArrayIndexOutOfBoundsException을 발생시킨다.

### 객체를 참조하는 배열

- 기본타입 배열은 각 항목에 직접 값을 갖고 있지만 참조 타입 (클래스, 인터페이스) 배열은 각 항목에 객체의 번지를 가지고있다.
- String은 클래스 타입이므로 String[]배열은 각 항목에 문자열이 아니라 String객체의 주소를 가지고 있다. 즉 String 객체를 참조하게 된다.

```java
String[] strArray - new String[3];
strArray[0] = 'Java';
strArray[0] = 'C++';
```

- 위 코드는 배열 변수 strArray를 선언하고  3개의 문자열을 참조하는 배열을 생성하면 다음과 같다.
- String[] 배열의 항목도 결국 String 변수와 동일하게 취급되어야한다.
- String[] 배열 항목 간에 문자열을 비교하기 위해서는 == 연산자 대신 equals() 메소드를 사용해야한다.

### 배열 복사

- 배열은 한 번 생성하면 크기를 변경할 수 없기 때문에 더 많은 저장공간이 필요하다면 보다 큰 배열을 새로 만들고 이전 배열로 부터 복사해야 한다.
- 배열 간의 항목 값들을 복사하려면 for문을 사용하거나 System.arraycopy() 메소드를 사용하면 된다.

```java
public class ArrayCopyByForExample {
	public static void main(String[] args) {
		int[] oldIntArray = { 1, 2, 3};
		int[] newIntArray = new int[5];
		
		
		for(int i=0; i<oldIntArray.length; i++) {
			newIntArray[i] = oldIntArray[i];
		}
		
		for(int i=0; i<newIntArray.length; i++) {
			System.out.print(newIntArray[i] + ", ");
		}
	}
}
```

- 복사되지 않은 항목은 int[] 배열의 기본 초기값 0이 그대로 유지된다. String[] 배열은 null
- System.arraycopy()를 호출하는 방법

```java
System.arraycopy(Object 원본 배열, int 원본 배열에서 복사할 항목의 시작 인덱스, 
Objetc 새 배열, int 새 배열에서 붙여넣을 시작 인덱스, int 복사할 개수);
```

```java
//원본 배열이 arr1이고 새 배열이 arr2일 경우 arr1의 모든 항목을 arr2에 복사하려면

System.arraycopy(arr1, 0, arr2, 0, arr1.length);

```

- 참조 타입 배열일 경우 배열 복사가 되면 복사되는 값이 객체의 번지이므로 새 배열의 항목은 이전 배열의 항목이 참조하는 객체와 동일하다. 이것을 얕은 복사라고 한다. 반대로 깊은 복사는 참조하는 개체도 별도로 생성하는 것을 말한다.

### 향상된 for문

- 자바 5부터 향상된 for문을 제공한다.
- 향상된 for문은 반복 실행을 위해 카운터 변수와 증감식을 사용하지 않는다.
- 배열 및 컬렉션 항목의 개수만큼 반복하고 자동적으로 for문을 빠져나간다.
- for문의 괄호() 에는 배열에서 꺼낸 항목을 저장할 변수 선언과 콜론(:) 그리고 배열을 나란히 작성한다.
    1. 배열에서 가져올 첫 번째 값이 존재하는지 평가한다.
    2. 가져올 값이 존재하면 변수에 저장한다.
    3. 실행문을 실행한다.
    4. 실행문이 모두 실행되면 다시 루프를 돌아 배열에서 가져올 값이 존재하는지 평가한다.
    5. 가져올 다음 항목이 없으면 for문이 종료된다.

```java
public class AdvancedForExample {
	public static void main(String[] args) {
		int[] scores = {95, 71, 84, 93, 87};
		
		int sum = 0;
		for (int score : scores) {
			sum = sum + score;
		}
		System.out.println("점수 총합 = " + sum);
		
		double avg = (double) sum / scores.length;
		System.out.println("점수 평균 = " + avg);
		
		}
	}
```

## 열거타입

- 데이터 중 몇 가지로 한정된 값만을 갖는 데이터 타입이 열거 타입이다.
    - 요일,계절
- 열거 타입은 몇 개의 열거 상수 중에서 하나의 상수를 저장하는 데이터 타입이다.

### 열거 타입 선언

- 열거 타입을 선언하기 위해서는 먼저 열거 타입의 이름을 정하고 열거 타입 이름으로 소스 파일을 생성해야 한다.
- 열거 타입 이름은 관례적으로 첫 문자를 대문자로 하고 나머지는 소문자로 구성한다.

```java
//열거 타입 소스 파일들의 이름
Week.java
MemberGrade.java
ProductKind.java
```

- public enum 키워드는 열거 타입을 선언하기 위한 키워드이고 반드시 소문자로 작성해야한다.
- 열거 타입 이름은 소스 파일명과 대소문자가 모두 일치해야 한다.

```java
public enum 열거타입이름 {...}
```

- 열거 타입을 선언했다면 열거 상수를 선언하면 된다.
- 열거 상수는 열거 타입의 값으로 사용되는데 관례적으로 열거 상수는 모두 대문자로 작성한다.

```java
public enum Week {MONDAY, TUESDAY, WEDNESDAY, TURSDAY, FRIDAY, ...}

//열거 상수가 여러 단어일 경우 (_)
public enum LoginResult {LOGIN_SUCCESS, LOGIN_FAILED}
```

<aside>
💡 열거 타입을 이클립스에서 생성
Package Explorer 뷰에서 프로젝트 선택한 다음 메뉴에서
[File - New - Enum] 을 선택한다.
[Package] 입력란에는 열거 타입이 속할 패키지 명을 입력하고
[Name] 입력란에는 열거 타입 이름인 Week를 입력후 finish 버

</aside>

### 열거 타입 변수

- 열거 타입도 하나의 데이터 타입으로 변수를 선언하고 사용해야한다.

```java
열거타입 변수;

Week today;
Week reservationDay;

//열거 타입 변수를 선언했다면 열거 상수를 저장할 수 있다.
//열거 상수는 단독으로 사용할 수는 없고 반드시 열거타입,열거상수로 사용된다.

열거타입 변수 = 열거타입.열거상수;

//today 열거변수에 열거 상수인 SUNDAY를 저장하면 다음과 같
Week today = Week.SUNDAY;

//열거 타입 변수는 null 값을 저장할 수 있는데 열거타입도 참조타입이기 때문

Week birthday = null;

```

- 참조 타입 변수는 객체를 참조하는 변수
- 열거 상수는 객체로 생성된다.
    - 열거 타입 Week의 경우 MONDAY 부터 SUNDAY까지의 열거 상수는 총 7개의 Week 객체로 생성된다.
    - 그리고 메소드 영역에 생성된 열거 상수가 해당 Week 객체를 각각 참조하게 된다.

```jsx
Week today = Week.SUNDAY;
```

- 열거 타입 변수 today는 스택 영역에 생성된다.
- today에 저장되는 값은 Week.SUNDAY 열거 상수가 참조하는 객체의 번지다.
- 따라서 열거 상수 Week.SUNDAY와 today 변수는 서로 같은 Week 객체를 참조하게 된다.
- today 변수와 Week.SUNDAY 상수의 == 연산 결과는 true가 된다.

### 5.7.3 열거 객체의 메소드

### name() 메소드

- name() ,메소드는 열거 객체가 가지고 있는 문자열을 리턴한다.
- 이때 리턴되는 문자열은 열거 타입을 정의할 때 사용한 상수 이름과 동일하다.

```jsx
Week today = Week.SUNDAY;
String name = today.name();
```

- today가 참조하는 열거 객체에서 name()메소드를 호출하여 문자열을 얻어낸다.
- name() 메소드는 열거 객체 내부의 문자열인 “SUNDAY”를 리턴하고 name 변수에 저장한다.

### ordinal()메소드

- ordinal()메소드는 전체 열거 객체 중 몇 번째 열거 객체인지 알려준다.
- 열거 객체의 순번은 열거 타입을 정의할 때 주어진 순번이다. 0부터 시작

```jsx
Week today = Week.SUNDAY;
int ordinal = today.ordinal();

```

- today가 참조하는 열거 객체가 전체 열거 객체에서 몇 번째 순번인지 알아내는 코드이다.
- ordinal() 메소드는 6을 리턴해서 ordinal 변수에 저장한다.

### compareTo() 메소드

- compareTo() 메소드는 매개값으로 주어진 열거 객체를 기준으로 전후로 몇 번째 위치하는지를 비교한다.
- 만약 열거 객체가 매개값의 열거 객체보다 순번이 빠르다면 음수가, 순번이 늦다면 양수가 리턴한다.

```jsx
Week day1 = Week.MONDAY;
Week day2 = Week.WEDNESDAY;
int result1 = day1.compareT(day2); //-2
int result2 = day2.compareTo(day1) //2
```

- day1과 day2의 상대적 우치를 비교하는 코드이다.
- day1.compareTo(day2)는 day2를기준으로 day1의 상대적 위치를 리턴한다.
- day1(순번0) 이 day2(순번 2)보다 앞에 위치하고 순번차이가 2이므로 result은 음수 -2가 저장된다.
    - 그러나 day2.comparetTto (day1)은 day을 기준으로 day2의 상대적 위치를 리턴한다
    - 따라서 day2가 day1보다 뒤에 위치하고 순번차이가 2이므로 result2는 양수 2가 저장된다.

‘

### valueOf() 메소드

- valueOf()  메소드는 매개값으로 주어지는 문자열과 동일한 문자열을 가지는 열거 객체를 리턴한다.,
- 이 메소드는 외부로부터 문자열을 입력받아 열거 객체로 변한할 때 유용하게 사용할 수 있다.

```jsx
Week weekDaly = Week.valueOf("SATURDAY");
```

- 이코드에서 weekDay  변수는 Week.SATURDAY 열거 객체를 참조하게 된다.

### values()메소드

- values() 메소드는 열거 타입의 모든 열거 객체들을 배열로 만들어 리턴한다.
- 다음은 Week 열거 타입의 모든 열거 객체를 배열로 만들어 향상된 for문을 이용해서 반복하는 코드이다.

Week [] days = Week.values();
for(Week day : days) {
    System.out.println(day);
}