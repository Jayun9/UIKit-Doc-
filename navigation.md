# Navigation 
화면에서 화면으로 컨텐츠를 탐색할 수 있게 하는 Navigation 의 대해서 알아본다. 

## NavigationController 
계층적 콘텐츠 탐색을 위한 스택 기반 체계를 정의하는 컨테이너 뷰 컨트롤러이다. 

### Declaration
```swift
@MainActor class UINavigationController: UIViewController
```

### Overview
navigationController 는 navigation stack 이라고 하는 정렬된 배열을 사용하여 viewController 를 관리한다. 

navigationController 는 상단의 navigationBar 를 가지고 하단의 선택적으로 toolbar 를 가진다. `isToolbarHidden` 프로퍼티 속성이 false 이면 toolbar 는 최상위 viewController 에서 제공하는 내용과 유사하게 컨텐츠를 업데이트한다. 

navigationController 는 delegate 를 통해서 동작을 정의한다. 커스텀 애니메이션 방향 동작 방식등을 `UINavigationControllerDelegate` 를 따르는 delegate 객체를 통해서 정의한다.

### Navigation Controller Views
navigationController 는 컨테이너 뷰 컨트롤러이다. 다른 뷰 컨트롤러의 내용을 자체 내부에 포함한다. view 프로퍼티를 통해서 navigationController 의 view 의 접금할 수 있다. 
navigationBar 를 숨기거나 표시하려면 `isNavigationBarHidden` 속성이나 `setNavigationBarHidden(\_:animated:)` 메서드를 사용한다. 
navigationController 는 탐색 항목의 관련된 UINavigationItem 를 사용하여 navigationBar 의 콘텐츠를 동적으로 빌드한다. navigationBar 의 전체 모양을 커스텀하려면 `UIAppearanceAPI` 를 사용하면 된다. 

### Updating the navigation bar 
최상위 뷰가 업데이트 될 때마나 navigationController 는 navigationBar 를 업데이트 한다. nnavigationBar 의 left, middle, right 를 `UIBarButtonItem` 인스턴스를 사용해서 구성할 수 있다. 
(navigationBar 는 `UIBarButtonItem` 로 구성된다. `navigationItem` 은 navigationController 의 하위 viewController 에서 navigationBar 에 접근할수 있게 해주는 옵셔널한 프로퍼티이다. 만약 navigationController 를 사용하지 않는데 navigationItem 을 강제 언래핑 해서 사용하면 런타임 에러가 발생할 수 있다.)
navigationBar 의 titnColor 를 통해서 navigationBar item 의 색상을 변경하고, navigationBar 자체의 색은 barTintColor 를 통해서 변경한다. 

### Displaying a toolbar
navigationController 는 자식 뷰 컨트롤러의 toolbar 를 관리한다. 
toolBar 는 기본적으로 숨겨져 있지만, `setToolbarHidden(\_:animated:)` 메서드를 호출하여 표시할 수 있다.
