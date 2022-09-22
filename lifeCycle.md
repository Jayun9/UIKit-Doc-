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






