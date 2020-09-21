# ios_Interview

1. 얼마나 자기가 사용하는 코드에 대해서 명확한 기준을 가지고 짜는가 -> 아주 간단하게는 이럴땐 이프문, 이럴땐 가드문
```
if 문: 해당 조건에 맞으면 블럭내의 구문을 실행합니다 
guard 문: else구문이 반드시 필요하다는 점, 참일때의 실행 코드 블럭이 없다는 점입니다
guard구문은 후속 코드가 실행되기전 조건을 만족하는지 확인하는 용도로 쓰임
특정조건을 만족하지 않고 후속코드를 실행하지 못하도록 오류발생을 예방하는 코드로 사용

**guard문의 장점** 
1> 코드의 중첩을 막아준다
2> guard구문을 많이 사용해도 코드의 depth가 깊어지지 않는다
```

2. 우리 화사랑 잘 맞을 사람인가 -> 코드레벨이나 성향?등

<hr>

- Swift 접근제어자: open, public, interal, fileprivate, private
- 외부 프레임워크에서 모듈로 클래스를 가져와서써야되는데 접근제어자를 뭘 써야하는지 > open? 
- 접근제어자에 대해서 설명해주세요 -> 접근제어자를 잘 지켜야하는 이유가 뭔가요? -> 그러면 다이나믹 디스패치 관련해서 설명해줄수 있나요? (잘모름)
```
1. open: 외부의 다른 모듈이 import 해서 접근 가능하다. 심지어 import하는 외부 모듈안에서 subclass와 override도 가능
2. public: 외부 모듈이 import해서 접근 가능하지만, subclass와 override는 오로지 자신의 모듈 안에서만 가능
3. internal: 자신의 모듈 안에서만 접근 가능하고 외부 모듈에서는 접근 불가하다. 한마디로 프로젝트 내부용이다. 
4. fileprivate: 같은 Source file안에서만 접근 가능하다. 
즉, .swift라는 파일 안에서 fileprivate인 함수가 있다면 해당 swift파일안에서는 접근이 가능하지만, 같은 프로젝트의 다른 swift 파일에서는 접근이 불가능하다.
5. private: 함수 안에서 private으로 선언된 변수는 해당 함수안에서, class안에서 private으로 선언된 변수는 해당 class 안에서만 접근이 가능하다.

접근제어자를 잘 써야하는 이유
> 데이터 은닉화 
> 코드의 구현 세부사항을 숨기고, 해당 코드를 접근하고 사용 할 수 있는 기본 인터페이스를 지정 할 수 있음
```

++ 모듈
```
코드의 묶음 단위로 프레임워크, 라이브러리, 어플리케이션처럼 배포할 코드들의 묶음을 나타낸다. 
즉 하나의 프레임워크는 하나의 모듈이고 우리가 Xcode로 만드는 프로젝트 역시 하나의 모듈이며 import를 통해 외부 모듈을 우리의 프로젝트(모듈)에서 사용
```


- Array dictionary는 값 참조타입중 뭔가요: 값타입 아닌가? / 배열이랑 딕셔너리는 어떤 타입인지
```
array, set, dictionary 모두 컬렉션 타입
- array: 정렬된 값을 정장하는 컬렉션
- set: 고유한 값을 가지는 정렬되지 않은 컬렉션
- dictionary: 키-밸류로 연결된 정렬되지 않은 컬렉션 

이 컬렉션타입은 항상 저장할 수 있는 값과 키의 타입이 명확하기에 실수로 잘못된 타입의 값을 삽입하는것은 불가능하다.
즉 컬렉션으로부터 가져오는 값의 타입에 대해 확신할 수 있다. 
```

++ 스위프트에서 array와 dictionary는 어떤 타입인가요? : 값타입 <br>
-> 그러면 a,b,c,d 배열을 계속 할당하면 복사할때마다 메모리도 계속할당되나요 : 넹 실제 메모리상 순차적으로 저장<br>
-> 그러면 언제 다른 사본이 생기죠? 스택영역에 바로 생기나요? : 넹 <br>
-> 그럼 벨류타입을 쓰게되면 메모리에 굉장히 손해를 보겠네요? : 손해를 보는데 그래봤자, Swift에 값타입은 String뿐이라.
```
문서 왈 

Swift에서 Array, String 및 Dictionary는 모두 값 유형입니다. 
그들은 C의 단순한 int 값처럼 작동하며 해당 데이터의 고유한 인스턴스 역할을 합니다. 
다른 코드가 뒤에서 해당 데이터를 수정하지 못하도록 하기 위해 명시적 사본 만들기와 같은 특별한 작업을 수행 할 필요가 없습니다. 
중요한 것은 동기화없이 스레드간에 값 복사본을 안전하게 전달할 수 있다는 것입니다. 
안전성 향상의 정신으로이 모델은 Swift에서보다 예측 가능한 코드를 작성하는 데 도움이됩니다.
```

- 값타입 참조타입 차이
```
Value: 데이터를 전달할 때 값을 복사하여 전달
Reference: 데이터를 전달할 때 값의 메모리 위치를 전달 > 단순히 참조값을 전달
```

++ Value 타입과 Referense 타입에 대해서 설명해주세요. <br>
-> 값 타입은 메모리 어느 영역에 할당되고 참조 타입은 메모리 어느 영역에 할당되나요? <br>
-> 그러면 레퍼런스 타입의 주소는 어디에 할당되나요?
```
Struct 인스턴스로 만들어진 녀석들을 STACK, CODE 영역에 저장된다.
이유는 Struct는 값 타입이라서, 기본적으로 Struct 인스턴스를 생성할때, 인스턴스의 값을 다른 공간에 새롭게 복사해서, 복사된 인자를 전달
그렇기 때문에 기본적으로 Stack에 쌓이게되지만, Struct의 값이 커지게 되면 Heap 영역에 저장 되기도 함

Class Instance 는 HEAP 영역에, 그 인스턴스의 주소값(이 인스턴스가 가리키는 ‘값’)은 Stack 영역에 쌓임
하지만 엄밀하게 얘기하면 Swift의 모든 타입은 변수들은 heap 저장되어서 참조 타입이다. 
사실 내부적으로 Struct도 어딘가를 참조하고 있다고 합니다. 그래서 엄밀하게는 Swift의 모든 녀석들은 참조 한다고 할수있다.
Class Instance 는 HEAP 영역에, 그 인스턴스의 주소값(이 인스턴스가 가리키는 ‘값’)은 Stack 영역에 쌓임

> 값 타입과 참조 타입 두개로 나누어서 생각하기 보다는, 
참조 할때는, Heap 영역에 있는 어떤 ‘값’을 바라보고 있고, 
값으로서 사용될떄는 Stack Frema 안에서 사용 되어 진다고 생각하자.
```

- 구조체는 언제 사용하나?
```
1. 연관된 몇몇의 값들을 모아서 하나의 데이터타이으로 표현하고 싶을때
2. 다른 객체 또는 함수 등으로 전달될 때 참조가 아닌 복사를 원할때
3. 자신을 상속할 필요가 없거나, 자신이 다른 타입을 상속받을 필요가 없을 때
```

- defer 함수의 의미
```
현재 코드 블록을 나가기 전에 꼭 실행해야 되는 코드를 작성하여 코드가 블록을 어떻게 빠져 나가든 꼭 마무리해야 되는 작업을 할 수 있게 도와준다.
중요한 부분은 실행순서로 defer는 선언 된 역순으로 실행된다.
그런데 무조건 defer를 선언한다고 100% 호출을 보장하지는 않는다.

1. throw를 이용해서 오류를 던질 경우
2. guard 문을 사용하여 중간에 함수를 종료하는 경우
3. 리턴값이 Never(비반환함수)인 경우
```
```swift 
func test() {
    defer {
        print("test function end")
    }
    print("Hello world")
}
```
실행결과
```
Hello word
test function end
```

- iOS VIEW LAYER
```
<참고>
1. 저수준의 프래임워크일수록 보다 많은 기능을 제공하지만 전체적인 코드량이 많다
2. 고수준의 프래임워크일수록 저수준보다 유연성은 떨어지지만 사용이 간편하고 코드량이 적다
3. Core Graphics -> Core Animation -> UIKIt, AppKit 순으로 발전했고 iOS 앱 개발시 해당 프래임워크들을 필요한 기능에 따라 선택적으로 사용할 수 있다.

UIView 와 CALayer
UIView 는 UIKit 에서 제공하는 클래스이고 CALayer 는 Core Animation 에서 제공하는 클래스이다. 
CALayer 가 UIKit 보다 한 단계 낮은 수준의 인터페이스를 제공하기 때문에 UIKit 보다 많은 기능을 제공하지만 몇가지 기능에 대해서는 직접 구현해하는 번거로움이 있다.

1. UIView
메인 쓰레드에서 CPU 를 사용해 UI 를 그림
Auto Layout 을 이용해 UI 제작 가능
단순한 애니메이션이나 퍼포먼스에 대한 요구가 크지 않을 때 사용할 수 있다

2. CALayer
별도의 쓰래드에서 GPU 를 사용해 UI 를 직접 그림
UIView와 달리 별도의 Responder 가 없어 유저 인터렉션 관련 기능은 직접 구현 및 설정해야함
복잡한 애니메이션, 퍼포먼스 등이 필요할 때 UIView 대신 사용할 수 있다
```

++ 그러면 사용자 이벤트는 어떤 객체가 관리하나요?: (UIResponder)

- 뷰 컨트롤러 라이프사이클
```
0. loadView: 화면에 띄워줄 view를 만드는 메소드로 view를 만들고 메모리에 올린다 > 실제로 해당 함수는 사용자가 직접 호출하여 사용하는 경우는 없다. 
1. viewDidLoad: 뷰의 컨트롤러가 메모리에 로드된 후 호출되며 시스템에 의해 자동으로 호출된다.
>  사용자에게 화면이 보여지기 전에 데이터를 뿌려주는 행위에 대한 코드를 작성하면 되고, 일반적으로 리소스를 초기화하거나 초기화면을 구성하는 용도로 자주 쓰인다. 
이 메소드는 view controller 생에 단 한번만 호출이 되기 때문에 한번만 있을 행위에 대해서는 이 메소드 안에 정의해주면 된다.
2. viewWillAppear: 뷰 컨트롤러의 화면이 올라오고 난 후 뷰가 화면에 나타나기 직전에 호출이 된다.
> 뷰가 로드된 이후 눈에 보이기 전에 컨트롤러에게 알리는 역할을 한다. 다른 뷰로 이동했다가 되돌아올때 재 호출되는 메소드로 화면이 나타날때마다 수행해야하는 작업을 정의하기 좋다
3. viweDidAppear: view가 데이터와 함께 완전히 화면에 나타난 후 호출되는 메서드이다.
즉, 뷰가 나타났다는 것을 컨트롤러에 알리는 역할로 뷰가 화면에 나타난 직후에 실행되며 화면에 적용될 애니메이션을 그려준다.
4. viewWillDisAppear: 다음 view controller화면이 전환하기 전이나 view controller가 사라지기 직전에 호출되는 메서드이다.
5. viewDidDisAppear: view controller들이 화면에서 사라지고 나서 호출되는 메서드이다. 화면이 사라지고나서 필요없어지는(멈춰야하는) 작업들을 여기서 진행한다.
```

++ 뷰컨트롤러 생명주기 > 그럼 didload가 실행되는 시점이 정확히 언젠가요?
```
뷰의 컨트롤러가 메모리에 로드된 후 호출
사용자에게 화면이 보여지기 전에 데이터를 뿌려주는 행위에 대한 코드를 작성
리소스를 초기화하거나 초기화면을 구성하는 용도
``` 

- 델리게이트랑 노티 차이
```
1. delegate
-  protocol 을 정의하여 사용
- 매우 엄격한 Syntax로 인해 프로토콜에 필요한 메소드들이 명확하게 명시됨
- 로직의 흐름을 따라가기 쉬움
- 많은 줄의 코드가 필요
- delegate 설정에 nil이 들어가지 않게 주의해야함. 크래시를 일으킬 수 있음
- 많은 객체들에게 이벤트를 알려주는 것이 어렵고 비효율적임(가능은 하지만)

2. notification
- Notification Center 라는 싱글턴 객체를 통해 이벤트들의 발생 여부를 옵저버를 등록한 객체들에게 Notification을 post 하는 방식
- 많은 줄의 코드가 필요없이 쉽게 구현이 가능
- 다수의 객체들에게 동시에 이벤트의 발생을 알려줄 수 있음
- 추적이 쉽지 않을 수 있음
- Notification post 이후 정보를 받을 수 없음
```


- 앱 상태에 대해서 설명
[요거 참고해보기](https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-%EC%95%B1-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0-878dfe51d182)
```
1. Not running(Unattached): 앱이 실행되지 않았거나 시스템에서 종료됨
2. In-Active: 앱이 Foreground에서 실행중이지만, 이벤트를 받을 수 없음 > 이 상태에 잠시 머물다가 다른 상태로 전이됨
3. Active: 앱이 화면에 떠 있을 때의 상태 > 이벤트를 받을 수 있음
4. Background: 앱이 백그라운드에서 코드를 실행중. 대부분의 앱은 일시중지 상태로 잠시 이 상태가 된다. 
그러나 추가 시간을 요청하는 앱은 일정기간 동안 이 상태로 남아있을 수 있다. 또한 백그라운드로 직접 실행되는 앱은 비활성 상태 대신 이 상태로 전환된다
5. Suspended: 앱이 백그라운드에 있지만 코드를 실행하지 않음. 시스템은 앱을 자동으로 이 상태로 이동시키고 그렇게 하기 전에 앱에 알리지 않는다.
일시 중지 된 앱은 메모리에 남아는 있지만 코드는 실행되지 않는다. 메모리 부족상태가 발생하면 시스템은 예고없이 일시 중단 된 앱을 제거하여 메모리를 확보한다.

<참고> app lifecycle
1. main 함수 실행
2. main 함수는 UIApplicationMain 함수를 호출
3. UIApplicationMain함수는 앱의 본체에 해당하는 객체인 UIApplication 객체를 생성
4. nib 파일을 사용하는 경우나, Info.plist 파일을 읽어들여 파일에 기록된 정보를 참고해 그 외에 필요한 데이터를 로드
5. App Delegate 객체를 만들고 앱 객체와 연결해 Main를 만드는 등 실행에 필요한 준비
6. 실행 완료를 앞두고 앱 객체가 App Delegate에게 application:didFinishLaunchingWithOptions: 메시지를 보냄
```

- 백그라운드 상태에서 코드 동작하게 하려면 어떤 함수 써야 하는지 > 이거 모르겠음 
```
위치정보 가져오는건 manager따로 있고 
beginBackgroundTaskWithName쓰면 백그라운드 가도 어느정도 시간동안 작동하게 할 수있음

정확한건 면접상황에서 질문이 어떤 상황인지 보고 판단하는게 맞는듯
```

<hr>

- 큐는 무엇일까요
```
FIFO 
데이터가 들어가는 곳과 나가는 곳이 다른 것 (중간에 들어갈 수 있는 곳도 없다)

iOS에서의 Queue
(DispatchQueue) 혹은 OperationQueue
> 실행할 작업을 생성한 뒤 Queue에 추가하면 작업에 맞는 스레드를 생성해 실행하고 작업이 끝나면 종료
> 들어온 순서대로 실행되니까 
```

- Http 메소드
```
클라이언트가 웹 서버에게 사용자 요청의 목적/종류를 알리는 수단으로
1. get: 서버에게 리소스를 보내도록 요청하는데 사용
2. head: get과 동일하지만 서버에서 body를 return 하지 않음
> 리소스 받지않고 오직 찾기만 원할때 사용
3. put: 서버에 문서를 쓸때 사용(get과 반대)
4. post: 서버에 input data를 보내기 위해 html form에서 많이 사용
5. trace:
6. option:
7. delete: 요청 리소스를 삭제하도록 요청
```

- Post put 차이
```
POST는 보통 INSERT의 개념으로 사용되고, PUT은 UPDATE개념으로 생각하면 이해하기 쉽다.
post는 서버에 데이터를 보내기 위한 용도이지만 put은 서버의 리소스에 데이터를 저장하기 위한 용도이다.
동일한 자원을 여러번 POST 하면 서버자원에는 변화가 생기지만, 여러번 PUT하는 경우는 변화가 생기지 않는다.

POST의 경우 클라이언트가 리소스의 위치를 지정하지 않는 경우 사용된다.
반면 PUT의 경우는 클라이언트가 명확하게 리소스의 위치를 지정한다.
```

++ 그렇다면 put과 patch의 차이
```
PUT이 해당 자원의 전체를 교체하는 의미를 지니는 대신, PATCH는 일부를 변경한다는 의미를 지니기 때문에 최근 update 이벤트에서 PUT보다 더 의미적으로 적합하다고 평가받고 있다.
```

- ARC에 대해서 설명해주세요 / 약한 참조랑 반대? -> 그러면 언제 ARC에서 메모리를 할당/해제 / strong weak unowned <br>
[해당 블로그 참고](https://velog.io/@cskim/ARCAutomatic-Reference-Counting)
```
컴파일 시점에 참조 횟수를 추적하여 자동으로 메모리를 관리해 주는 방법

Class instance나 함수 등 참조 타입의 값들은 메모리의 heap 영역에 저장됨.
이 영역 저장되는 값은 명시적으로 삭제하지 않는 한 메모리에 계속 남아있기 때문에 적절한 시점에 메모리에서 삭제하지 않으면 메모리의 낭비로 이어짐.
그래서 용량이 작고 한정된 메모리 자원을 효율적으로 사용하기 위해 더 이상 사용되지 않는 값들은 
메모리에서 해제시키고 그 공간을 또 다른 데이터를 저장하는데 사용하기 위해 메모리 관리가 필요.

메모리 관리를 잘 하지 못하면,
용하지 않는 데이터가 메모리 공간을 계속 차지하게 되는 메모리 누수(Memory Leak) 문제가 발생하거나
이미 해제된 주소로 메모리에 접근하여 발생하는 고아 포인터(Dangling Pointer) 문제가 발생

할당: class instance 등의 참조 타입 값을 변수에 할당할 때 증가
> 메모리의 heap 영역에 저장되어 있는 instance meta data의 주소값이 변수에 할당되는 시점이 참조 카운트가 증가하는 시점
해제: instance를 참조하던 stack 영역의 변수들이 메모리에서 해제될 때 참조 카운트도 감소 
- 변수의 생명 주기가 끝날 때
- nil이 할당될 때 
- 프로퍼티의 경우, 속해 있는 class instance가 메모리에서 해제될 때

- strong: 인스턴스의 주소값이 변수에 할당되면 참조 횟수가 증가 > 서로를 강하게 참조하여 강한참조순환 발생
- weak: instance를 참조할 때 RC를 증가시키지 않으면서 인스턴스를 참조 > 항상 옵셔널 타입의 변수(?)
- unowned: 약한 참조와 마찬가지로 RC를 증가시키지 않으면서 인스턴스를 참조
> 인스턴스를 참조하는 도중에 해당 인스턴스가 메모리에서 사라질 일이 없다고 가정하기 때문에 약한 참조와 달리 암묵적으로 옵셔널을 해제(!)하여 선언

미소유 참조는 참조하고 있던 인스턴스가 먼저 메모리에서 해제될 때 nil을 할당할 수 없어 오류를 발생시키므로 위험한 방법.
일반적으로 약한 참조만 사용해도 문제가 없기 때문에, 특별한 경우가 아니면 미소유 참조는 사용하지 않는 것이 좋음 
```

- 고차함수에는 뭐가잇는지: map, filter, flapMap, compactMap, reduce
```
sort: 정렬하여 반환 > 원본에 영향을 줌 // sorted: 기존 리스트를 건들지 않고 새로운 리스트에 정렬된 값을 반환
filter: 필터된 값을 반환
map: map은 배열 내부의 값을 하나씩 mapping / 각 요소에 대한 값을 변경하고자 할때 사용하고, 그 결과들을 배열의 상태로 반환합니다
reduce: 초기값이 있고 초기값과 첫번째 요소 ~ 끝번째 요소까지의 실행된 최종 결과값만을 반환

flatMap이 compactMap로 변경되지만, flatMap이 없어지는 것은 아님
> 일차원 배열에서는 동일한 결과를 나타냄 
flatmap: 2차원 배열을 1차원으로 flatten하게 만들고 싶을 때 사용 
compactmap: 1차원 배열에서 nil을 제거하고 옵셔널 바인딩을 하고싶을 때 사용 

// flatten: 반음 낮춤 
```

- 클로저
```
클로저: {}로 감싸진 실행가능한 코드블럭(함수는 이름 있는 클로저로 생각하면 쉬움)
함수의 이름을 지정해주지 않으며 파라미터와 반환갑을 가질 수도 있는 특징이 있다
로저의 가장 큰 특징은 간결함과 유연함
```

- OOP 객체지향 프로그래밍
[참고 블로그](https://velog.io/@hkoo9329/OOPObject-Oriented-Programming-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9D%B4%EB%9E%80)
```
C언어같은 절차 지향적인 프로그래밍이 아닌 객체의 관점에서 프로그래밍
객체들의 유기적인 관계를 통해서 프로세스가 진행
애플리케이션을 구성하는 요소들을 객체로 바라보고, 객체들을 유기적으로 연결하여 프로그래밍 하는 것을 말함
// 절차 지향 프로그래밍은 프로세스가 함수 단위로 순서대로 진행

- 캡슐화: 하나의 객체에 대해 그 객체가 특정한 목적을 위한 필요한 변수나 메소드를 하나로 묶는 것을 의미 > 데이터 은닉 
- 추상화: 목적과 관련이 없는 부분을 제거하여 필요한 부분만을 표현하기 위한 개념
- 다형성: 다형성은 형태가 같은데 다른 기능을 하는 것을 의미한다(같은 동작이지만 다른 결과물이 나올때 다형이라고 생각하면 된다)
```

- 오버라이딩과 오버로딩의 차이점
[참고 블로그](https://java119.tistory.com/32)
```
둘은 우선적으로 다형성을 지원하기 위한 방식들이라는 공통점을 가짐 

- 오버라이딩: 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의해서 사용
- 오버로딩: 같은 이름의 메서드를 여러개 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술
```

- POP 프로토콜 지향 
```
클래스를 통해 기능적으로 하나의 원본을 여러군데에서 사용해야하는 경우도 있지만, 
멀티쓰레드 환경에서는 한 원본을 두고 여러작업이 동시에 진행되게 되면 원본 데이터가 꼬일 가능성이 크기때문에 
하나의 원본으로 작업해야할 필요가 없다면 가급적으로 값 타입인 구조체나 열거형을 사용하는 것을 권장한다.
```

- 프로토콜 지향 프로그래밍을 추구하는 이유
```
1. 구조체, 클래스, 열거형 등 구조화된 타입 중에 상속은 클래스 타입에서만 가능하다.
클래스는 참조 타입이므로 참조 추적에 비용이 많이 발생한다. 
비교적 비용이 적은 값 타입을 활용하고 싶어도, 상속을 할 수 없으므로 때마다 기능을 다시 구현해 주어야 했지만, 
프로토콜 지향 프로그래밍은 그 한계를 없앴다. 즉 이를 통해 상속이 필요한 프로그램을 짤때에도 class가 아닌 struct, enum을 사용할 수 있도록 해준다.

2. 기능의 모듈화가 더욱 명확해진다
클래스가 상속을 할 수 있도록 설계되어 있다고 하더라도 다중상속을 지원하는 언어는 많지 않다. 
다중상속을 지원하지 않는다는 뜻은 하나의 상속체계에서 다른 상속체계에 속해있는 기능을 끌어다 쓸 수 없다는 뜻인데, 
프로토콜 지향 프로그래밍은 기능을 프로토콜이라는 단위로 묶어 표현하고 초기 구현을 해 둘 수 있으니 상속이라는 한계점을 탈피할 수 있다. 
따라서 OOP처럼 수직적인 확장구조가 아닌 수평적인 확장구조의 형태를 띄게 된다. 이는 곧 이것저것 제약없이 필요한 기능을 가져와 쓸 수 있음을 의미한다.

더 나아가 class는 모든 api에 접근이 가능한 반면 Protocol은 정의한 api만 가져오게 된다. 이는 곧 더 가볍고 보안성 높게 코드를 짤 수 있음을 의미한다.
```

나는 코어데이터 해서 코어데이터 관련 질문 > 깃헙 실습해봄 <br>

- 코어데이터랑 에스큐엘라이트 차이 > 왜 그걸 사용을 선택하는지
```
코어데이터는 객체 그래프를 관리하기 위한 프레임워크이고 SQLite는 관계형 데이터베이스
즉, 코어데이터 그 자체는 데이터베이스가 아니다.
```

- 에러코드에 대해서 설명해보세요. (200, 300, 400, 500)
```
200: 성공
300: 리다이렉션
400: 클라이언트 요청 오류(접근거부, 인증실패 등) > 내 잘못
500: 서버 실행 오류 > 서버잘못
```

- 리다이렉트
```
클라가 서버에 요청 > 서버는 요청에 대한 응답 > 클라에게 새로 요청할 곳을 알려주면서 다시 요청
```

- 암호화 방식 공개키 대칭키 차이
```

```
1. 암호화 방식에는 뭐가 있을까요?  (공개키와 대칭키 설명함)
2. 공개키와 비공개키를 만드는 방식
3. HTTPS에서 공개키 암호화 방식이 어떤 방식으로 사용되나요? (그림으로 설명해보세요)
4. 그러면 공개키는 누가 가지고 있고 개인키는 누가 가지고 있나요? (브라우저와 웹서버, 인증기관 세가지를 바탕으로) 진짜 열라열라 헤멤… -> 그럼 개인키를 웹서버가 가지고 있으면 사용자도 가지고 있나요>?
5. 그러면 SSL 인증서안에는 뭐가 들어있나요?
6. 그러면 웹서버에는 인증키 없나요?
7. 그러면 공개키를 브라우저가 가지고 있으면 어떻게 
== 죽을 것 같다 ==

- GCD란?
```
GCD는 백그라운드에서 스레드를 관리하면서 동시적으로 작업을 실행시키는 저수준 API를 제공하는 라이브러리

Dispatch Queues: 디스패치 큐는 FIFO 순서로 작업을 실행시키는 역할을 담당
Serial Dispatch Queue: 시리얼 디스패치 큐는 한번에 한 작업만 실행
Concurrent Dispatch Queue: 컨커런트 디스패치 큐는 시작한 작업이 끝나는것을 기다리지 않고 가능한 많은 작업을 실행
Main Dispatch Queue: 앱의 메인 스레드에서 작업을 실행할 수있는 전역에서 사용가능한 시리얼 큐

Main Queue: 메인 스레드(UI 스레드)에서 사용 되는 Serial Queue로 모든 UI 처리는 메인 스레드에서 처리를 해야한다.
Global Queue: 편의상 사용할수 있게 만들어 놓은 Concurrent Queue로 Global Queue는 처리 우선 순위를 위한 
qos(Quality of service) 파라메터를 제공하여 병렬적으로 동시에 처리를 하기때문에 작업 완료의 순서는 정할수 없지만 우선적으로 일을 처리하게 할수 있다.

sync는 동기 처리 메소드로 해당 작업을 처리하는 동안 다음으로 진행되지 않고 계속 머물러 있다.
async는 비동기 처리 메소드로 sync와는 다르게 처리를 하라고 지시후 다음으로 넘어가 버린다.

보통 스레드 처리를 하는 작업들은 시간이 꽤나 걸리는 큰 작업이거나 언제 끝날지 알수 없는 작업에 사용 되는데 (ex: 네트워크, 파일로딩) 
작업이 처리 되는동안 아무것도 하지 못하고 멈춰 있으면앱이 렉이 걸리거나 아무 반응이 없는거처럼 보인다. 
그래서 보통 동기 처리 메소드인 sync는 잘 사용하지 않는다.
```

- Swift에서 멀티스레딩을 할때는 어떤 것을 사용하나 (gcd, operation queue) -> 두 개 차이점 설명 -> 둘 다 써봄? (Op 안써봄)
```
1. Operation Queue
> 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용하는 데 적합. KVO(Key Value Observing)를 사용해 작업 진행 상황을 감시하는 방법이 필요할 때도 적합.
(Operation Queue 는 작업의 실행 순서를 결정할 때에 다른 요인들을 고려)
2. GCD
작업이 복잡하지 않고 간단히 처리하거나 특정 유형의 시스템 이벤트를 비동기 처리할 때 적합. 예를 들면 타이머, 프로세스 등 관련 이벤트.
(디스패치 대기열은 항상 FIFO - First in First out 순으로 작업 실행)
```

- 프로세스와 스레드 간에 메모리 영역 측면에서 다른점 설명해달라 -> 스택영역 공유하지 않는 이유에 대해서 설명해달라
```
프로세스는 완벽히 독립적이기 때문에 메모리 영역(Code, Data, Heap, Stack)을 다른 프로세스와 공유를 하지 않지만, 
쓰레드는 해당 쓰레드를 위한 스택을 생성할 뿐 그 이외의 Code, Data, Heap영역을 공유한다.

> 스택은 함수 호출 시 전달되는 인자, 되돌아갈 주소값 및 함수 내에서 선언하는 변수 등을 저장하기 위해 사용되는 메모리 공간이다. 
따라서 스택 메모리 공간이 독립적이라는 것은 독립적인 함수 호출이 가능하다는 것이고, 이는 독립적인 실행 흐름이 추가되는 것이다.
결과적으로 실행 흐름의 추가를 위한 최소 조건이 독립된 스택을 제공하는 것이다. 
```

++ 멀티프로세스의 문제점
```
두 개의 프로세스는 완전히 독립된 두 개의 프로그램 실행을 위해서 사용되기 때문에 컨텍스트 스위칭(프로세스의 상태 정보를 저장하고 복원하는 일련의 과정)으로 인한 성능 저하가 발생
쓰레드는 하나의 프로그램 내에서 여러 개의 실행 흐름을 두기 위한 모델이다.
쓰레드는 프로세스처럼 완벽히 독립적인 구조가 아니다. 쓰레드들 사이에는 공유하는 요소가 있다.
쓰레드는 이 공유하는 요소로 인해 컨텍스트 스위칭에 걸리는 시간이 프로세스보다 짧다.
```

- 리터럴에 대해서 설명해주세요
```
상수는 변하지 않는 변수를 의미하며(메모리 위치) 메모리 값을 변경할 수 없다 > 값이 아닌 변수 
리터럴은 변수의 값이 변하지 않는 데이터(메모리 위치안의 값)를 의미 > 변수안에 들어가는 변하지 않는 값 
```

- 이뮤타블과 뮤타블에 대해서 설명해달라 -> 그러면 멀티스레딩에서는 어떤걸 써야 안전하나?<br>
그러면 개발하면서 동기화처리 해본적있나?(동기화는 없고 싱글톤은써봄) -> 그러면 싱글톤에서 외부에서 함부로 생성 못하게 하려면 뭘써야하냐 (private init)
```
- immutable: 객체 생성 후 바꿀 수 없는 객체
- mutable: 객체 생성 후 상태를 바꿀 수 있는 객체 

불변객체는 복제나 비교를 위한 조작을 단순화할 수 있지만,

참조관계에서의 가변객체는 위험함 > 참조를 통해 언제든지 객체가 변할 수 있으니 
그래서 보통 불변객체들은 객체를 복사하게 되면 객체 자체가 아닌 참조값만을 복사하고 끝낸다.
따라서 객체를 복사할 때 똑같은 값을 가진 객체가 메모리에 하나 더 생성되는 것이 아닌 
그 객체를 가리키는 포인터가 하나 더 생성이 된다고 보면 된다. 

이때의 불변 객체는 멀티스레드 관점에서 매우 유용하다
데이터가 불변객체에 저장되어 있다면 여러 스레드에 의해 이 객체 안의 데이터에 접근을 하게 되엇을 때
데이터가 변경될 우려가 없을 것이기 때무에 불변객체가 가변객체에 비해 쓰레드 안전하다고 한다.
```

- 임계 구역에 대해서 설명해달라 -> 해결방안 세마포 뮤텍스 모니터 락<br>
[블로그 읽어보기](https://www.zehye.kr/)

14. logN의 시간복잡도를 가지는 자료구조나 알고리즘에는 어떤것들이 있나요? (이진탐색트리, 비트리)
15. NlogN은 어떤 것들이 있나요? (합병정렬, 퀵정렬) -> logN과 NlogN중 어떤게 더 빠름?
16. NlogN은 어떻게 계산된 시간복잡도인지 N과 logN 나눠서 설명해달라 (합병정렬, 분할정복과정 그림 그려서 설명)

CocoaPods / Carthago / SPM > 이거 한번씩 셋업도해보래 라이브러리 관리툴

라이브러리
- coreadata
- 이미지 라이브러리 동작방식
- alamofire, realm 등 부가 질문 생각해보기 

- swift와 objective-c 의 차이
```
포인터의 유무, C와의 연동성, 옵셔널의 유무
swift 없, 브릿지를 만들어야하고 옵셔널 있
objective-c 있, 실행가능, 옵셔널 없
```

- objective-c와 objective-c++의 확장자
```
Objective-c는 .m Objective-c++는 .mm
```
<hr>

- 클로저 델리게이트 사용 시에 주의할점 (강한참조)
- 해시 함수에 대해서 설명해달라
- 다이나믹 프로그래밍에 대해 설명해달라
- 호프먼 코딩에 대해서 들어본적 있나?
- 디비 트렌젝션에 대해서 설명해달라
- AOP에 대해서 들어본적있나? (관점 지향 프로그래밍…난생 처음 들음…)
- Copy on write에 대해서 설명해주세요
- SOLID의 개념에 대해서 설명해주세요. (경력자 질문이긴 한데 신입 면접자중에 대답하시는 분들이 있다 그러니 해봐라(?????)) 
-> 단일 책임 원칙을 지키기 위해서 어떤 상황이나 Lint 사용해 보았으면 이 SRP를 위해 제약을 걸었던게 있나요?
-> 그러면 단일책임원칙을 위해 Lint를 제한한다면 어떤식으로 활용할 수 있을까요? (추가 질문있었는데 결국 모른다 함)
- 그러면 Lint말고 이번에 개발하면서 단일책임원칙을 지키기위해 염두한 부분은 무엇인가요?
