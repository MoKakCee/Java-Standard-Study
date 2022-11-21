# Chapter 4 조건문과 반복문

## **if**

```java
if(조건식) {
    // 조건식이 true일 때 수행될 문장들
}
```

### **else 혼용**

```java
if(조건식1){
    //조건식1이 true일 때 수행될 문장들
}else if(조건식2){
    //조건식2가 true일 때 수행될 문장들
}else if(조건식3){
    //조건식3이 true일 때 수행될 문장들
}else{
    //위의 모든 조건식들이 false일 때 수행될 문장들
}
```

- 위에서부터 순서대로 조건을 검사하다 참인 조건식을 만나면, 해당 블럭`{}`만 수행하고, 전체 `if-else`문을 빠져나온다.

## **switch**

```java
// 하나의 조건식으로 여러 경우의 수를 처리할 수 있고, if문에 비해 처리시간이 더 짧다.
switch(조건식){
    case 값1:
        //조건식의 결과가 값1과 일치할 경우 수행될 문장들
        break;
    case 값2:
        //조건식의 결과가 값2와 일치할 경우 수행될 문장들
        break;
    default:
        //조건식의 결과와 일치하는 case문이 없을 때 수행될 문장들
}
```

- break 문이 없으면 참이 된 case부터 모든 case를 모두 수행한다.

## **향상된 switch - case**

JVM 13부터 기존 `switch - case` 의 문제점을 해결하기 위해 몇가지 개선점이 추가된 `switch - case` 를 사용할 수 있게 되었다.

- 다중값을 가진 `case`
- 반환값을 위한 `yield`
- 화살표 연산자(`→` )
- 코드 블럭

```java
//이전 방식
switch(score){
	case 10 :
	case 9 :
	case 8 :
		System.out.println("A");
		break;
	case 7 :
	case 6 :
	case 5 :
		System.out.println("B");
		break;
	default :
		System.out.println("C");
}

//JVM 13
switch(score){
	case 10, 9, 8 :
		System.out.println("A");
		break;
	case 7, 6, 5 :
		System.out.println("B");
		break;
	default :
		System.out.println("C");
}
```

### **yield**

`switch` 문 내에 사용하여 `switch` 문의 반환값을 갖게 합니다. 따라서 `switch` 문을 표현식으로 사용할 수 있다.

```java
System.out.println(
	switch(score){
		case 10, 9, 8 :
			yield "A";
		case 7, 6, 5 :
			yield "B";
		default :
			yield "C";
	});

String str =
	switch(score){
		case 10, 9, 8 :
			yield "A";
		case 7, 6, 5 :
			yield "B";
		default :
			yield "C";
	}
```

### **코드 블럭**

`case` 내에 코드블럭을 사용할 수 있다.

### **화살표**

화살표 연산자로 `case` 를 표현하여 표현식, 구문, 코드 블럭을 사용한다.

```java
String grade;
switch(score){
	case 10, 9, 8 -> grade = "A";
	case 7, 6, 5 -> grade = "B";
	default -> grade = "C";
}
```

> 참고 [https://docs.oracle.com/en/java/javase/13/language/switch-expressions.html](https://docs.oracle.com/en/java/javase/13/language/switch-expressions.html)
>

### 임의이 정수 만들기 Math.random()

```java
int num=0;
for(int i=0;i<5;i++){
		num=(int)(Math.random()*6)+1; //0~5사이의 랜덤값 +1을 하여 1~6사이의 랜덤값을 받는다	

}
```

## **for**

```java
for(초기화;조건식;증감식){
    // 조건식이 참일 경우 수행될 문장들
}

// example.
for(int i=0;i<10;i++){
    System.out.print(i+" ");
}
// result.
// 0 1 2 3 4 5 6 7 8 9
```

- 향상된 `for`문
    - JDK 1.5부터 배열과 컬렉션에 저장된 요소에 접근할 때 더 편리한 방법을 사용할 수 있다.
    - for( 타입 레퍼런스 : Iterable 구현체)

```java
for(타입 변수명 : 배열 또는 컬렉션) {
    // 반복할 문장
}

// example.
int[] nums = {1,2,3,4,5};
for (int num : nums){
    System.out.print(num+" ");
}
// result.
// 1 2 3 4 5
```

## **while**

```java
while(조건식){
    // 조건식이 참일 경우 수행될 문장들
}
```

`do-while`문

- `while`문과 반대로 블럭 `{}`을 먼저 수행한 후에 조건식을 평가한다. (최소 한 번은 실행된다.)

```java
do {
    // 조건식이 참일 경우 수행될 문장들
} while (조건식);
```

- `for`문과 `while`문은 서로 변환이 가능하다. 하지만 `for`문과 달리 `while`문의 조건식은 생략할 수 없다.

```java
for( ; ; ){ // 항상 true
    // 수행할 코드
}
while() { // 조건식이 없으므로 에러 발생
    // 수행할 코드
}
```

*cf. `break`문과 `continue`문의 사용법*

- *`break`문은 자신이 포함된 가장 가까운 반복문을 벗어난다.*
- *`continue`문은 아래의 수행문을 더 이상 수행하지 않고 다음 반복으로 넘어간다*

> for문은 반복 횟수를 알고 있을 때 주로 사용하고 while문은 조건에 따라 반복할 때 주로 사용한다
>

## **이름 붙은 반복문**

반복문과 break, continue에 이름을 붙여 하나 이상의 반복문을 벗어날 수 있다.

```java
loop1 :
while(true){
	while(true){
		//isTrue()가 true 이면 상위의 반복문으로 이동하여 반복을 계속 진행
		//해당 루프의 출력 1 과 출력 2 모두 continue 됨
		if(isTrue()) continue loop1;
		System.out.println("출력1");
	}
	System.out.println("출력2");
}
```

## **Iterartor**

Iterator는 Java의 Collection에 저장되어 있는 데이터를 읽어오는 방법을 표준화한 기술 중 하나이다.

**hasNext(), next(), remove()** 메소드를 이용해 데이터를 뽑아와 사용할 수 있다.

```java
Set<String> set = new HashSet<>();
set.add("안녕");
set.add("hello");
set.add("world");

Iterator<String> it = set.iterator();
while(it.hasNext()){
	//요소 출력 후 다음 요소로 이동
	System.out.println(it.next());

	it.remove(); //요소 삭제
}
```