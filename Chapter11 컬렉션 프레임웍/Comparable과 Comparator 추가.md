# 객체 비교를 위한 **Comparable과 Comparator**

[https://st-lab.tistory.com/243](https://st-lab.tistory.com/243) 참고

### **Comparable과 Comparator**

Comparable 인터페이스를 쓰려면 compareTo 메서드를 구현해야하고, Comparator 인터페이스를 쓰려면 compare메서드를 구현해야 한다.

```java
//java.util
public interface Comparator {
	int compare(Object o1, Object o2);  //o1, o2 두 객체를 비교
	boolean equals(Object obj);
}

//java.lang
public interface Comparable {
	int compareTo(Object o);  //주어진 객체(o)를 자신과 비교
}
```

위의 인터페이스가 정렬을 위한 인터페이스라고 하지만 이것은 용도일 뿐이다. 중요한것은 **“객체를 비교할 수 있도록 만든다”**가 핵심이다.

단순 자바에서 제공하는 기본형의 경우 비교연산자를 사용해서 비교하면 끝이지만, 개발자가 만든 객체의 경우 비교 기준이 다를것 이다.

이것때문에 Comparator와 Comparable이 존재한다.

### Comparable

자기 자신과 매개변수 객체를 비교하는 것.

필수 구현 메서드 `compareTo()`를 이용해서 객체를 비교할 기준을 정의할 수 있다.

`객체.compareTo(o); //객체와 o객체를 비교`   

Student객체 비교해보기

**1) Comparable의 compareTo() 오버라이딩**

```java
class Student implements Comparable<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compareTo(Student o) {
		/*
		 * 비교 구현
		 */
	}
}
```

**2) 비교 기준 구현**

```java
class Student implements Comparable<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compareTo(Student o) {
    
		// 자기자신의 age가 o의 age보다 크다면 양수
		if(this.age > o.age) {
			return 1;
		}
		// 자기 자신의 age와 o의 age가 같다면 0
		else if(this.age == o.age) {
			return 0;
		}
		// 자기 자신의 age가 o의 age보다 작다면 음수
		else {
			return -1;
		}
	}
}
```

compareTo메서드는 int값을 반환하도록 되어있다.

즉, 쉽게 말해 ‘값’을 비교해서 정수를 반환해야 한다는 뜻이다. 

하지만 꼭 1, 0, -1이 아닌 양수, 0, 음수를 반환해도 된다.

이것을 이용해 코드를 다음과 같이 수정할 수 있다.

**3) 최종 코드**

```java
class Student implements Comparable<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compareTo(Student o) {
 
		/*
		 * 만약 자신의 age가 o의 age보다 크다면 양수가 반환 될 것이고,
		 * 같다면 0을, 작다면 음수를 반환할 것이다.
		 */
		return this.age - o.age;
	}
}
```

### Comparator

두 매개변수 객체를 비교하는 것

필수 구현 메서드 `compare()`를 이용해서 객체를 비교할 기준을 정의할 수 있다.

`객체.compare(o1, o2); //o1과 o2비교`

이 때 객체는 비교와 아무 상관없다.

1) **Comparator의 compare() 오버라이딩**

```java
import java.util.Comparator;	// import 필요
public class ClassName implements Comparator<Student> { 
 
/*
  ...
  code
  ...
 */
 
	// 필수 구현 부분
	@Override
	public int compare(Student o1, Student o2) {
		/*
		 비교 구현
		 */
	}
}
```

**2) 비교 기준 구현**

```java
import java.util.Comparator;	// import 필요
class Student implements Comparator<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compare(Student o1, Student o2) {
    
		// o1의 학급이 o2의 학급보다 크다면 양수
		if(o1.classNumber > o2.classNumber) {
			return 1;
		}
		// o1의 학급이 o2의 학급과 같다면 0
		else if(o1.classNumber == o2.classNumber) {
			return 0;
		}
		// o1의 학급이 o2의 학급보다 작다면 음수
		else {
			return -1;
		}
	}
}
```

두 객체를 비교하는 것이기 때문에 파라미터로 들어오는 o1과 o2를 비교.

Comparable에서 했던것 처럼 수정 가능

**3) 최종 코드**

```java
import java.util.Comparator;	// import 필요
class Student implements Comparator<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	@Override
	public int compare(Student o1, Student o2) {
 
		/*
		 * 만약 o1의 classNumber가 o2의 classNumber보다 크다면 양수가 반환 될 것이고,
		 * 같다면 0을, 작다면 음수를 반환할 것이다.
		 */
		return o1.classNumber - o2.classNumber;
	}
}
```

객체 내부에 비교를 위한 Comparator 상속시 

`객체.compare(o1, o2)` 이런식으로 객체 비교를 진행해야 한다. 이 방법은 o1, o2 비교를 위한 객체를 생성할 수 밖에 없는데 익명클래스를 사용하여 다음과 같이 코드를 수정할 수 있다.

**익명 클래스를 이용한 Comparator 사용**

```java
import java.util.Comparator;
 
public class Test {
	public static void main(String[] args) {
    
		// 익명 객체 구현방법 1
		Comparator<Student> comp1 = new Comparator<Student>() {
			@Override
			public int compare(Student o1, Student o2) {
				return o1.classNumber - o2.classNumber;
			}
		};
	}
 
	// 익명 객체 구현 2
	public static Comparator<Student> comp2 = new Comparator<Student>() {
		@Override
		public int compare(Student o1, Student o2) {
			return o1.classNumber - o2.classNumber;
		}
	};
}
 
 
// 외부에서 익명 객체로 Comparator가 생성되기 때문에 클래스에서 Comparator을 구현 할 필요가 없어진다.
class Student {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
 
}
```

익명 클래스를 통해 여러가지 비교 기준을 정의하여 사용할 수 있다는 장점이 있다.



# Comparable과 Comparator를 이용한 객체 정렬

자바에서의 정렬은 특별한 정의가 되어있지 않는 한 ‘오름차순’을 기준으로 한다.

ex) Arrays.sort(), Collections.sort()

자바에서 어떤 정렬 알고리즘이든 **두 데이터(요소)를 비교하는 방법**을 사용한다.

두 데이터를 빼기해서 음수가 나오면 두 값의 위치를 바꾸지 않고 양수가 나오면 두 값의 위치를 바꾼다.

이러한 방법으로 오름차순 정렬이 진행된다.

정렬 기법중 Counting Sort같은 특수한 경우를 제외한 정렬 알고리즘은 ‘두 데이터(요소)의 비교’를 통해 두 원소를 교환할지 말지를 정하게 된다.

Arrays.sort 메서드에서의 Merge Sort 내부를 보면

Comparator c라는 매개변수를 통해 c.compare를 호출하고 각 두 요소를 비교한다.

또한 Comparator가 아닌 Comparable을 통한 compareTo() 메서드를 활용한 Merge Sort 또한 존재한다.

그동안 Arrays.sort()를 쓸 때 Arrays.sort(array); 이런식으로 배열만 넘겨주었지만 사실은 Comparator로 구현된 객체를 파라미터로 같이 넘겨주어 Arrays.sort(array, comp); 로도 쓸 수 있다는 것이다.

```java
import java.util.Arrays;
import java.util.Comparator;
 
public class Test {
	
	public static void main(String[] args) {
		
		MyInteger[] arr = new MyInteger[10];
		
		// 객체 배열 초기화 (랜덤 값으로) 
		for(int i = 0; i < 10; i++) {
			arr[i] = new MyInteger((int)(Math.random() * 100));
		}
 
		// 정렬 이전
		System.out.print("정렬 전 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
		
		Arrays.sort(arr, comp);		// MyInteger에 대한 Comparator을 구현한 익명객체를 넘겨줌
        
		// 정렬 이후
		System.out.print("정렬 후 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
	}
 
	
	static Comparator<MyInteger> comp = new Comparator<MyInteger>() {
		
		@Override
		public int compare(MyInteger o1, MyInteger o2) {
			return o1.value - o2.value;
		}
	};
}
 
 
class MyInteger {
	int value;
	
	public MyInteger(int value) {
		this.value = value;
	}
	
	
}
```
