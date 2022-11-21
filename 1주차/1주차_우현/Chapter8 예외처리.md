# CHAPTER 8 예외처리

### 프로그램 오류

**컴파일 에러:** 컴파일 시에 발생하는 에러

**런타임 에러**: 실행 시에 발생하는 에러

**논리적 에러**: 실행은 되지만, 의도와 다르게 동작하는 것

### 컴파일 에러

소스코드를 컴파일 하면 컴파일러가 소스코드(.java)에 대해 오타나 잘못된 구문, 자료형 체크 등의 기본적인 검사를 수행하여 오류가 있는지를 알려준다. 

컴파일러가 알려 준 에러들을 모두 수정해서 컴파일을 성공적으로 마치고 나면, 클래스 파일(.class)이 생성되고, 생성된 클래스 파일을 실행할 수 있다.

자바에서는 실행 시 발생할 수 있는 프로그램 오류를 `에러` 와 `예외` , 두가지로 구분.

**에러:** 프로그램 코드에 의해서 수습될 수 없는 심각한 오류

**예외:** 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

에러는 메모리 부족(OutOfMemoryError)이나 스택오버플로우(StackOverflowError)와 같이 일단 발생하면 복구할 수 없는 심각한 오류, 예외는 발생하더라도 수습될 수 있는 덜 심각한 것.

### 예외 클래스의 계층구도

자바에서는 실행 시 발생할 수 있는 오류를 클래스로 작성하였다.

**Exception과 RuntimeException**

**RuntimeException클래스들**

주로 프로그래머의 실수에 의해서 발생될 수 있는 예외

배열의 범위를 벗어남(ArrayIndexOutOfBoundsException), 값이 null인 참조변수의 멤버를 호출(NullPointerException), 클래스간 잘못된 형변환(ClassCaseException), 정수를 0으로 나누기(ArithmeticException)

**Exception클래스들**

주로 외부의 영향으로 발생, 프로그램의 사용자들의 동작에 의해서 발생.

존재하지 않는 파일의 이름을 입력(FileNotFoundException), 실수로 클래스의 이름을 잘못 적었다(ClassNotFoundException), 입력한 데이터 형식이 잘못됨(DataFormatException)

### 예외 처리하기 - try-catch문

프로그램 실행도중에 발생하는 에러는 어쩔 수 없지만, 예외는 프로그래머가 이에 대한 처리를 미리 해주어야 한다.

예외처리란 프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성하는 것

예외처리를 통해 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지할 수 있다.

발생한 예외를 처리하지 못하면, 프로그램은 비정상적으로 종료되며, 처리되지 못한 예외는 JVM의 ‘예외처리기’가 받아서 예외의 원인을 화면에 출력한다.

```java
try {
...
} catch (Exception1 e1) {
...
} catch (Exception2 e2) {
...
} catch (Exception3 e3) {
...
}
```

**예외의 발생과 catch블럭**

catch의 ()에는 처리하고자 하는 예외타입을 선언.

예외가 발생하면, 발생한 예외에 해당하는 클래스의 인스턴스가 만들어진다.

또 예외발생시 내부적으로 instanceof연산자를 이용해서 검사하는데 결과가 true인 catch 블럭이 나올때까지 검사한다. 모두 검사 후 true인 catch블럭이 하나도 없으면 예외 처리는 되지 않는다.

**printStackTrace()와 getMessage()**

예외가 발생했을 때 생성되는 예외 클래스의 인스턴스에는 발생한 예외에 대한 정보가 담겨있으며, getMessage()와 printStackTrace()를 통해서 이 정보들을 얻을 수 있다.

**printStackTrace()**

예외발생 당시의 호출스택에 있었던 메서드의 정보와 예외 메시지 출력

**getMessage()**

발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있다.

**멀티 catch블럭**

```java
try {
...
} catch (Exception1 | Exception2 e) {
...
}
```

단 `|` 기호로 연결된 예외 클래스가 부모와 자식 관계에 있다면 컴파일 에러 발생

### 예외 발생시키기

키워드 `throw` 를 사용해서 프로그래머가 고의로 예외를 발생시킬 수 있다.

1. 연산자 new를 이용해서 발생시키려는 예외 클래스의 객체를 만든 다음
    
    Exception e = new Exception(”고의로 발생”);
    
2. 키워드 throw를 이용해서 예외를 발생
    
    throw e;
    

```java
try {
	Exception e = new Exception(”고의로 발생”);
	throw e;
} catch (Exception e) {
	e.printStackTrace();
}
```

### chencked예외, unchecked예외

Exception클래스와 그 자식들은 checked예외여서 이에 대한 예외처리를 해주지 않으면 컴파일 조차 되지 않는다.

RuntimeException클래스와 그 자식들은 unckecked예외여서 컴파일이 완료된 이후에 에러가 발생한다.

### 메서드에 예외 선언하기

예외를 처리하는 방법은 try-catch문 외에, 예외를 메서드에 선언하는 방법이 있다.

메서드에 예외를 선언하려면, 메서드의 선언부에 키워드 throws를 사용해서 메서드 내에서 발생할 수 있는 예외를 적어주기만 하면 된다. 그리고 예외가 여러 개일 경우 쉼표(,)로 구분

```java
void method() throws Exception1, Exception2, ... ExceptionN {
	//메서드의 내용
}
```

throw와 throws를 잘구분하자.

### finally블럭

예외의 발생여부에 상관없이 실행되어야할 코드를 포함시킬 목적으로 사용

```java
try {
...
} catch (Exception e) {
...
} finally {
...
}
```

### 사용자 정의 예외 만들기

보통 Exception클래스 또는 RuntimeException클래스로부터 상속받아 클래스를 만든다. 필요에 따라 알맞은 예외 클래스를 선택할 수 있다.

기존의 예외 클래스는 주로 Exception을 상속받아서 ‘checked예외’로 작성하는 경우가 많았지만, 요즘은 예외처리를 선택적으로 할 수 있도록 RuntimeException을 상속받아서 작성한다.

 ‘checked예외’는 반드시 예외처리를 해주어야 한다.

### 예외 되던지기(exception re-throwing)

한 메서드에서 발생할 수 있는 예외가 여럿인 경우, 몇 개는 try-catch문을 통해서 메서드내에서 자체적으로 처리하고, 그 나머지는 선언부에 지정하여 호출한 메서드에서 처리하도록 함으로써, 양쪽에서 나눠서 처리되도록 할 수 있다.

이것은 예외를 처리한 후에 인위적으로 다시 발생시키는 방법을 통해서 가능한데, 이것을 ‘예외 되던지기’ 라고 한다.

### 연결된 예외(chained exception)

한 예외가 다른 예외를 발생시킬 수도 있다.
