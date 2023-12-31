# Java 기초 개념
### 객체지향 프로그래밍(OOP)의 특징 - Object Oriented Programming
※ 코드의 재사용성이 용이하다.

핵심적인 특징 : 추상화, 캡슐화, 상속, 다형성

### 클래스와 객체
클래스란? 객체를 생성하는데 사용한다.

#### 클래스의 정의
1. 변수 : 하나의 데이터를 저장하는 공간
2. 배열 : 같은 종류의 여러 데이터를 하나로 저장하는 공간
3. 구조체 : 서로 관련된 여러 데이터를 하나로 저장하는 공간
4. 클래스 : 데이터와 메소드의 결합 ( 구조체 + 메소드 )

객체란? 기능(메소드)와 속성(변수)

인스턴스란? 특정 클래스로부터 생성된 객체를 의미한다.

```java
class Ex{
    // 변수 (속성)
    int channel;
    String color;
    boolean power;
    // 메소드 (기능)
    void power(){power = !power;}
    void channelUp(){channel++;}
    void channelDown(){channel--;}
}
```

### 여러 클래스 작성시 주의 사항
public class가 있는 경우 소스 파일의 이름은 반드시 public class의 이름과 일치해야한다.

※ 한개의 소스파일에는 단 하나의 public class만 존재한다.

※ 만약 public class가 없다면 class의 이름 중 하나는 소스파일의 이름과 일치하면 된다.

이외의 class에는 public을 제외하면 되지만 하나의 소스파일에는 하나의 클래스만 작성하는 것을 권장한다.

```java
public class Github{}
       class Test1{}
       class Test2{}
```

### 객체의 생성과 사용
생성하는 방법 : 클래스명 참조변수명 = new 클래스명();

⭐ 기본형(Primitive) byte, short, int, long, float, double, char, boolean을 제외한 나머지는 참조형이다.

객체를 사용할때는 참조변수명을 통해 사용할 수 있다.

참조변수명에는 객체의 주소가 저장된다.
```java
Tv t1 = new Tv(); // 예) 객체 주소 : 0X100
Tv t2 = new Tv(); // 예) 객체 주소 : 0X200
// 이 경우 0X200 주소의 객체를 아무도 참조하고 있지 않기 때문에 GC(가바지 컬렉터)에 의해 제거된다.
t2 = t1; 
t1.channel = 7; // 변수 사용
t1.channelDown(); // 메소드 호출
```

⭐ 하나의 인스턴스를 여러 개의 참조변수가 가리키는 것은 가능하다.

⭐ 하나의 참조변수를 여러 개의 인스턴스가 가리키는 것은 불가능하다.
#### 객체 배열
Java에서 알고 있어야하는 배열의 특징으로는 길이의 불변이 있다.

```java
Tv[] tvArr = new Tv[3]; // 길이가 3인 배열을 만든다.
for(int i = 0; i < tvArr.length; i++){
    tvArr[i] = new Tv();
}
// 각각의 인덱스에는 각각의 생성한 객체의 주소가 저장되어있다.
```

### 변수의 종류
```java
class Ex{
    int iv; // 인스턴스 변수
    static int cv; // 클래스 변수

    void method(){ // 메소드 정의
        int lv = 0; // 지역 변수
    }
}
```

클래스 변수는 클래스가 메모리(RAM)에 올라갈때 생성되며 프로그램 종료시 제거된다.

(객체 생성 필요 X)

⭐ 멤버 변수 중에서 공통으로 사용되는 것에 static을 붙여서 클래스변수로 사용한다.

```java
Ex.cv = 300;
// 이런식으로 객체 생성없이 "클래스.클래스변수"로 호출할 수 있다.
// 객체들이 공통으로 사용해야 하는 것을 클래스 변수로 만들어 둔다.
```

인스턴스 변수는 인스턴스가 생성된다.

지역변수는 메소드가 호출될때 생성되며 메소드가 종료될때 제거된다.

### 메소드
메소드는 중복을 줄이고, 관리가 쉽고, 재사용성이 좋다는 장점이 있다.

OOD(객체 지향 설계)에서 SRP(Single Responsibility Principle)에 의하면 하나의 메소드는 한가지의 기능만 수행하도록 작성해야 한다.
```java
// 선언부 : 반환타입 메소드명 (매개변수)
int test (int x, int y){
// 구현부 : 함수의 내용
    int result = x + y;
    return result;
}
// 이 메소드에서 지역변수는 x, y, result이다.
```

#### static 메소드
객체 생성 없이 "클래스 이름. 메소드이름()"으로 호출 가능하다.

인스턴스 멤버(변수, 메소드)와 관련없는 작업을 하는 메소드를 의미하기 때문에 인스턴스 멤버를 사용할 수 없다.

클래스 멤버(변수, 메소드)는 사용이 가능하다.

⭐ 이런 이유는 생성 시기가 static 메소드가 빠르기 때문이다.

#### 인스턴스 메소드
객체 생성 후 "참조변수명.메소드이름()"으로 호출 가능하다.

인스턴스 멤버(변수, 메소드)와 클래스 멤버(변수, 메소드)를 모두 사용할 수 있다.

### 호출 스택 (Call Stack)
메소드 수행에 필요한 메모리가 제공되는 공간을 의미한다.

메소드가 호출되면 호출스택에 메모리를 할당 받고 종료되면 해제된다.

⭐ Last in Frist Out 구조를 가지고 있다.

⭐ 일반적으로는 하나의 호출 스택만 가지고 있지만 멀티 스레드 환경에서는 여러개의 호출 스택이 존재한다.

### 매개변수
⭐ 기본형 매개변수 : 변수의 값을 읽기만 가능하다.

⭐ 참조형 매개변수 : 변수의 값을 읽고 변경할 수 있다.

기본형 매개변수
```java
public class Test{
    public static void main(String[] args){
        Test t = new Test(); // 예) 주소 0X100
        t.x = 10; // 객체에 있는 x를 10으로 초기화
        System.out.println("main x = " + t.x); // 10
        change(t.x); // 1000
        System.out.println("main x = " + t.x); // 10
        // 이런식으로 기본형 매개변수의 경우 값을 읽어올 수 밖에 없다.
    }

    static void change(int x) { // 기본형 매개변수
        x = 1000;
        System.out.println("change() x = " + x);
    }
}
```

참조형 매개변수
```java
public class Test{
    public static void main(String[] args){
        Test t = new Test(); // 예) 주소 0X100
        t.x = 10; // 객체에 있는 x를 10으로 초기화
        System.out.println("main x = " + t.x); // 10
        change(t); // 1000
        System.out.println("main x = " + t.x); // 1000
        // 이런식으로 참조형 매개변수는 값을 읽거나 변경할 수 있다.
    }

    static void change(Test t) { // 참조형 매개변수
        t.x = 1000; // 주소 0X100에 변수 x에 접근하여 변경하였다.
        System.out.println("change() x = " + t.x);
    }
}
```

### 오버로딩 : 새로운 메소드 정의
한 클래스 안에 같은 이름의 메소드를 여러개 정의하는 것을 말한다.

매개변수는 다르지만 같은 의미의 기능수행하는 메소드를 만들 때 사용한다.

1. 메소드의 이름이 같아야한다.
2. 매개변수의 개수 또는 타입이 달라야한다.
3. 리턴타입은 영향을 주지 않는다.

```java
int add(int x, int y){return x + y;} // 기존 메소드
int add(int x, int y, int z) {return x + y + z;} // 오버로딩 O
long add(int x, int y){return (long)(x + y);} // 오버로딩 X >> 리턴 타입은 영향을 주지 않는다.
```

### 생성자
인스턴스가 생성될 때마다 호출되는 인스턴스 초기화 메소드를 말한다.

생성자의 이름은 클래스 이름과 같아야한다.

⭐ 클래스는 하나 이상의 생성자를 가지고 있어야한다.

⭐ 클래스에 생성자가 하나도 없는 경우에만 컴파일러가 기본생성자를 자동으로 추가한  바이트 코드로 만든다.

```java
class Test{
    int x;
    int y;

    // 생성자 오버로딩을 통해 이런식으로 여러개 만들 수 있다.
    Test(){ // 기본 생성자
        // 인스턴스 초기화 작업
    }
    Test(int x, int y){ // 매개변수 있는 생성자
        // 인스턴스 초기화 작업
        this.x = x;
        this.y = y;
    }
}
```

매개변수 있는 생성자의 흐름을 알아보자.

Test t = new Test(1,2);

1. 참조변수 만들어진다.
2. new 연산자가 객체를 만든다.
3. 생성자가 호출된다.
4. 생성자에 의해 인스턴스 변수가 초기화가 된다.
5. 대입으로 참조변수가 해당 객체를 가르킨다.

### 생성자 this(), 참조변수 this
생성자 this()는 같은 클래스 안에서 생성자가 다른 생성자를 호출할때 사용된다.

⭐ 생성자 this()의 경우 생성자의 첫 줄에서만 사용가능하다.

참조변수 this의 경우 인스턴스 자기 자신을 가리키는 참조변수이다.

⭐ 인스턴스 메소드(생성자 포함)에서 사용가능하다.

⭐ 대표적으로 지역변수와 인스턴스 변수를 구분할 때 사용한다.

```java
class Test{
    int x;
    int y;

    Test(){
        this(1,2); // Test(int x, int y)를 호출 한 것이다.
    }
    Test(int x){
        this(x, 20); // Test(int x, int y)를 호출한 것이다.
    }
    Test(int x, int y){
        this.x = x; // this는 Test를 말한다.
        // 지역변수인 매개변수의 x와 인스턴스 변수 x를 구분지은 것이다.
        // 의미 >> 인스턴스 변수 x = 지역변수 x
        this.y = y;
    }
}
```

### 변수의 초기화
⭐ 지역변수의 경우는 사용전에 수동으로 초기화 해줘야한다. (인스턴스, 클래스변수의 경우 자동 초기화)

⭐ 지역변수의 경우 생명주기가 짧기 때문에 매번 초기화 하는 것보다 새로운 값으로 덮어쓰는 것이 성능에 좋다.

⭐ 자료형들의 기본값

- boolean : false : 1 byte
- char : '\u0000' : 1 byte
- byte, short, int : 0 : 1, 2, 4 byte
- long : 0L, 0 : 8 byte
- float : 0.0f : 4 byte
- double : 0.0d, 0.0 : 8 byte
- 참조형 : null

##### 명시적 초기화 (=)
```java
class Test{
    int x = 1; // 기본형 변수의 초기화
    Git git = new Git(); // 참조형 변수의 초기화
}
```
##### 초기화 블럭 (복잡한 초기화)
인스턴스 초기화 블럭 : {} >> 잘 사용하지 않는다.

클래스 초기화 블럭 : static {}
```java
class Test{
    static int[] arr = new int[3];
    static { // 복잡한 초기
        for(int i = 0; i < arr.length; i++){
            arr[i] = (int)(Math.random() * 10) +1;
        }
    }
}
```

##### 생성자 (인스턴스 초기화, 복잡한 초기화)
```java
Test(int x, int y){
    this.x = x;
    this.y = y;
}
```

⭐ 클래스, 인스턴스 변수의 초기화는 자동 초기화(기본값), 간단 초기화(명시), 복잡 초기화(블록, 생성자)가 있다.

#### 멤버 변수의 초기화 시점
클래스 변수 : 클래스가 처음 로딩(메모리에 올라갈때)될 때 단 한번 초기화된다.

인스턴스 변수 : 인스턴스가 생성될때 마다 초기화 된다.

```java
class Test{
    static int cv = 1;
    int iv = 2;

    static { cv = 3; }
    { iv = 4; }

    Test(){iv = 5;}
}
```

1. 클래스 변수 cv의 자동 초기화로 기본값 0
2. 클래스 변수 cv의 명시적 초기화로 1
3. 클래스 변수 cv의 초기화 블록으로 3  >> 클래스 변수 초기화 완료
4. 인스턴스 변수 iv의 자동 초기화로 기본값 0
5. 인스턴스 변수 iv의 명시적 초기화로 2
6. 인스턴스 변수 iv의 초기화 블록으로 4
7. 인스턴스 변수 iv의 생성자로 인해 5 >> 인스턴스 변수 초기화 완료

### 상속(Inheritance) : ~은 ~이다.
기존의 클래스로 새로운 클래스를 작성하는 것이며 두 클래스는 부모와 자식의 관계를 맺어주는것이다.

⭐ Java는 단일 상속만을 허용한다!

만약 여러개의 클래스를 사용하고 싶다면 비중이 가장 높은 클래스는 상속을 나머지는 포함관계로 작성할 수 있다.

⭐ 모든 클래스는 Object를 상속받게 되기 때문에 Object에서 정의된 11개(toString(), equals(Object obj), hashCode()...)의 메소드를 상속받는다.

```java
class Test{} // extends Object는 생략가능하고 컴파일러가 자동으로 작성해준다.
class Test2 extends Test{}
class Test3 extends Test, Test4{} // Error!!!
```

⭐ 자식은 조상의 모든 멤버를 상속 받지만 생성자와 초기화 블럭은 제외된다.

이런 이유로 인해 자식의 멤버 개수가 조상보다 적을 수 없다. (같거나 많다.)

⭐ 자식의 변경은 조상 클래스에 영향을 미치지 않는다.

### 포함(Composite) : ~은 ~을 가지고 있다.
클래스의 멤버로 참조변수를 선언하는 것을 말한다.

작은 단위의 클래스를 만든 후 조합하여 클래스를 만들어서 복잡도를 줄일 수 있다.

⭐ 상속보다는 포함 관계가 많다.

```java
class Test2{
    Test t = new Test(); // 인스턴스 변수로 참조변수를 선언
}

Test2 t2 = new Test2();
// Test2에서 Test의 멤버에 접근하려면? t2.t.x; 이런식으로 접근이 가능하다.
```

### 오버라이딩(Overriding) : 내용 변경
상속받은 조상의 메소드를 자신에게 맞게 변경하는 것을 말한다.

⭐ 오버라이딩에서 가장 많은 실수가 오타인데 이를 방지할 수 있는것이 Override 어노테이션이다.

⭐ Override 어노테이션을 붙이면 컴파일러에게 해당 메소드가 오버라이딩 되었다는 사실을 알리고 컴파일시 체크를 하는데 이를 통해 실수를 방지해준다.

오버라이딩의 조건

⭐ 선언부가 조상 클래스의 메소드와 일치해야 한다.

⭐ 접근 제어자를 조상 클래스의 메소드보다 좁은 범위로 변경할 수 없다.

접근 제어자 : public > protected > (default) > private

좁은 범위로 변경할 수 없다는 것은 조상이 protected 접근제어자를 가진다면 자식은 private으로 바꿀 수 없다는 말이다.

⭐ 예외는 조상 클래스의 메소드보다 많이 선언할 수 없다.

```java
class Test{
    int x;
    int y;
    String getLoctaion(){
        return "x : " + x + ", y : " + y;
    }
}

class Test2 extends Test{
    int z;
    // 오버라이딩 : 구현부만 변경한다.
    String getLocation(){ 
        return "x : " + x + ", y : " + y + ", z : " + z;
    }
}
```

### 참조변수 super
객체 자신을 가리키는 참조변수이며 인스턴스 메소드(생성자 포함)에서만 존재한다.

조상의 멤버를 자신의 멤버와 구별할 때 사용된다.

```java
class Git{
    public static void main(String[] args){
        Test t = new Test();
        t.method();
    }
}

class Test {int x = 10;}
class Test2 extends Test{
    int x = 20;
    // 현재 Test2의 객체에는 x가 2개 있다.
    
    void main(){
        System.out.println("X = " + x); // 20 >> 가까운 x를 찾는다.
        System.out.println("this.X = " + this.x); // 20
        System.out.println("super.X = " + super.x); // 10
    }
}
```

### 생성자 super()
조상의 생성자를 호출할 때 사용한다.

조상의 멤버는 조상의 생성자를 호출해서 초기화한다.

⭐ 상속시 생성자와 초기화 블록은 상속되지 않기 때문에 사용된다.

⭐ 생성자의 첫 줄에 반드시 생서자를 호출해야 하며 그렇지 않을 경우 컴파일러가 생성자 첫줄에 super()를 삽입한다.

```java
class Point{
    int x;
    int y;
    Point(int x, int y){
        // super(); >> 생성자 첫줄에 super()를 컴파일러가 자동 추가한다.
        this.x = x;
        this.y = y;
    }
}

class Point3D extends Point{
    int z;
    Point3D(int x, int y, int z){
        /*
        this.x = x; // 부모의 멤버를 자식이 초기화 하고 있다.
        this.y = y; // 부모의 멤버를 자식이 초기화 하고 있다.
        */
        // 부모의 멤버는 부모가 초기화하도록 해야하는 것이 좋다.
        super(x, y);
        this.z = z;
    }
}
```
### 제어자(Modifier)
클래스와 클래스의 멤버(변수, 메소드)에 붙혀서 부가적인 의미를 부여한다.

접근제어자 : public, protected, (default), private

⭐ 접근제어자의 경우는 하나만 사용 가능하다.

그 외 제어자 : static, final, abstract, native, transient, synchronized, volatile, strictfp

```java
public class Test{
    public static final int YEAR = 2023;
    // 보통 접근제어자를 먼저 쓴다.
    public static void main(String[] args){
        System.out.println("YEAR = " + YEAR);
    }
}
```

#### static (변수, 메소드)
변수에 사용하게 되면 모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.

- 클래스 변수는 인스턴스를 생성하지 않고도 사용 가능하다.
- 클래스가 메모리레 로드될 때 생성된다.

메소드에 사용하게 되면 인스터스를 생성하지 않고도 호출이 가능한 static 메소드가 된다.

- static 메소드는 내부에서 인스턴스 멤버를 직접 사용할 수 없게 된다.

```java
class Test{
    static int width = 100;
    static {} // 복잡한 초기화
    static int show(int x){
        return 1;
    }
}
```

#### final (클래스, 메소드, 멤버변수, 지역변수)
클래스에 사용하게 되면 "확장될 수 없는 클래스"가 된다.

- 쉽게 말해 다른 클래스의 부모가 될 수 없다.

메소드에 사용하게 되면 오버라이딩으로 재정의 할 수 없다.

변수에 사용하게 되면 값을 변경할 수 없는 상수가 된다.

```java
final class Test{
    final int MAX_SIZE = 5;
    final void show(){
        final int LV = MAX_SIZE;
        System.out.println(LV);
    }
}
```

#### abstract (클래스, 메소드)
클래스에 사용하면 클래스 내부에 추상 메소드가 선언되어 있다는 의미이다.

⭐ 미완성 설계도이기 때문에 인스턴스를 생성 할 수 없다.

⭐ 자식이 상속을 받아서 완전한 클래스로 만든 후 사용해야 한다.

메소드에 사용하면 선언부만 있고 구현부가 없는 추상 메소드임을 알린다.

```java
abstract class AbstractTest{ // 추상 클래스 
    abstract void move(); // 추상 메소드
}
```

### 접근제어자
접근제어자를 사용하는 이유는 외부로부터 데이터를 보호하기 위해서이며 이를 캡슐화라고 부른다.

#### public (클래스, 멤버)
접근 제한이 전혀 없다.
#### protected (멤버)
같은 패키지 내에서 사용 가능 + 다른 패키지의 상속 후 자식 클래스에서만 사용 가능
#### (default) (클래스, 멤버) - 생략 가능
같은 패키지 내에서만 사용 가능
#### private (멤버)
같은 클래스 내에서만 사용 가능

### 캡슐화
외부에는 불필요하고 내부적으로만 사용되는 부분을 감추기 위해서 사용한다.

```java
public class Test{
    // private이기 때문에 외부에서 직접 접근이 안된다.
    private int year;
    private int month;

    // 메소드를 사용해야만 외부에서 간접적으로 접근할 수 있다.
    public int getYear(){return year;}
    public int setYear(int year){
        if(year < 0 || year > 2023){
            return;
        }
        this.year = year;
    }
}
```

### 다형성
쉽게 말해 부모의 타입으로 자식의 타입을 컨트롤 할 수 있다.

```java
class Tv{
    int channel;
    void channelUp(){++channel;}
}
class SmartTv extends Tv{
    String text;
    void show(){System.out.println(text);}
}

Tv t = new SmartTv(); // 가능하다.
// 하지만 이 경우 참조변수 t에서 접근 가능한것은 Tv 인스턴스이다.
```

### 참조 변수의 형변환
사용할 수 있는 멤버의 개수를 조절하는 것을 말한다.

```java
SmartTv st = new SmartTv();
Tv t = (Tv)st; // 가능 조상인 Tv타입으로 형 변환(생략 가능)
SmartTv st2 = (SmartTv)t; // 가능 자식인 smartTV타입으로 형 변환 (생략 불가능)

// 상속 관계가 아닌 클래스 간의 형변환은 불가능하다.
```

### instanceof 연산자
참조변수의 형변환 가능 여부 확인에 사용한다. (가능할 경우 true 반환)

⭐ A instanceof B : B가 A 자기자신이거나 부모일 경우 true를 반환

```java
void work(Tv t){
    if(t instnaceof SmartTv){
        SmartTv st = (SmartTv)t;
        t.show();
    }
}
```

### 추상 클래스(Abstract class)
미완성 설계도이며 추상 메소드를 하나라도 갖고 있는 클래스를 말한다.

- 추상메소드 : 꼭 필요하지만 자식마다 다르게 구현될 것으로 예상되는 경우

다른 클래스 작성에 도움을 주기 위한 것이며 독자적으로 인스턴스 생성이 불가능 하다.

상속을 통해 모든 추상 메소드를 완성해야 인스턴스를 생성 가능하다.

```java
abstract class Player{
    int currentPos; // 인스턴스 변수

    Player(){ // 생성자
        currentPos = 0;
    }
    
    abstract void play(int pos); // 추상 메소드
    abstract void stop(); // 추상 메소드
    void play(){ // 오버로딩 : 매개변수의 개수 또는 타입이 다른 
        play(currentPos); // 추상 메소드 호출 가능
        // 추상 메소드를 호출할때 필요한 것은 선언부 이기 때문이다.
    }
}

class AudioPlayer extends Player{
    void play(int pos){}
    void stop(){}
}
AudioPlayer ap = new AudioPlayer(); // OK
Player p = new AudioPlayer(); // OK
```

### 인터페이스(interface)
프로그래밍 관점으로는 추상 메소드의 집합을 의미하며, 구현된 것이 전혀 없는 설계도이고 모든 멤버가 public이다.

- JDK 1.8 이후로는 static 메소드, 상수, 디폴트 메소드도 가능하지만 부수적인것이다.

```java
interface Test{
    public static final int YEAR = 2023; // 상수
    String COLOR = "RED";
    public abstract void show(); // 추상 메소드
    void getGit();

    // 메소드는 public abstract가 공통이기 때문에 생략 가능하다.
    // 상수의 경우 public static final이 공통이기 때문에 생략 가능하다.
}
```

#### 인터페이스 상속
인터페이스의 조상은 인터페이스만 가능하고 Object는 인터페이스의 최고 조상이 아니다.

⭐ 다중 상속이 가능하다. - 충돌이 발생해도 구현부가 없기 때문에 상관없다.

⭐ 인터페이스를 구현한 곳에서 구현부를 완성하면 되기 때문이다.

```java
interface Movable{
    void move(int x, int y);
}
interface Attackable{
    void attack(Unit u);
}
interface Fightable extends Movable, Attackable{}
```

#### 인터페이스 구현
인터페이스에 정의된 추상 메소드를 완성하는 것을 말한다.

⭐ 모든 추상 메소드를 구현하지 않으면 추상 클래스가 된다.

```java
class Fighter implements Fightable{
    // implements 키워드를 사용해서 인터페이스의 추상메소드를 모두 구현해야한다.
    void move(int x, int y) {}
    void attack(Unit u) {}
}
Fighter f = new Fighter();
```

#### 인터페이스를 이용한 다형성
인터페이스도 구현 클래스의 부모라고 볼 수 있다.

```java
class Fighter extends Unit implements Fightable{
    public void move(int x, int y){}
    public void attack(Fightable f){}
}

Unit u = new Fighter(); // 클래스 간 다형성

Fightable f = new Fighter(); // 인터페이스와 클래스 간 다형성
// 이때도 Fightable에 정의된 메소드들만 사용가능하다.
f.move(10,20);
f.attack(new Fighter()); // 매개변수 다형성을 이용
```

그 외에도 인터페이스를 메소드의 리턴타입으로 지정할 수 있다.

```java
Fightable method(){
    Fighter f = new Fighter(); // Fighter는 Fightable을 구현한 객체이기 때문에 가능하다.
    return f;
}
```

#### 인터페이스의 장점
두 객체 간을 돕는 중간 역할을 한다.

서로 관계없는 클래스들 간 관계를 맺어 줄 수도 있다.

⭐ 설계와 구현을 분리시켜서 클래스를 유연하고 변경에 유리하게 만든다.

⭐ 인터페이스를 사용하면 느슨한 결합이 가능하다.

```java
// 강한 결합 - 직접적인 관
class A {
    public void methodA(B b){ // B클래스와 직접적인 관계
    // 만약 class C가 새로 생기면 전체 내용을 변경해야한다.
        b.methodB();
    }
}

class B {
    public void methodB(){
        System.out.println("methodB");
    }
}

// 느슨한 결합 - 간접적인관계
class AA{
    public void methodAA(I i){ // I와 관계가 생겨서 BB와는 간접적인 관계가 된다.
    // 새로운 class C가 생겨도 AA클래스의 내용을 바꿀 필요가 없다.
        i.methodBB();
    }
}

interface I{ void methodBB(); }

class BB implements I{
    public void methodBB(){
        System.out.println("methodBB");
    }
}
```

```java
class Unit{}
class Ground extends Unit{}
class Air extends Unit{}

Interface Repariable{}
class A extends Ground implements Repariable{}
class B extends Air implements Repariable{}
class C extends Ground 

//... 생략
void repair(Repariable r){ // A, B만 가능하다.
    if(r instanceof Unit){
        //... 생략
    }
}
```

#### 디폴트 메서드
인터페이스에 새로운 추상 메소드를 추가하기 어렵다.

이 문제를 해결하기 위해서 나온 것이 디폴트 메서드 이다.

하지만 이로 인해 충돌이 발생하는데 이를 해결하는 방법은 아래와 같다.

⭐ 여러 인터페이스의 디폴트 메소드 간의 충돌
⭐ 해결 : 인터페이스를 구현한 클래스에서 디폴트 메소드를 오버라이딩하야 해결할 수 있다.

⭐ 디폴트 메서드와 부모 클래스의 메소드 간의 충돌
⭐ 해결 : 부모 클래스의 메소드가 상속되고 디폴트 메서드는 무시된다.

```java
interface Test{
    void method();
    default void newMethod(){}
}
```

### 내부 클래스 (inner class)
클래스 안에 있는 클래스를 말한다.

내부 클래스의 장점

- 내부 클래스에서 외부 클래스의 멤버들을 객체생성 없이 쉽게 접근가능하다.
- 코드의 복잡성을 줄이며 캡슐화가 가능하다.

```java
class A{ // B의 외부 클래
    int i = 1;
    B b = new B();

    class B{ // A의 내부 클래스
        // ⭐객체 생성없이 A의 멤버 접근 가능하다.
        void show(){System.out.println(i);}
    }
}
```

#### 내부 클래스의 종류와 scope는 변수와 동일하다.
```java
class Outer{
    private class InstanceIneer{} // 인스턴스 변수와 동일
    protected static class StaticInner{} // 클래스 변수와 동일

    void method(){
        class LocalInner{} // 지역 변수와 동일
    }
}
```

##### 인스턴스 클래스
주로 외부 클래스의 인스턴스 멤버들과 관련된 작업에 사용될 목적으로 선언된다.

##### 스태틱 클래스
주로 외부 클래스의 static 멤버, 특히 static 메소드에서 사용될 목적으로 선언된다.

##### 지역 클래스
외부 클래스의 메소드나 초기화블록 안에 선언하며, 선언된 영역 내에서만 사용 가능하다.

##### 익명 클래스
클래스의 선언과 객체의 생성을 동시에 하는 이름 없는 클래스이고 1회용이다.

⭐ 주의 사항 : 내부 클래스의 접근제어자는 변수에 사용 가능한 4가지 모두 사용 가능하다.

```java
class Outer{
    private int outerIv = 0;

    class InstanceInner{
        int iv = 10;
        // static int cv = 20; 불가능하다.
        // 이유는 static은 객체 생성 없이 사용해야하지만 지금은 생성해야하기 때문이다.
        final static int CONST = 100; // 상수는 가능하다.
        // 사용시 "해당 클래스명.CONST" 이렇게 접근이 가능하다.

        int iiv = outerIv; // 외부 클래스의 private 멤버도 접근 가능하다.
    }

    static class StaticInner{
        int iv = 30;
        static int cv = 40; // static 클래스는 static 멤버를 정의할 수 있다.
        // 사용시 "해당 클래스명.cv" 이렇게 접근이 가능하다.
    }

    void method(){
        int lv = 0;
        final LV = 0;

        class LocalInner{
            int iv = 50;
            // static int cv = 60; 불가능하다.
            // 이유는 static은 객체 생성 없이 사용해야하지만 지금은 생성해야하기 때문이다.
            final static int CONST = 70; // 상수는 가능하다.

            // int liv = lv; 불가능하다.
            // 이유는 내부 클래스의 객체가 메소드안에 있는 지역변수보다 더 오래 존재할 수 있기 때문이다.
            // 하지만 jdk 1.8부터는 값이 변하지 않으면 상수 취급하기 때문에 가능하다.
            int liv2 = LV; // 가능하다.
        }
    }
}
```

### 익명 클래스
이름이 없는 일회용 클래스이며 정의와 생성을 한번에 한다.

```java
new 조상클래스이름(){
    //...
}

new 구현인터페이스이름(){
    //...
}

class Test{
    Object iv = new Object(){void method(){}}; // 익명 클래스
    static Object cv = new Object(){void method(){}}; // 익명 클래스

    void method(){
        Object lv = new Object(){void method(){}}; // 익명 클래
    }
}
```
