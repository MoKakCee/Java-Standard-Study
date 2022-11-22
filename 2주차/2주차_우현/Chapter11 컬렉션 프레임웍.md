# CHAPTER 11 컬렉션 프레임웍

**컬렉션 프레임웍**

데이터 군을 저장하는 클래스들을 표준화한 설계

**컬렉션 프레임웍의 핵심 인터페이스**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9be32c99-46b8-456d-a70c-1be1991c84e5/Untitled.png)

| 인터페이스 | 특징 |
| --- | --- |
| List | 순서가 있는 데이터의 집합. 데이터의 중복을 허용한다. (ArrayList, LinkedList, Stack, Vector 등) |
| Set | 순서를 유지하지 않는 데이터의 집합, 데이터의 중복을 허용하지 않는다. (HashSet, TreeSet 등) |
| Map | 키와 값의 쌍으로 이루어진 데이터의 집합. 순서는 유지되지 않으며, 키는 중복을 허용하지 않고, 값은 중복을 허용한다. (HashMap, TreeMap, Hashtable, Properties 등) |

**Map인터페이스**

값을 반환받을때 타입이 Collection타입이다. 키를 반환받을때 타입은 Set타입이다.

Map인터페이스에서 값은 중복을 허용하기 때문에 Collection타입으로 반환하고, 키는 중복을 허용하지 않기 때문에 Set타입으로 반환한다.

**ArrayList**

ArrayList는 List인터페이스를 구현하기 때문에 데이터의 저장순서가 유지되고 중복을 허용한다.

ArrayList는 기존의 Vector를 개선한 것

ArrayList는 **Object배열**을 이용해서 데이터를 순차적으로 저장한다. (0번째 위치 → 1번째 위치→ 2번째 위치 …)

```java
ArrayList<String> list = new ArrayList<>(); // 선언
ArrayList<String> list2 = new ArrayList<>(10); // 크기 지정 가능

list.add("a"); // 값 추가
list.add(null); // null도 추가 가능
list.add(0, "b"); // 0번째 index에 5 추가
list.addAll(list2); // list 전체 복사

list.remove(0); // 해당 index의 값 제거
list.clear(); // ArrayList 값 모두 제거
list.size(); // ArrayList 크기 리턴

list.get(0); // 0번째 index 값 리턴
list.set(0, "aa"); // 0번째 index 값을 변경
list.contains("a"); // ArrayList에 해당 값이 존재하면 true
list.indexOf("a"); // ArrayList에 해당 값이 존재하면 index, 없으면 -1 리턴

list.retainAll(list2); // list2와 겹치는 부분만 남기고 나머지는 삭제
```

**ArrayList의 추가와 삭제**

ArrayList의 요소를 삭제하는 경우

1. 삭제할 데이터의 아래에 있는 데이터를 한 칸씩 위로 복사해서 삭제할 데이터를 덮어쓴다.
2. 데이터가 모두 한 칸씩 위로 이동하였으므로 마지막 데이터는 null로 변경
3. 데이터가 삭제되어 데이터의 개수가 줄었으므로 size의 값을 1감소.

배열에 객체를 순차적으로 저장할 때와 객체를 마지막에 저장된 것부터 삭제하면 데이터를 옮기지 않아도 되기 때문에 작업시간이 짧다.

반면 배열의 중간에 위치한 객체를 추가하거나 삭제하는 경우 다른 데이터의 위치를이동시켜야 하기 때문에 다루는 데이터의 개수가 많을수록 작업시간이 오래 걸린다.

**LinkedList**

배열은 구조가 간단하며 사용하기 쉽고 데이터를 읽어 오는데 걸리는 시간이 가장 빠르다는 장점을 가지고 있지만 다음과 같은 단점이 있다.

1. 크기를 변경할 수 없다.
2. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.

이러한 배열의 단점을 보완하기 위해 링크드 리스트가 고안되었다.

배열은 모든 데이터가 연속적으로 존재하지만 링크드 리스트는 불연속적으로 존재하는 데이터를 서로 연결한 형태로 구성되어 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/efe27481-7f54-42c5-8243-e957af4e1f0a/Untitled.png)

링크드 리스트의 각 요소들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성되어 있다.

```java
class Node {
		Node next;  //다음 요소의 주소를 저장
		Object obj; //데이터를 저장
}
```

**LinkedList의 추가와 삭제**

**LinkedList의 삭제**는 삭제하고자 하는 요소의 이전 요소를 삭제하고자 하는 요소의 다음 요소로 참조하도록 변경하기만 하면 된다.

배열처럼 데이터를 이동하기 위해 복사하는 과정이 없기 때문에 처리속도가 매우 빠르다.

**새로운 데이터를 추가**할 때는 새로운 요소를 생성한 다음 추가하고자 하는 위치의 이전 요소의 참조를 새로운 요소에 대한 참조로 변경해주고, 새로운 요소가 그 다음 요소를 참조하도록 변경하기만 하면 되므로 처리속도가 매우 빠르다.

**LinkedList 사용**

```java
// LinkedList는 초기 크기 지정 불가능
LinkedList<Integer> list = new LinkedList<>(); // 선언

list.addFirst(1); // 가장 앞에 값 추가
list.addLast(2); // 가장 뒤에 값 추가
list.add(3); // 값 추가
list.add(1, 10); // 1번 index에 값 추가

list.removeFirst(); // 가장 앞의 값 제거
list.removeLast(); // 가장 뒤의 값 제거
list.remove(1); // index 1에 해당하는 값 제거
list.remove(); // 생략시 0번 index 값 제거
list.clear(); // 모든 값 제거

list.size(); // LinkedList 크기 리턴
list.get(0); // 0번째 index 값 리턴
list.contains("a"); // LinkedList 해당 값이 존재하면 true
list.indexOf("a"); // LinkedList 해당 값이 존재하면 index, 없으면 -1 리턴
```

**ArrayList와 LinkedList의 비교**

| 컬렉션 | 읽기(접근시간) | 추가/삭제 | 비고 |
| --- | --- | --- | --- |
| ArrayList | 빠르다 | 느리다 | 순차적으로 추가삭제는 더 빠름. 비효율적인 메모리 사용 |
| LinkedList | 느리다 | 빠르다 | 데이터가 많을수록 접근성이 떨어짐 |

배열은 각 요소들이 연속적으로 메모리상에 존재하기 때문에 간단한 계산만으로 원하는 요소의 주소를 얻어서 저장된 데이터를 곧바로 읽어올 수 있다.

반면 LinkedList는 불연속적으로 위치한 각 요소들이 서로 연결된 것이라 처음부터 n번째 데이터까지 차례대로 따라가야만 원하는 값을 얻을 수 있다.

**Stack과 Queue**

스택: 마지막에 저장한 데이터를 가장 먼저 꺼내는 LIFO(Last In First Out)구조

큐: 처음에 저장한 데이터를 가장 먼저 꺼내는 FIFO(First In First Out)구조

순차적으로 데이터를 추가하고 삭제하는 **스택**에는 **ArrayList**와 같은 배열기반의 컬렉션 클래스가 적합.

**큐**는 데이터를 꺼낼 때 항상 첫 번째 저장된 데이터를 삭제하므로 **LinkedList**로 구현하는 것이 적합.

(ArrayList로 구현하게 되면 삭제할때마다 빈공간을 채우기 위해 데이터의 복사가 발생 → 메모리 낭비)

**Stack 사용**

```java
Stack<Integer> s = new Stack<>(); // 선언

s.push(1); // 값 추가
s.pop(); // 값 제거
s.clear(); // 초기화(모든 값 제거)
s.peek(); // top 값 출력
s.size(); // 스택 크기 출력
s.empty(); // 스택이 비어있으면 true
s.contains(1); // 스택에 값이 포함되어 있으면 true
```

**Queue 사용**

```java
Queue<Integer> q = new LinkedList<>(); // 선언

// 값 추가
q.add(1);
q.offer(2);

q.poll(); // top 값 출력 후 제거
q.remove(); // top 값 제거
q.clear(); // 큐 초기화
q.peek(); // top 값 출력
q.size(); // 큐 크기 출력
q.isEmpty() // 큐가 비어있으면 true
q.contains("str") // 큐에 포함되어 있으면 true
```

자바에서는 스택을 Stack클래스로 구현하여 제공하고 있지만, 큐는 Queue인터페이스로만 정의해 놓았을 뿐 별도의 클래스를 제공하고 있지 않다.

**Iterator, ListIterator, Enumeration**

Iterator, ListIterator, Enumeration은 모두 컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스이다.

**Iterator:** 컬렉션에 저장된 요소를 접근하는데 사용되는 인터페이스

**ListIterator:** Iterator에 양방향 조회기능추가(List를 구현한 경우만 사용 가능)

**Enumeration:** Iterator의 구버전

Collection인터페이스에는 ‘Iterator를 구현한 클래스의 인스턴스’를 반환하는 iterator()가 있다.

```java
List list = new ArrayList();
Iterator it = list.iterator();

while(it.hasNext()) {  // boolean hasNext() 읽어올 요소가 있는지 확인
		System.out.println(it.next());  // Object next() 다음 요소를 읽어옴
}
```

**Collection 요소를 순회하는** **Iterator**

- 컬렉션 프레임워크에 저장된 요소들을 하나씩 차례로 참조하는 것
- 순서가 있는 List 인터페이스의 경우는 Iterator를 사용하지 않고 get(i) 메서드를 활용할 수 있음
- Set 인터페이스의 경우 get(i) 메서드 제공되지 않으므로 Iterator를 활용하여 객체를 순회

**Map과 Iterator**

Map인터페이스를 구현한 컬렉션 클래스는 키와 값을 쌍으로 저장하고 있기 때문에 iterator()를 직접 호출할 수 없다.

그 대신 keySet()이나 entrySet()과 같은 메서드를 통해서 키와 값을 각각 따로 Set의 형태로 얻어 온 후에 다시 iterator()를 호출해야 한다.

```java
Map map = new HashMap();
Iterator it = map.entrySet().iterator();
```

**Arrays의 메서드(1) - 복사**

**배열의 복사 - copyOf(), copyOfRamge()**

copyOf()는 배열 전체를, copyOfRange()는 배열의 일부를 복사해서 새로운 배열을 만들어 반환.

```java
int[] arr = {0,1,2,3,4};
int[] arr2 = Arrays.copyOf(arr, arr.length); //arr2=[0,1,2,3,4]
int[] arr3 = Arrays.copyOf(arr, 3); //arr3=[0,1,2]
int[] arr4 = Arrays.copyOf(arr, 7); //arr4=[0,1,2,3,4,0,0]
int[] arr5 = Arrays.copyOfRange(arr, 2, 4); //arr5=[2,3] <- 4는 미포함
int[] arr6 = Arrays.copyOfRange(arr, 0, 7); //arr5=[0,1,2,3,4,0,0]
```

**Arrays의 메서드(2) - 채우기, 정렬, 검색**

**배열 채우기 - fill(), setAll()**

**fill()**은 배열의 모든 요소를 지정된 값으로 채운다.

**setAll()**은 배열을 채우는데 사용할 함수형 인터페이스를 매개변수로 받는다. 이 메서드를 호출할 때는 함수형 인터페이스를 구현한 객체를 매개변수로 지정하던가 아니면 람다식으로 지정해야한다.

```java
int[] arr = new int[5];
Arrays.fill(arr, 9);  //arr=[9,9,9,9,9]
Arrays.setAll(arr, (i) -> (int)(Math.random()*5)+1) //arr=[1,5,2,1,1]
```

**배열의 정렬과 검색 - sort(), binarySearch()**

**sort()**는 배열을 정렬

**binarySearch()**는 배열에 저장된 요소를 검색, 지정된 값이 저장된 외치(index)를 찾아서 반환, 반드시 배열이 정렬된 상태이어야 올바른 결과를 얻는다. 또 검색한 값과 일치하는 요소들이 여러 개 있다면, 이 중에서 어떤 것의 위치가 반환되는지 알 수 없다.

배열의 첫 번째 요소부터 순서대로 하나씩 검색하는 것을 ‘순차 검색’ 이라고 하는데, 이 검색방법은 배열이 정렬되어 있을 필요는 없다. 하지만 하나씩 비교하기 때문에 시간이 많이 걸린다.

반면 이진탐색(binary search)는 배열의 검색할 범위를 반복적으로 절반씩 줄여가면서 검색하기 때문에 검색속도가 상당히 빠르다. 단, 정렬이 되어 있어야 한다.

**Arrays의 메서드(3) - 비교와 출력**
