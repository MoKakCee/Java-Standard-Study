# CHAPTER 4 조건문과 반복문

프로그램의 흐름을 바꾸는 역할을 하는 문장들을 `제어문`이라고 한다.

제어문에는 `조건문`과 `반복문`이 있다.

### 조건문:

**if문**

```java
if(조건문) {

}
```

if 블럭안 문장이 한문장이면 중괄호 생략 가능

### if-else문

```java
if (조건식) {
		//true일때
} else {
		//false일때
}
```

 if-else문 특성상 두 개의 블럭{ } 중 하나는 무조건 실행된다.

두 블럭{ }의 내용이 모두 수행되거나, 모두 수행되지 않는 경우는 있을 수 없다.

### if-else if문

```java
if (조건식1) {
		//조건식1일때
} else if (조건식2){
		//조건식2일때
} else if (조건식3){
		//조건식3일때
} else{
		//위 조건이 모두 만족하지 않을때
}
```

### 중첩 if문

```java
if (조건식1) {
		// 조건식1이 true일 때
		if (조건식2) {
		// 조건식1과 조건식2가 모두 true일 때
		} else {
		// 조건식1이 true이고, 조건식2가 false일 때
		}
} else {
		// 조건식1이 false일 때
}
```

### switch문

if문은 조건식의 결과가 참과 거짓, 두 가지 밖에 없기 때문에 경우의 수가 많아질수록 else-if를 계속 추가해야 하므로 조건식이 많아져서 복잡해진다. 또 여러개의 조건식을 계산해야 하므로 처리시간도 오래 걸림.

즉, 경우의 수가 많은 경우 if문 보다 switch문이 적합.

```java
switch (조건식) {
	case 값1 :
					//수행할 로직
					break;  //switch문 탈출
  case 값2 :
					//수행할 로직
					break;
  default :
					//조건식 모두 만족하지 못했을때
}
```

switch 제약조건

1. 조건식은 무조건 정수 또는 문자열
2. case문의 값은 정수 상수(문자 포함), 문자열만 가능, 또 중복 불가능
3. case문의 값에 변수로 불가능

### 임의의 정수만들기 Math.random()

Math.random()은 0.0과 1.0사이의 범위에 속하는 하나의 double값을 반환

만약 1과 3 사이의 정수를 원한다면

`(int) (Math.random() * 3) + 1`

### 반복문:

for문

while문

do-while문

for문과 while문은 구조와 기능이 유사하여 어느 경우에나 서로 변환이 가능하며, **반복 횟수를 알고 있을 때는 for문**을, **그렇지 않을때는 while문**을 사용

### for문

```java
for (초기화; 조건식; 증감식) {
	//조건식이 true일때 수행
}
```

 for문 초기화 (둘 이상의 변수가 필요할 경우 ,를 이용해서 초기화 가능)

```java
for(int i=0, j=0; i<=10; i++) {

}
```

마찬가지로 증감식도 ,를 이용해서 두 문장 이상을 하나로 연결 가능

무한반복

for( ; ; )

### while문

```java
while (조건식) {
		//조건식이 true일때 수행
}
```

### while문을 이용한 숫자의 각 자리의 합 구하기

```java
//각 자리 숫자의 합 구하기
public class Main {
    public static void main(String[] args) throws Exception{

        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();

        int sum = 0;

        while(num != 0) {
            sum += num%10;  //나머지 연산으로 마지막 자리의 숫자 구하고 sum에 더하기
            num /= 10;      //다음 반복문 진행 전에 마지막 숫자 잘라내기
        }

        System.out.println(sum);

    }
}
```

### do-while문

구조상 do-while문은 최소 한번은 수행될 것을 보장한다.

```java
do {
		//조건식 결과가 참일때 수행
} while (조건식);
```

### break문

반복문 탈출을 위한 break문

if문과 함께 사용하여 특정 조건을 만족했을때 반복문을 벗어나게 만들 수 있다.

### continue문

continue문은 반복문 내에서만 사용 가능

반복이 진행되는 도중에 continue문을 만나면 반복문의 끝으로 이동하여 다음 반복으로 넘어간다.

for문의 경우 증감식으로 이동

while문과 do-while문의 경우 조건식으로 이동

if문과 함께 사용되어 특정 조건을 만족하는 경우에 continue문 이후의 문장들을 수행하지 않고 다음 반복으로 넘어가게 만들 수 있다.

### 이름 붙은 반복문

break문은 근접한 단 하나의 반복문만 벗어날 수 있다. 그렇기에 여러 개의 중첩 반복문의 경우 break문으로 중첩 반복문을 완전히 벗어날 수 없다.

이때는 중첩 반복문 앞에 이름을 붙이고 break문과 continue문에 이름을 지정해 주어서 하나 이상의 반복문을 벗어나거나 건너뛸 수 있다.

