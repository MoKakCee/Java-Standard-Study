# Chapter5 배열

## **배열**

> 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것
>
- 배열의 생성

```java
// 자료형[] 배열이름 = new 자료형[배열크기]
// 7칸짜리 정수형 배열
int[] list_1 = new int[7];
// 배열 선언과 동시에 초기화
int[] list_2 = {1,2,3,4,5,6,7};
//문자열 = 배열,
String a = "자바스터디";
String b = new String("자바스터디");
```

### 배열 관련 유용한 메서드

- binarySearch() 메소드 : 전달받은 배열에서 특정 객체의 위치를 이진 검색 알고리즘(선 정렬 후 사용)을 사용하여 검색한 후, 해당 위치를 반환

```java
int[] arr = new int[1000];
for(int i = 0; i < arr.length; i++) {
  arr[i] = i;
}
System.out.println(Arrays.binarySearch(arr, 437));
```

- sort() 메소드: 전달받은 배열의 모든 요소를 오름차순으로 정렬 , Comparator를 사용하여 정렬 순서, 정렬 기준을 정할 수 있음

```java
int[] arr = {5, 3, 4, 1, 2};
Arrays.sort(arr);
for (int i = 0; i < arr.length; i++) {
    System.out.print(arr[i] + " ");
}
```

- copyOf 메소드: 전달받은 배열의 특정 길이만큼을 새로운 배열로 복사하여 반환,
- 새로운 배열의 길이가 원본 배열보다 길면, 나머지 요소는 배열 요소의 타입에 맞게 다음과 같은 기본값으로 체워서 반환

```java
int[] arr1 = {1, 2, 3, 4, 5};
int[] arr2 = Arrays.copyOf(arr1, 3);

for (int i = 0; i < arr2.length; i++) {
    System.out.print(arr2[i] + " ");
}

int[] arr3 = Arrays.copyOf(arr1, 10);

for (int i = 0; i < arr3.length; i++) {
    System.out.print(arr3[i] + " ");
}
```

- asList() 메소드: 배열을 List로 변환

```java
String[] strArr2 = {"aa", "bb", "cc"};
List<String> list2 = new ArrayList<String>(Arrays.asList(strArr2));
list2.set(0, "hi");list2.add("dd");
System.out.println(Arrays.toString(strArr2)); // [aa, bb, cc]
System.out.println(list2.toString()); // [hi, bb, cc, dd]
```

- toString(), deepToString() 메소드: 배열의 element 출력

```java
int[] intStr1 = {1, 2, 3};
System.out.println(Arrays.toString(intStr1)); // [1, 2, 3]
int[][] intStr2 = {{1, 2, 3}, {4, 5, 6}};
System.out.println(Arrays.toString(intStr2)); // [[I@15db9742, [I@6d06d69c]
System.out.println(Arrays.deepToString(intStr2)); // [[1, 2, 3], [4, 5, 6]]
```

- equals(), `deepEquals()` 메소드: 배열 비교

```java
int[] intStr1 = {1, 2, 3};
int[] compStr1 = new int[]{1, 2, 3};
System.out.println(Arrays.equals(intStr1, compStr1)); // true 
int[][] intStr2 = {{1, 2, 3}, {4, 5, 6}};
int[][] compStr2 = new int[][]{{1, 2, 3}, {4, 5, 6}};
System.out.println(Arrays.equals(intStr2, compStr2)); // false
System.out.println(Arrays.deepEquals(intStr2, compStr2)); // ture
```

- fill() 메서드: 배열 채우기

```java
int[] intArr = new int[5];
Arrays.fill(intArr, 1); // 채울 배열, 채울 값 
System.out.println(Arrays.toString(intArr)); // [1, 1, 1, 1, 1]
```

- arr.length: 배열의 길이
- arr.clone(): CopyOf와 같은 결과 제공
- array vs arraylist vs linkedlist 속도비교 : array> arraylist > linkedlist ([https://jerry92k.tistory.com/63](https://jerry92k.tistory.com/63))

## **다차원 배열**

- 배열의 생성

```
1. 타입[][] 배열이름;
2. 타입 배열이름[][];
3. 타입[] 배열이름[];
```

- 가변배열

```
int[][] arr = new int[3][];
arr[0] = new int[2];
arr[1] = new int[4];
arr[2] = new int[1];
```

## **String class**

> String은 참조형 클래스 객체이며, 불변 객체이다
>
- 0 length array:

`public Cheese[] getCheeses() {
if(cheeseInStock.size() == 0)
return null; // return newint[0]`

null값을 처리하지 않아서 발생하는 오류를 방지하기 위해서 0 길이 배열