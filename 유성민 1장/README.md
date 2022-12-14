# 모던 자바 인 액션
# 1장: 자바 8, 9, 10, 11: 무슨 일이 일어나고 있는가?

이 장의 내용
  - 자바가 거듭 변화하는 이유
  - 컴퓨팅 환경의 변화
  - 자바에 부여되는 시대적 변화 요구
  - 자바 8과 자바 9의 새로운 핵심 기능 소개

## 1.1 역사의 흐름은 무엇인가?

멀티코어 CPU  대중화와 같은 하드웨어적인 변화가 자바8에 많은 영향을 끼쳤다. 자바 8이 등장하기 전에는 나머지 코어를 활용하려면 스레드를 사용해야했다, 하지만 스레드는 관리하기 어렵고 많은 문제가 발생할 수 있다는 단점이 있다. 하지만 자바 8에서는 병령 실행을 새롭고 단순한 방식으로 접근할 수 있는 방법을 제공한다. 하지만 이 기법을 이용하려면 몇 가지 규칙을 지켜야 한다.

자바 8에서 제공하는 새로운 기능:
  - 스트림 API
  - 메서드에 코드를 전달하는 기법
  - 인터페이스의 디폴트 메서

자바 8은 병령 연산을 지원하는 스트림이라는 새로운 API를 제공한다. 이 API를 이용하면 에러를 자주 일으키며 멀티코어 CPU를 사용하는 것보다 비용이 훨씬 비싼 키워드 **synchronized**를 사용하지 않아도 된다. (멀티코어 CPU의 각 코어는 별도의 캐시를 포함하고 있다. 락을 사용하면 이 캐시들이 동기화 되어야 하므로 속도가 느린 캐시 일관성 프로토콜 인터코어 통신이 이루어진다.)

## 1.2 왜 아직도 자바는 변화하는가?

사람들은 항상 완벽한 프로그래밍 언어를 찾고자 하였고, 그런 노력이 있은후로 수천 개의 언어가 쏟아져 나왔다. 하지만 항상 새로운 언어가 등장하면서 진화하지 않은 기존 언어는 사장되었다. 자바는 1995년 첫 베타 버전이 공개된 이후로 겨쟁 언어를 대신하며 커다란 생태계를 성공적으로 구축했다. 이제 자방의 성공이 어떻게 이루어질 수 있었는지 살펴보자.

### 1.2.1 프로그래밍 언어 생태계에서 자바의 위치

자바는 출발이 좋았다.
  - 많은 유용한 라이브러리를 포함하는 잘 설계된 객체지향 언어.
  - 스레드와 락을 이용한 소소한 동시성.
  - 코드를 JVM 바이트 코드로 컴파일하는 특징 (모든 브라우저에서 가상 머신 코드를 지원하기 때문에).
  
하지만 빅데이터 시대가 오면서 병령 프로세싱을 활용해야 하는 데 지금까지의 자바로는 충분히 대응할 수 없었다.

### 1.2.2 스트림 처리

**스트림**이란 한 번에 한 개씩 만들어지는 연속적인 데이터 항목들의 모임이다. 이론적으로 프로그램은 입력 스트림에서 데이터를 한 개씩 읽어드리며 마찬가지로 출력 스트림으로 데이터를 한 개씩 기록한다. 

자바 8에는 *java.util.stream* 패키지에 스트림 API가 추가되었다. 우선은 스트림 API가 조립 라인처럼 어떤 항목을 연속으로 제공하는 어떤 기능이라고 단순하게 생각하자. 스트림 API의 핵심은 기존에는 한 번에 한 항목을 처리했지만 이제 자바 8에서는 우리가 하려는 작업을 고수준으로 추상화해서 일련의 스트림으로 만들어 처리할 수 있다는 것이다. 또한 스레드라는 복잡한 작업을 사용하지 않으면서 병렬성을 얻을 수 있다.

### 1.2.3 동작 파라미터화로 메서드에 코드 전달하기

자바 8에 추가된 두 번째 프로그램 개념은 코드 일부를 API로 전달하는 기능이다. 쉽게 말하면 자바 8에서는 메서드를 다른 메서드의 인수로 넘겨주는 기능을 제공한다. 이러한 기능을 이론적으로 **동작 파라미터화 (behavior parameterization)**라고 부른다.

### 1.2.4 병렬성과 공유 가변 데이터

세 번째 프로그래밍의 개념은 *병렬성을 공짜로 얻을 수 있다*라는 말에서 시작된다. 대신 스트림 메서드로 전달하는 코드의 동작 방식을 조금 바꿔야 한다. 보통 다른 코드와 동시에 실행하더라도 안전하게 실행할 수 있는 코드를 만들려면 *공유된 가변 데이터 (shared mutable data)*에 접근하지 않아야 한다. 이러한 함수를 **순수 함수, 부작용 없는 함수, 상태없는 함수**라 부른다. 

물론 기존처럼 **syncrhonized**를 이용해서 공유된 가변 데이터를 보호하는 규칙을 만들 수 있다, 하지만 일반적으로 synchronized는 시스템 성능에 악영향을 미친다. 

## 1.3 자바 함수

**함수 (function)** 이라는 용어는 **메서드** 특히 **정적 메서드**와 같은 의미로 사용된다.
자바의 함수는 이에 더해 수학적인 함수처럼 사용되며 부작용을 일으키지 않는 함수를 의미한다.

자바 8에서는 함수를 새로운 값의 형식으로 추가했다. 함수를 값처럼 취급한다는 특징이 어떤 장점을 제공하는지 살펴보자.

프로그래밍 언어의 핵심은 값을 바꾸는 것이다. 전통적으로 프로그래밍 언어에서는 이 값을 **일급 값 또는 시민**이라고 부른다. 그리고 자유롭게 전달할 수 없는 구조체를 **이급 시민**이라고 부른다. int, double, 등과 같은 값은 일급 시민이지만 메서드, 클래스 등은 이급 자바 시민에 해당한다. 그리하여 자바 8 설계자들은 이급 시민을 일급 시민으로 바꿀 수 있는 기능을 추가했다.

### 1.3.1 메서드와 람다를 일급 시민으로

이미 다른 언어에서 메서드를 일급값으로 사용하면 프로그래밍이 수월해진다는 사실이 입증되었다. 그래서 자바 8에서 메서드를 값으로 취급할 수 있는 기능은 스트림 같은 다른 자바 8 기능의 토대를 제공했다.

**메서드 참조 (method reference)**라는 새로운 자바 8의 기능을 알아보자.

디렉터리에서 모든 숨겨진 파일을 필터링 한다고 가정하자. File 클래스는 이미 isHidden 메서드를 제공한다. 

```java
    File[] hiddenFiles = new File(".").listFiles(new FileFilter() {
       public boolean accept(File file) {
        return file.isHidden();    //숨겨진 파일 필터링
       } 
    });
```

File 클래스가 이미 isHidden이라는 메서드를 제공하는데 왜 굳이 FileFilter로 isHidden을 복잡하게 감싼 다음에 FileFilter를 인스턴스화 해야 하는지 이해가 가지 않는다. 하지만 자바 8이 나오기 전에는 딱히 다른 방법이 없었다.

이제 자바 8에서는 아래와 같은 코드 작성이 가능하다:

```java
    File[] hiddenFiles = new File(".").listFiles(File::isHidden);
```

이미 isHidden이라는 함수는 준비되어 있으므로 자바 8의 **메서드 참조 (method reference) ::** 를 이용해서 listFiles에 직접 전달할 수 있다.
이제 자바 8에서는 더 이상 메서드가 이급값이 아닌 일급값이다!!

#### 람다: 익명 함수

자바 8에서는 메서드를 일급값으로 취급할 뿐 아니라 **람다 또는 익명 함수 (anonymous functions)**를 포함하여 함수도 값으로 취급할 수 있다.

### 1.3.2 코드 넘겨주기 : 예제

모든 녹색 사과를 선택해서 리스트를 반환하는 프로그램을 구현해보자.

자바 8 이전에는 다음처럼 구현했을 것이다.
```java
  public static List<Apple> filterGreenApples(List<Apple> inventory) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
      if ("green".equals(apple.getColor())) {
        result.add(apple);
      }
    }
    return result;
  }
```

다른 누군가가 150그램 이상으로 필터링 하고 싶다면 아마 위에 코드를 복붙해서 아래 코드로 변경했을 것이다.
```java
  public static List<Apple> filterHeavyApples(List<Apple> inventory) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
      if (apple.getWeight() > 150) {
        result.add(apple);
      }
    }
    return result;
  }
```

이제 위와 같은 코드를 자바 8에 맞게 구현해보자.

```java
  public static boolean isGreenApple(Apple apple) {
    return "green".equals(apple.getColor());
  }

  public static boolean isHeavyApple(Apple apple) {
    return apple.getWeight() > 150;
  }

  public static List<Apple> filterApples(List<Apple> inventory, Predicate<Apple> p) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
      if (p.test(apple)) {
        result.add(apple);
      }
    }
    return result;
  }
```

다음처럼 메서드를 호출할 수 있다.

```java
  filterApples(inventory, Apple::isGreenApple);

  filterApples(inventory, Apple::isHeavyApple);
```

**Predicate** - 수학에서는 인수로 값을 받아 true나 false를 반환하는 함수를 프레디케이트라고 한다. 

### 1.3.3 메서드 전달에서 람다로

메서드를 값으로 전달하는 것은 분명 유용한 기능이다. 하지만 한두 번만 사용할 메섣으를 매번 정의하는 것은 매우 귀찮다. 자바 8에서는 람다라는 새로운 개념을 이용해서 코드를 구현할 수 있다.

```java
  filterApples(inventory, (Apple a) -> GREEN.equals(a.getColor()));

  또는

  filterApples(inventory, (Apple a) -> a.getWeight() > 150);

  또는!

  filterApples(inventory, (Apple a) -> a.getWeight() < 80 || RED.equals(a.getColor()));
```

이렇게 한번만 사용할 메서드는 따로 구현할 필요가 없다.

## 1.4 스트림

스트림 API를 이용하면 컬렉션 API와는 상당히 다른 방식으로 데이터를 처리할 수 있다는 사실을 기억해두자.

컬렉션에서는 반복 과정을 직접 처리했다, 즉 for-each 루프를 이용해서 각 요소를 반복하면서 작업을 수행했다. 이런 방식의 반복을 **외부 반복 (external iteration)** 이라고 하낟.

반면 스트림을 이용하면 루프를 신경 쓸 필요가 없어진다. 스트림 라이브러리 내부에서 모든 데이터를 처리하는 이와 같은 반복을 **내부 반복 (internal iteration)** 이라고 한다. 

### 1.4.1 멀티스레딩은 어렵다

기존의 스레드 API로 멀티스레딩 코드를 구현해ㅑ서 병렬성을 이용하는 것은 쉽지 않다. 전톡적인 멀티스레딩 환경에서는 syncrhonized를 자주 활용한다, 하지만 이를 활용하더라도 많은 미묘한 버그가 발생할 수 있다. 자바 8에서는 synchronized가 필요치 않은 함수형 프로그래밍 형식의 스트림 기반 병렬성을 이용하도록 권고한다. 그래서 자바 8에서 프로그래머는 데이터 접근 방법을 제어하는 것이 아니라 어떻게 데이터를 분할할지 고민하게 된다. 그리고 바로 이러한 점이 언어를 변화하게 하는 원동력이다. 

기존의 컬렉션에서는 데이터를 처리할 때 반복되는 패턴이 너무 많았다 (filter Apples를 생각해보면 알수있다). 
따라서 이러한 반복적인 작업들:
  - 필터링 (filtering)
  - 추출 (extracting)
  - 그룹화 (grouping)
을 라이브러리에서 제공하면 좋을 것이라는 아이디어가 변화의 동기가 되었다.

또한 이러한 동작을 쉽게 병렬화 할수 있도록 하기도 하였다, CPU는 리스트의 앞부분을 처리하고, 다른 CPU는 리스트의 뒷부분을 처리하도록 요청할 수 있다. 이 과정을 **포킹 단계 (forking step)** 이라고 한다.

병렬 처리 방식의 코드를 하나 예제로 보도록 하자:

```java
  import static java.util.stream.Collectors.toList;
  List<Apple> heavyApples = inventory.parallelStream().filter((Apple a) -> a.getWeight() > 150).collect(toList());
```

자바 8은 우선 라이브러리에서 분할을 처리한다. 즉 큰 스트림을 병렬로 처리할 수 있도록 작은 스트림으로 분할한다. 

## 1.5 디폴트 메서드와 자바 모듈

자바 8, 9이전에는 인터페이스를 바꿔야 하는 상황에서는 인터페이스를 구현하는 모든 클래스의 구현을 바꿔야했다.
하지만 자바 8에서는 인터페이스를 쉽게 바꿀 수 있도록 **디폴트 메서드**를 지원한다. 

자바 8은 구현 클래스에서 구현하지 않아도 되는 메서드를 인터페이스에 추가할 수 있는 기능을 제공한다. 메서드 본문은 클래스 구현이 아니라 인터페이스의 일부로 포함된다 (그래서 이를 디폴트 메서드라 부른다). 이 방법을 활용하면 기존의 코드를 건드리지 않고도 원래의 인터페이스 설계를 자유롭게 확장할 수 있다.

예를 들어 자바 8에서는 List에 직접 sort 메서드를 호출할 수 있다. 이는 List 인터페이스에 다음과 같은 디폴트 메서드가 추가되었기 때문이다.

```java
  default void start(Comparatr<? super E> c){
    Collections.sort(this, c);
  }
```

따라서 자바 8 이전에는 List를 구현하는 모든 클래스가 sort를 구현해야 했지만 자바 8부터는 디폴트 sort를 구현하지 않아도 된다.

## 마치며

  - 프로그래밍 언어 생태계는 항상 변화하고 있다. 자바가 영원히 지배적인 위치를 유지할 수 없을수도 있다.
  - 자바 8은 프로그램을 효과적이고 간결하게 구현할수 있는 새로운 기능들을 제공한다.
  - 함수는 일급값이다, 메서드를 어떻게 함수형값으로 넘기는지, 익명 함수를 어떻게 구현하는지 기억하자.
  - 스트림과 컬렉션을 적절하게 활용하면 스트림의 인수를 병렬로 처리할수 있고 가독성도 증가시킬수 있다.
  - 디폴트 메소드를 이용해 기존 인터페이스를 구현하는 클래스를 바꾸지 않고도 인터페이스를 변경할 수 있다.