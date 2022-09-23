# Life Cycle
ios 앱의 생명 주기에 대한 정리

## Responding to the launch of your app 
앱이 처음 실행될때의 작업. 앱의 데이터 구조를 초기화 하고, 앱이 실행되도록 준비하며, 시스템의 시작 시간 요청에 응답한다. 

모든 앱에는 `UIApplication` 개체가 나타내는 연결된 프로세스가 있고, 연관된 프로세스에 응답하는 (`UIApplicationDelegate`  을 준수함) 대리자 개체가 있다. 
앱을 처음 시작할때 UIKit 은 UIApplication 객체와 앱 대리자 개체를 자동으로 생성한다. 그런다음 앱의 메인 이벤트 루프를 시작한다. 

### Provide a launch storyboard 
앱이 실행되고 UI 가 준비되기 전까지 launch storyboard 를 보여줌으로써 앱이 실행됬으며 기다리는 순간 무엇인가 준비중임을 사용자에게 알린다.

```
시작화면에 정적 이미지를 사용하지 않도록 주의한다. ios 14 에상에서 시작 화면은 25MB 로 제한된다.
```

### Initialize your app's data structures
앱의 시작시 초기화를 위해 다음 두가지 메서드중 하나를 구현하거나 둘 다 구현한다. 

- `application(_:willFinishLaunchingWithOptions:)`
- `application(_:didFinishLaunchingWithOptions:)`

초기화 시에는 다음과 같은 작업을 실행한다.

- app data 초기
- 앱 실행에 필요한 리소스가 있는지 확인한다. 
- 앱을 실행하면서 해야하는 일회성 설정을 수행한다. 
- 앱에서 사용하는 모든 중요한 서비스에 연결한다. 

### Move long-running tasks off the main thread
앱의 시작하고 UI 는 `application(:didFinishLaunchingWithOptions:)` 이 반환되기 전까지 보이지 않는다. 해당 메서드나 `application(:willFinshLaunchingWithOptions:)` 같은 메서드에서 오래거리는 작업을 진행하게 되면 화면이 늦게 보이게 되고 사용자에게 안좋은 경험을 줄 수 있다. 

사용자 경험을 높이기 위해서는 초기화시에 오래걸리는 작업은 피하고, 오래걸리는 작업이 있다면 main thread 에서 벗어나 비동기로 실행하도록 한다. 

```
scene 기반 앱의 경우는 application(_:configurationForConnectiong:options:) 를 사용한다.
```

## UIApplication
ios 에서 앱이 실행되는 동안 제어하고 조정하는 기능을 담당한다. 

정의
```swift
@MainActor class UIApplication: UIResponder
```

모든 앱은 앱이 실행되면 하나의 UIApplication (드물게는 UIApplication 의 서브클래스도 갖음)  를 갖는다. 앱이 실행되면 UIApplicationMain(_:_:_:_:) 를 호출하고, 싱글톤 패턴으로 UIApplication 인스턴스를 생성한다. 

애플리케이션 객체는 들어오는 사용자 이벤트의 초기 라우팅을 처리하고, 제어 개체(UIControl) 는 전달한 작업 메ㅅ세지를 적절한 대상 개체에 전달한다. 응용 프로그램 개체는 앰의 UIView 개체를 검색하는데 사용할 수 있는 window(UIWindow) 목록을 유지 관린한다. 

UIApplication 클래스는 대신 주요 작어을 처리할 수 있는 UIApplicationDelegate 정의하고, 앱의 다양한 런타임 이벤트를 처리할 수 있는 메서드를 이곳에 제공함으로써 대응할 수 있게 한다.


## UIApplicationDelegate
앱에서 발생하는 여러 상황을 관리하는 메서드의 집합이다.

정의
```swift
@MainActor protocol UIApplicationDelegate
```

UIKit 은 UIApplication 과 함께 UIApplicationDelegate 객체를 생성해 시스템과 상호작용할 수 있도록 한다. UIApplicationDelegate 를 사용해서 다음을 다룬다.

- 데이터 구조 초기화
- scenes 구성
- 메모리 부족 경고, 다운로드 완료 알림 등 외부에서 발생하는 알림에 응답
- 앱 자체를 대상으로 한 이벤트에 응답(view 나 viewController 에 해당하지 않는)
- Apple Push Notification 서비스 등 서비스 등록

ios12 나 그 전 버전에서는 UIApplicationDelegate 를 통해서 앱의 생명주기를 관리한다. 포그라운드로 진입하거나 백그라운드로 이동할때 앱의 상테를 업테이트하는 작업을 담당하기도 한다. 

### 주요 메서드
Initialzing the App
- `func application(UIApplication, willFinishLaunchingWithOptions: [UIApplication.LaunchOptionsKey : Any]?) -> Bool` : 실행 프로세스가 시작 되었음
- `func application(UIApplication, didFinishLaunchingWithOptions: [UIApplication.LaunchOptionsKey : Any]?) -> Bool` : 실행 프로세스가 거의 완료 되었으며 앱을 실행할 준비가 거의 완료되었음을 알린다.


<br />

Responding to app life-cycle events
- `func applicationDidBecomeActive(UIApplication)` : 앱을 활성화 되었을 때
- `func applicationWillResignActive(UIApplication)` : 앱이 곧 비활성화될 때
- `func applicationDidEnterBackground(UIApplication)` : 앱이 이제 백그라운드에 있음을 대리자에게 알린다.
- `func applicationWillEnterForeground(UIApplication)` : 앱이 포그라운드로 진입하려고 한다고 대리인에게 알린다. 
- `func applicationWillTerminate(UIApplication)` : 앱이 종료되려고 할때 대리자에게 알린다.

























































