# 4장 조건문과 반복

# 4.1 코드 실행 흐름 제어

---

- 자바 프로그램을 시작하면 main () 메소드의 시작 중괄호 {}까지 위에서부터 아래로 실행하는 흐름을 가지고 있다.
- 실행 흐름을 개발자가 원하는 방향으로 바꿀 수 있도록 해주는 것이 흐름 제어문이다.
    - 흐름 제어문 = 제어문
- 제어문은 조건식과 중괄호 {} 블록으로 구성되는데 조건식의 연산 결과에 따라 블록 내부의 실행 여부가 결정된다.
- 제어문 종류
    - 조건문 : if문 switch문
    - 반복문: for문, while문, do-while문
- 조건문일 경우 제어문 블록이 실행 완료되었을 경우 정상 흐름으로 돌아간다.
- 반복문일 경우 제어문 처음으로 다시 되돌아가 반복 실행한다.
    - = 루핑(looping)이라고 한다.
- 제어문 블록 내부에는 또 다른 제어문을 사용하여 복잡한 흐름 제어도 가능하다.

# 4.2 조건문(if문, switch문)

---

> if문
>

```java
if( 조건식 ) {

	조건식이 true
}
```

- 조건식에는 true 또는 false 값을 산출할 수 있는 연산식이나 boolean 변수가 올 수 있다.
- 조건식이 ture일 경우 블록 실행

> if - else 문
>

- if문 조건식이 true이면 if문 블록 실행, false면 else블록이 실행된다.
- 조건식의 결과에 따라 한 블록의 내용만 실행하고 전체 if문을 벗어난다.

> if - else if else 문
>

- 조건문이 여러 개인 if문일 경우
- 처음 if문의 조건식이 false일 경우 다른 조건식의 결과에 따라 실행 블록을 선택할 수 있다.
- if 블록의 끝에 else if문을 붙이면 된다.
- else if문의 수는 제한이 없고 여러 개의 조건식 중 true가 되는 블록만 실행하고 전체 if문을 벗어나게 된다.
- 모든 조건식이 false일 경우 else 블록을 실행하고 if문을 벗어난다.

> 주사위 숫자 출력하는 프로그램
>
- 임의의 정수를 뽑는 방법
    - Math.random() 메소드
    - 이 메소드는 0.0과 1.0 사이에 속하는 double 난수 하나를 리턴한다. (0.0은 포함 1.0 포함X)
- 1~10 얻기 위해서는

```java
0 < = Math.random()*10 < 1.0 *10
(0.0)                      (10.0)

0+1 < = (int) Math.random()*10 < (int) 10+1
(1)             (1 ~ 10)               (11)
```

- 이원리를 이용하여 start부터 시작하는 n개의 정수 중 임의의 정수 하나를 얻기 위한 연산식

```java
int num = (int) (Math.random() * n) + start; //

//주사위 번호 뽑기

int num = (int) (Math.random() * 6) + 1;

if(num==1){
	 System.out.println("1번이 나왔습니다.");
} else if(num==2) {
	 System.out.println("2번이 나왔습니다.");
}  ...
} else {
	 	System.out.println("6번이 나왔습니다.");
	 }
	}
}
```

> 중첩 if문
>

- if문 블록 내에 또 다른 if문을 사용할 수 있고 if문 뿐만 아니라 switch문, for문, while문, do-while문은 서로 중첩시킬 수 있다.

```java

public class IfNestedExample {
	public static void main (String[] args) {
		int score = (int)(Math.random()*20) +81;
		System.out.println("점수: + score);
		
		String grade;
		
		if(score>=90) {
			if (score>=95) {
				grade = "A+";
			} else {
				grade = "A";
			}
		} else {
			if (score>=85) {
				grade = "B+";
			} else {
				grade = "B";
			}
		}
		
		System.out.println ("학점: " + grade);
		
	}
}
```

> switch 문
>

- switch문 변수가 변수가 어떤 값을 갖느냐에 따라 실행문이 선택된다.
- if문은 조건식의 결과가 true, false 두가지뿐이라 코드가 복잡해지지만 switch문은 변수의 값에 따라 실행문이 결정되기 때문에 if문보다 코드가 간결하다.
- switch문은 괄호 안의 값과 동일한 값을 갖는 case로 가서 실행문을 실행시킨다.
- case안에 동일한 값이 없으면 default로 가서 실행문을 실행시킨다.( default문은 생략 가능)

```java

public class SwitchExample {
	public static void main (String[] args) {
		int num = (int)(Math.random()6) +1;
		
		switch(num) {
		case 1:
			System.out.println("1번이 나왔습니다.");
			break;
		case 2:
			System.out.println("2번이 나왔습니다.");
			break;
			...
			default:
			System.out.println("6번이 나왔습니다.");
			break;
		}
	}
}
```

- case 끝에 break가 붙어 있는 이유는 다음 case를 실행하지 말고 switch 문을 빠져나가기 위함이다.
- break가 없으면 다음 case가 연달아 실행되는데 이때 case 값과는 상관없이 실행된다.

```java
public class SwitchCharExample {
	public static void main (String[] args) {
		
		char grade = 'B';
		
		switch(grade) {
		case 'A':
		case 'a':
			System.out.println("우수 회원입니다.");
			break;
		case 'B':
		case 'b':
			System.out.println("일반 회원입니다.");
			break;
			...
			default:
			System.out.println("손닙입니다.");
			break;
		}
	}
}
```

- siwtch 문의 괄호에는 정수타입(byte, char, short, int, long)변수나 정수값을 산출하는 연산식, 자바7부터는 String 타입의 변수이 올 수 있다.

# 4.3 반복문 (for문, while문, do-while문)

- 반복문 종류
    - for문
    - while문
    - do-while문
- for문과 while문은 서로 변환이 가능하기 때문에 어느 쪽을 사용해도 좋지만, for문은 반복 횟수를 알고 있을 때, while문은 조건에 따라 반복할 때 주로 사용한다.
- while문과 do-while문의 차이점은 조건을 먼저 검사하냐 나중에 검사하냐의 차이고 동작 방식은 동일하다.

> for문
>

- 프로그램을 작성하다 보면 똑같은 실행문을 반복적으로 실행해야 할 경우가 많이 발생한다.
- 반복문은 한 번 작성된 실행문을 여러 번 반복 실행해주기 때문에 코드를 절감하고 간결하게 만들어준다.

- for문이 처음 실행될때 조건식을 평가해서 true면 실행문을 실행시키고 false면 for문 블록을 실행하지 않고 끝나게 된다.
- 블록 내부의 실행문들이 모두 실행되면 증감식을 실행시키고 다시 조건식을 평가하게된다.

```java
int i = 1;
```

- 초기화식의 역할은 조건식과 실행문, 증감식에서 사용할 변수를 초기화하는 역할을 한다.
- 초기화식이 필요없을 경우에는 다음과 같이 초기화식을 생략할 수 있다.

```java
int i = 1;
for (; i<=100; i++) {...}
```

- 어떤 경우에는 초기화식이 둘 이상, 증감식도 둘 이상 있을 수 있다.
- 이런 경우는 쉼표로 구분해서 작성한다.

```java
for (int i = 0, j =100; i<=50 && j>=50; i++, j-) {...}
     ------초기화식----  ----조건식----  -증감식-
```

- 초기화식에 선언된 변수는 for문 블록 내부에서 사용되는 로컬 변수다.
- 따라서 for문을 벗어나면 사용할 수 없다.

```java
public class ForSumFrom1To100Example {
	public static void main (String[] args) {
		int sum = 0;
		
		//int i = 0;
		
		for (int i = 1; i<=100; i++ {
		//for (i = 1; i<=100; i++ {
			sum += i;
		}
		
		System.out.println("1~"+i+ "합: " + sum);
		// i는 for문을 벗어나면 사용할 수 없기 때문에 컴파일 에러가 발생한다.
		
		}
	}
```

- for문을 작성할 때 초기화식에서 루프 카운트 변수를 선언할 때 부동소수점 타입을 사용하지 말아야한다.
- for문은 또 다른 for문을 내포할 수 있는데 이것을 중첩된 for문이라고 한다.
- 바깥쪽 for문이 한 번 실행할 때마다 중첩된 for무은 저장된 횟수만큼 반복해서 돌다가 다시 바깥쪽 for문으로 돌아간다.

```java
public class ForMultiplicationTableExample {
	public static void main (String[] args) {
		for (int m=2; m<=9; m++ {
			System.out.println("*** " + m + "단 ***");
			for (int n =1; n<=9; n++) {
				System out.println(m + "X" + n + " = " + (m*n));
			}
		}
	}
}
```

- 3라인 바깥쪽 for문은 m이 2에서 9까지 변하면서 8번 반복 실행되는데  바깥쪽 for문이 한 번실행할 때 마다 5라인의 중첩 for문은 n이 1~9번 실행한다.

> while문
>

- for문이 정해진 횟수만큼 반복한다면, while은 조건식이 true일 경우 계속해서 반복한다.
- 조건식에는 비교 또는 연산식이 주로 오고 조건식이 false가 되면 반복 행위를 멈추고 while문을 종료한다.
- 조건식 평가 결과가 true이면 실행문 실행 후 다시 조건문으로 돌아가서 다시 조건식을 평가

```java
public class WhilePrintFrom1To10Example {
	public static void main (String[] args) {
		int i = 1;
		while (i<=10) {
			System.out.println(i);
			i++;
		}
	}
}
```

- 조건문 i가 10 이하일 때까지 true가 되므로 while문은 총 10번 반복 실행하게된다.

```java
public class WhileSumFrom1To100Example {
	public static void main (String[] args) {
		
		int sum = 0;   //합계를 저장할 변수를 while 시작 전에 미리 선언해야한다.
		
		int i = 1;
		
		while(i<=100) {
		sum += i;
		i++;
	}
	
	System.out.println("1!" + (i-1)+ "합 " + sum);
	}	
}
```

- 조건식에는 boolean 변수나 true/false 값을 산출하는 어떠한 연산식이든 올 수 있다.
    - 만약 조건식에 true를 사용하면 무한 루프를 돌게 된다.
    - 이 경우 while문을 빠져 나가기 위한 코드가 필요하다.
- 키보드에서 1, 2 입력했을 때 속도를 증속, 감속 시키고 3 입력시 프로그램을 종료한다.

- 먼저 키보드에서 입력된 키가 어떤 키인지 확인하자
- 키보드로부터 입력된 키 코드를 리턴한다.

```java
int keyCode = System.in.read();
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/de4e3c9d-6400-429e-87f8-eceb13c4cb90/10339662-52d3-4438-81d7-f5184b198d4f/Untitled.png)

https://search.pstatic.net/common/?src=http://blogfiles.naver.net/MjAyMTA3MTJfNTIg/MDAxNjI2MDkxNzUzMzA1.AxkxBHV2LuA_WhPeVQ2TJw0R5RW8qUO9GrLYeRyfKE0g.N4Ah3XseD2IWXUJJWuNCCsAYN78R5l6O2yJGCXKKX8Ug.PNG.ekqls9960/18.PNG&type=sc960_832

```java
public class WhileKeyControlExample {
	public static void main (String[] args) thhrows Exeception {
		boolean run = true;
		int speed = 0;
		int keyCode = 0;
	
		while(run) {
			if(keyCode!=13 && keyCode!=10){
			System.out.println("-----------------");
			System.out.println("1.종속 | 2.감속 | 3.중지");
			System.out.println("-----------------");
			System.out.println("선택: ");
			
			keyCode = System.in.read();    //키보드의 키 코드를 읽음
			
			if (keyCode == 49) { //1을 읽었을 경우
				speed++;
				System.out.println("현재 속도=" + speed);
			} else if (keyCode == 50) { //2를 읽었을 경우
				speed--;
				System.out.println("현재 속도=" + speed);
			}else if (keyCode == 51) { //3을 읽었을 경우
				run =false;  // while문을 종료하기 위해 run 변수에 false를 저장
			}
		}
		
		System.out.println ("프로그램 종료");
	}
}
```

- while문을 빠져나가기 위한 또 다른 방법으로는 break문을 이용한다.

(조금 뒤 설명이 나온다고 한다)

> do-while문
>

- while문은 시작할 때부터 조건식을 검사하여 블록 내부를 실행할지 결정하지만 경우에 따라 블록 내부의 실행문을 우선 실행시키고 실행 결과에 따라 반복 실행을 계속할지 결정하는 경우도 있다.
- 이때 do-while문을 사용할 수 있다.
- 작성시 주의할 점!
    - while() 뒤에 반드시 세미콜론(;)을 붙여야한다.
    - do-while문이 처음 실행될 때
        1. 실행문을 우선 실행한다.
        2. 실행문이 모두 실행되면 조건식을 평가하는데
        3. 그 결과가 true이면1→2와 같이 반복 실행
        4. false이면 do-while문을 종료한다.

- 키보드로부터 문자열을 입력받고 출력시키는 예제
- Scanner 객체를 생성하고 nextLine()메소드를 호출하면 콘솔에 입력된 문자열을 한번에 읽을 수 있다.
- nextLine() 메소드로 읽은 문자열을 저장하기 위해 String변수가 필요하다.
-

```java
Scanner scanner = new Scanner(System.in);   //Scanner 객체 생성
String inputString = scanner.nextLine();    //nextLine() 메소드 호출
```

```java
import java.utill.Scanner;    

public class WhileKeyControlExample {
	public static void main (String[] args) {
	System.out.println("메시지를 입력하세요");
		System.out.println("프로그램을 종료하려면 q를 입력하세요");
		
		scanner scanner = new Scanner(System.in);
		String inputString;
		
		do {
			System.out.print(">");
			inputString = scanner.nextLine();   //키보드로 입력한 값을 읽
			System.out.println(inputString);
		} while ( ! inputString.equals("q"));
		
		System.out.print("");
		System.out.print("프로그램 종료");

```

- 처음 한 번 실행 후 조건식이 true일 경우 반복 실행하고
- inputString 변수의 문자열과 q가 같으면 true를 리턴하고 그렇지 않으면 false를 리턴한다.
- 결국 전체 조건식은 inputString에 q가 저장되어 있으면 false가 산출되어 do-while문을 종료한다.

> break문
>
- break문은 반복문인 for문, while문, do-while문을 실행 중지할 때 사용된다.
- switch문, if문 조건식에 따라 for문과 while문을 종료할 때 사용한다.

```java
public class BreakExample {
	publi static void main(String{} args) throws Exception {
		while(true) {
			int num = (int)(Math.random()*6) +1;
			System.out.println(num);
			if(num == 6) {
				break;
			}
		}
		System.out.println("프로그램 종료");
	}
} 
```

- while문을 이용해서 주사위 번호 하나를 반복적으로 뽑되 6이 나오면 while문을 종료시킨다.
- 반복문이 중첩되어 있을 경우 break문은 가장 가까운 반복문만 종료하고 바깥쪽 반복문은 종료시키지 않는다.
- 바깥쪽 반복문까지 종료시키려면 바깥쪽 반복문에 이름을 붙이고 “break 이름;”을 사용하면된다.

> continue문
>

- continue문은 반복문인 for문, while문, do-while문에서만 사용된다.
- 블록 내부에서 continue문이 실행되면 for문의 증감식 또는 while문, do-while문의 조건식으로 이동한다.
- continue문은 반복문을 종료하지 않고 계속 반복을 수행한다는 점이 break문과 다르다.

```java
public class ContinueExample {
	public static void main(String[] args) throws Exception {
		for(int i=1; i<=10; i++ {
			if(i%2 != 0) { //2로 나눈 나머지가 0이 아닐경우, 즉 홀수인 경우
				continue;
			}
			System.out.println(i); //홀수는 실행되지 않는다.
		}
	}
}
```

- 조건을 만족한 경우 continue문을 실행해서 그 이후의 문장을 실행하지 않고 다음 반복으로 넘어간다.