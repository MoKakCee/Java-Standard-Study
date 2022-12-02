# CHAPTER 15 입출력

### 입출력(I/O)과 스트림(stream)

**입출력**

컴퓨터 내부 또는 외부의 장치와 프로그램간 데이터를 주고받는 것

**스트림(stream)**

자바에서 입출력을 수행하려면, 즉 어느 한쪽에서 다른 쪽으로 데이터를 전달하려면, 두 대상을 연결하고 데이터를 전송할 수 있는 무언가가 필요한데 이것을 스트림(stream)이라고 정의.

14장의 스트림과 같은 용어를 쓰지만 다른 개념

즉, 스트림이란 데이터를 운반하는데 사용되는 연결통로

스트림은 단방향통신만 가능하기 때문에 하나의 스트림으로 입력과 출력을 동시에 처리할수 없다.

그래서 입력과 출력을 동시에 수행하려면 입력을 위한 입력스트림과 출력을 위한 출력스트림, 모두 2개의 스트림이 필요하다.

스트림은 먼저 보낸 데이터를 먼저 받게 되어 있으며 중간에 건너뜀 없이 연속적으로 데이터를 주고받는다.

### 바이트 기반 스트림-InpustStream, OutputStream

스트림은 바이트단위로 데이터를 전송하며 입출력 대상에 따라 다음과 같은 입출력스트림이 있다.

- 파일
- 메모리(byte배열)
- 프로세스(프로세스간의 통신)
- 오디오장치

InpustStream과 OutputStream이 최상위 부모이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c6a7e4e-169a-40ec-b21b-88758085a57d/Untitled.png)

### 보조 스트림

기존 스트림의 기능을 보완하기 위한 보조 스트림이 제공.

보조스트림은 데이터를 입출력할 수 있는 기능은 없지만, 스트림의 기능을 향상시키거나 새로운 기능을 추가할 수 있다.

그래서 스트림을 먼저 생성한 다으 보조스트림을 생성해야 한다.

```java
//먼저 기반 스트림을 생성한다.
FileInpustStream fis = new FileInputStream("test.txt");

//기반 스트림을 이용해서 보조 스트림을 생성한다.
BufferedInputStream bis = new BufferedInputStream(fis);
bis.read();  //보조 스트림인 BufferedInputStream으로부터 데이터를 읽는다.
```

버퍼를 사용한 입출력과 사용하지 않은 입출력간의 성능차이는 상당하기 때문에 버퍼를 이용한 보조 스트림을 사용하자.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/548c1153-860b-435f-b846-14339d1b7bee/Untitled.png)

### **문자기반 스트림 - Reader, Writer**

지금까지의 스트림은 모두 바이트기반 스트림이었다.

바이트기반은 입출력의 단위가 1byte이다. 

C언어와 달리 Java에서는 한 문자를 의미하는 char형이 1byte가 아니라 2byte이기 때문에 바이트기반 스트림으로 처리하기 어렵다.

그래서 문자기반의 스트림이 제공된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72ba9b08-861b-4261-bfff-391a07c6a629/Untitled.png)

문자기반 스트림은 byte배열 대신 char배열을 사용

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b47face-ebba-4661-b944-2c7f7f48b3d3/Untitled.png)

문자기반 스트림의 보조 스트림

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/581a3889-2ebf-4d46-9819-4fac6fa0e94c/Untitled.png)

### InputStream과 OutputStream

InpustStream과 OutputStream은 모든 바이트 기반 스트림의 최상위 부모이다.

InputStream

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f90b7cb-68ad-46d9-82c2-37be4278605d/Untitled.png)

OutputStream

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfd4d139-9aff-4d4b-b297-431b7f8bf62c/Untitled.png)

프로그램이 종료될 때, 사용하고 닫지 않은 스트림을 JVM이 자동적으로 닫아 주기는 하지만, 스트림을 사용해서 모든 작업을 마치고 난 후에는 close()를 호출해서 반드시 닫아 주어야 한다.

그러나 ByteArrayInputStream과 같이 메모리를 사용하는 스트림과 System.int, System.out과 같은 표준 입출력 스트림은 닫아 주지 않아도 된다.

### FileInputStream과 FileOutputStream

파일 입출력을 위한 스트림.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dd833a9f-3a7c-43ef-9229-e53af348ebea/Untitled.png)

### FilterInputStream과 FilterOutputStream

FilterInputStream/FilterOutputStream은 InputStream/OutputStream의 자손이면서 모든 보조 스트림의 조상이다. (바이트 기반 스트림이다.)

보조스트림이므로 자체적으로 입출력을 수행할 수 없기 때문에 기반 스트림이 필요하다.

상속을 통해 FilterInputStream/FilterOutputStream의 read()와 write()를 원하는 기능대로 오버라이딩해야 한다. (FilterInputStream은 접근 제어자가 protected여서 오버라이딩이 필수)

### BufferedInputStream과 BufferedOutputStream

스트림의 입출력 효율을 높이기 위해 버퍼를 사용하는 보조스트림이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab6ff3b6-1ea6-4278-b888-c30af66ea641/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3cbf0434-ea0c-470e-85bb-3126da7050b4/Untitled.png)

### SequenceInputStream

여러 개의 입력스트림을 연속적으로 연결해서 하나의 스트림으로부터 데이터를 읽는 것과 같이 처리할 수 있도록 도와주는 보조 스트림

- 큰 파일을 여러 개의 작은 파일로 나누었다가 하나의 파일로 합치는 것과 같은 작업을 수행할 때 사용하면 좋다.
- 다른 보조 스트림들과는 달리 FilterInputStream의 자손이 아닌 InputStream을 바로 상속받아서 구현하였다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5983cc20-dd90-472f-951e-377895daab72/Untitled.png)

### PrintStream

PrintStream은 데이터를 기반스트림에 다양한 형태로 출력할 수 있는 print, println, printf와 같은 메서드를 오버로딩하여 제공한다.

- System.out과 System.err이 PrintStream이다.
- PrintStream보다 PrintWriter를 사용하는 것을 권장.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c7b94fb1-b5f4-4d93-ae29-3520f3054c4a/Untitled.png)

### 문자 기반 스트림 - Reader, Writer

바이트기반 스트림의 조상이 InputStreamReader/OutPutStream인 것과 같이 문자기반의 스트림에서는 Reader/Writer가 그와 같은 역할을 한다.

**Reader**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/37f6324e-35d9-4e85-9ca5-b07adf11f7a4/Untitled.png)

**Writer**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83f6a467-fc40-4f65-bf33-ad751e7f27c2/Untitled.png)

### FileReader와 FileWriter

사용방법은 FileInputStream/FileOutputStream과 다르지 않다. (FileReader/FileWriter는 문자기반 스트림이다.)

FileInputStream는 한글이 깨진다.

### StringReader와 StringWriter

CharArrayReader, CharArrayWriter처럼 입출력 대상이 메모리인 스트림이다.

StringWriter에 출력되는 데이터는 내부의 StringBuffer에 저장된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9d895522-fee5-4d28-8c57-1550198ecf38/Untitled.png)

### BufferedReader와 BufferedWriter

버퍼를 이용해서 입출력의 효율을 높일 수 있도록 해주는 보조스트림이다.

라인 단위의 입출력이 편리하다.

### InputStreamReader, OutputStreamWriter

바이트기반 스트림을 문자기반스트림처럼 쓸 수 있게 해준다.

인코딩을 변환하여 입출력할 수 있게 해준다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83e41727-abf5-4506-9905-8df70a05629c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/301ebf5d-fe80-461d-8e7e-cdb306ca37ae/Untitled.png)

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String s = br.readLine();
```

BufferedReader와 InputStream인 System.in을 연결하기 위해 InputStreamReader를 사용.

### 표준 입출력

표준 입출력은 콘솔(도스창)을 통한 데이터 입력과 콘솔로의 데이터 출력을 의미한다.

JVM이 시작되면서 자동적으로 생성되는 스트림이다.

- System.in - 콘솔로부터 데이터를 입력받는데 사용
- System.out - 콘솔로 데이터를 출력하는데 사용
- System.err - 콘솔로 데이터를 출력하는데 사용

### 표준 입출력의 대상변경

기본 입출력의 대상은 콘솔 화면이지만, setIn(), setOut(), setErr()를 사용하면 입출력을 콘솔 이외에 다른 입출력 대상으로 변경가능

### File

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2d8e604b-713a-4b72-86ff-5f1f997e80bf/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4af0ce9f-b0de-4678-919d-cd6b1e9d0562/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59dfa2c6-61db-4954-93fe-01eaa6590f89/Untitled.png)

### 직렬화

직렬화란 객체를 데이터 스트림으로 만드는 것을 뜻한다.

객체에 저장된 데이터를 스트림에 쓰기(write)위해 연속적인(serial) 데이터로 변환하는 것을 말한다.

반대로 스트림으로부터 데이터를 읽어서 객체를 만드는 것을 역직렬화라고 한다.

객체는 클래스에 정의된 인스턴슨변수의 집합이다. 객체에는 클래스변수나 메서드가 포함되지 않는다. 객체는 오직 인스턴스 변수들로만 구성되어 있다.

인스턴스변수는 인스턴스마다 다른 값을 가질 수 있여야하기 때문에 별도의 메모리공간이 필요하지만 메서드는 변하는 것이 아니라서 메모리를 낭비해 가면서 인스턴스마다 같은 내용의 코드(메서드)를 포함시킬 이유는 없다.

그래서 객체를 저장한다는 것은 객체의 모든 인스턴스변수의 값을 저장한다는 것과 같은 의미.

### ObjectInputStream, ObjectOutputStream

직렬화(스트림에 객체를 출력)에는 ObjectInpuStream을 사용하고, 역직렬화(스트림으로부터 객체를 입력)에는 ObjectInputStream을 사용한다. (보조스트림이어서 기반스트림을 필요로 한다.)

 

객체를 파일에 저장하는 방법

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8619cc88-bb00-49ff-a3f6-5c006d6433c9/Untitled.png)

파일에 저장된 객체를 다시 읽어오는 방법

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee07e413-5aeb-499c-9201-c97e5a7f1040/Untitled.png)

직렬화작업시간을 단축시킬려면 직렬화하고자 하는 객체의 클래스에 다음과 같은 2개의 메서드를 직접 구현해주어야 한다.

```java
private void writeObject(ObjectOutputStream out)
			throws IOException {
			//write메서드를 사용해서 직렬화를 수행한다.
}

private void readObject(ObjectInputStream in)
			throws IOException, ClassNotFoundException {
			//read메서드를 사용해서 역직렬화를 수행한다.
}
```

### 직렬화가 가능한 클래스 만들기

직렬화 하고자 하는 클래스가 java.io.Serializable인터페이스를 구현하도록 하면 된다.

부모클래스가 Serializable속성이 있다면 자식클래스도 직렬화가 가능하다.

### 직렬화 대상에서 제외시키기 - transient

제어자 transient가 붙은 인스턴스변수는 직렬화 대상에서 제외된다.

transient가 붙은 인스턴스변수의 값은 그 타입의 기본값으로 직렬화된다고 볼 수 있다.
