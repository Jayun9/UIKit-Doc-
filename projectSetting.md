# project setting

ios 프로젝트를 만들고 셋팅하는 방법에 대한 문서

## no Storyboard

storyboard 를 사용한 방법은 쉽긴 하지만 때때로 협업을 어렵게 한다.
storyboard 를 없애고 모든것을 코드로 개발하기 위한 방법을 알아본다.
다음과 같은 단계로 진행할 수 있다.

1. Remove files
   - SceneDelegate.swift 삭제
   - Main.storyboard 삭제
2. Update info.plist
   - Shift + Cmd + F -> Main 검색 (네비게이터에서 프로젝트 이름 -> UIMainStoryboardFile 클릭)
   - 검색창에서 main
   - Info.plist Values 에서 UIKit Main Storyboard Files Base Name 삭제
   - (네비게이터 에서 Info.plist -> Main 클릭)
   - Application Scene Manifest 전체 삭제
3. Update AppDelegate
   - AppDelegate.swift 에 바디 삭제

```swift
import UIKit

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        window = UIWindow(frame: UIScreen.main.bounds)
        window?.makeKeyAndVisible()
        window?.backgroundColor = .systemBackground
        window?.rootViewController = ViewController()

        return true
    }

}
```

## 단축키

- Shift + Cmd + J : 현제 작업중인 파일로 돌아간다.
- Shift + Cmd + F : 프로젝트 전체 검색
- Cmd + R : 시뮬레이터 실행
