# CHAPTER 5 배열

**배열의 생성**

배열을 선언하는 것은 단지 생성된 배열을 다루기 위한 참조변수를 위한 공간이 만들어진것 뿐

`타입[] 변수이름; //배열을 선언`

배열을 생성해야만 비로소 값을 저장할 수 있는 공간이 만들어진다.

`변수이름 = new 타입[길이]; //배열의 생성`

**배열의 인덱스**

생성된 배열의 각 저장공간을 `배열의 요소` 라고 한다.

`배열이름[인덱스]`의 형식으로 배열의 요소에 접근

**배열의 길이(배열이름.length)**

자바에서 자바 가상 머신(JVM)이 모든 배열의 길이를 별도로 관리

배열은 한번 생성하면 길이를 변경할 수 없다.

배열의 index가 유효한 범위를 벗어났을때 예외 발생 `ArrayIndexOutOfBoundsException`

**배열의 초기화**

`int[] score = new int[5];`

배열 선언

`int[] score; //자동 0으로 초기화` 

생성과 동시에 초기화

`int[] score = new int[] {50, 60, 70, 80, 90};`

`int[] score = {50, 60, 70, 80, 90};`

**배열의 출력**

배열이름으로 바로 출력하면 `‘타입@주소’`의 형식으로 출력된다.

예외적으로 char배열은 println메서드로 출력하면 각 요소가 구분자 없이 그대로 출력된다.

또 Arrays.toString()을 사용하면 배열의 모든 요소를 스트링형(,로 구분자까지 해줌)으로 반환해준다.

**String배열의 선언과 생성**

`String[] name = new String[3];`

각 요소의 값은 null로 초기화

`name[0] = “joe”;`

`name[1] = “woo”;`

`name[2] = “hyeon”;`

**String클래스**

여러 문자, 즉 문자열을 저장할 때 String타입의 변수를 사용했다. 사실 문자열이라는 용어는 ‘문자를 연이어 늘어놓은 것’을 의미하므로 문자배열인 char배열과 같은 뜻이다.

그런데 자바에서는 char배열이 아닌 String클래스를 이용해서 문자열을 처리하는 이유는 String클래스가 char배열에 여러 가지 기능을 추가하여 확장한 것이기 때문이다.

메서드는 객체지향 언어에서 ‘함수’ 대신 사용하는 용어이다. (함수와 같은 뜻)

**char배열과 String클래스의 차이**

String객체(문자열)는 읽을 수만 있을 뿐 내용을 변경할 수 없다.

```java
String str = "Java";
str = str + "8";  //"Java8"이라는 새로운 문자열이 str에 저장된다.
System.out.println(str);  //"Java8"
```

문자열 str의 내용이 변경되는 것 같지만, 문자열은 변경할 수 없으므로 새로운 내용의 문자열이 생성된다.

**String클래스의 주요 메서드**

해당 인덱스의 한 문자 가져오기

`char ch = str.charAt(3);` 

문자열의 일부를 뽑아내기

`String tmp = str.substring(1, 4); //인덱스 1~4의 문자를 반환`

문자열 비교

`str.equals("abc")`

 

**2차원 배열의 선언**

타입[][] 변수이름;

`int[][] score = new int[4][3]; // 4행과 3열의 2차원 배열` 

테이블에서 세로 = 행, 가로 = 열

**2차원 배열의 초기화**

생성과 동시에 초기화

int[][] arr = new int[][] {{1,2,3}, {4,5,6}};

int[][] arr = {{1,2,3}, {4,5,6}};

```java
int[][] score = {
				{100, 100, 100},
        {20, 20, 20},
        {30, 30, 30},
        {40, 40, 40}
};
```

**score.length의 값은 얼마일까?**

배열 참조변수 score가 참조하고 있는 배열의 길이를 뜻한다. 길이는 4이다.

**score[0].length의 값은 얼마일까?**

score[0].length은 배열 참조변수 score[0]이 참조하고 있는 배열의 길이를 뜻한다. 길이는 3이다.

같은 이유로 score[1].length, score[2].length, score[3].length, score[4].length의 값 역시 모두 3이다.

**Arrays로 배열 다루기**

**Arrays.toString()**

일차원 배열을 문자열로 출력

**Arrays.deepToString()**

다차원 배열을 문자열로 출력

**Arrays.equals()**

`Arrays.equals(arr1, arr2);`

두 배열의 모든 요소를 비교

그렇다면 `arr1.equals(arr2);` 이것은?

요소를 비교하는게 아닌 두 배열이 같은 배열(주소값으로 비교)인지 비교

**Arrays.deepEquals()**

다차원 배열의 모든 요소를 비교

**배열의 복사 - copyOf(), copyOfRange()**

copyOf()는 배열 전체를, copyOfRange()는 배열의 일부를 복사해서 새로운 배열을 만들어 반환

copyOfRange()에 지정된 범위의 끝은 포함되지 않는다.

```java
int[] arr = {0,1,2,3,4};
int[] arr2 = Arrays.copyOf(arr, arr.length); // arr2=[0,1,2,3,4]
int[] arr3 = Arrays.copyOf(arr, 3);          // arr2=[0,1,2,3,4]
int[] arr4 = Arrays.copyOf(arr, 7);          // arr2=[0,1,2,3,4,0,0]
int[] arr5 = Arrays.copyOfRange(arr, 2, 4);  // arr2=[2,3] <- 4는 불포함
int[] arr6 = Arrays.copyOfRange(arr, 0, 7);  // arr2=[0,1,2,3,4,0,0]
```

**배열의 정렬 - sort()**

`Arrays.sort(arr);`

