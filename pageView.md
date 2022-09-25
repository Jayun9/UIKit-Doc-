# UIPageViewController

자식 뷰 컨트롤러 간의 컨텐츠 페이지 노출을 관리하는 컨트롤러이다.

정의

```swift
@MainActor class UIPageViewController: UIViewController
```

보여질 컨텐츠를 선택하기 위해서는 `setViewControllers(_:direction:animated:completion:)` 을 사용한다. 데이터 기반으로 보여질 컨텐츠를 설정할때에는 `data source` 를 사용한다. `data source` 는 `UIPageViewControllerDataSource` 프로토콜을 준수해야 한다. 또한, `UIPageVicewControllerDelegate`프로토콜을 준수하는 대리자 개체를 통해서 제시처 시작이나 전환에 대한 정보를 받을 수 있다.

## 생성자

```swift
init(
	transitionStyle style: UIPageViewController.TransitionStyle,
	navigationOrientation: UIPageViewController.NavigationOrientation,
	options: [UIPageViewController.OptionsKey: Any]? = nil)
```

### Parameters

- style : 화면 전환 효과
  - pageCurl : 페이지 말림 효과 (책 넘기는 효과)
  - scroll : 스크롤
- navigationOrientation : page 방향
- options : 옵션

### Return Value

UIPageViewController 인스턴스

## addChild(\_:)

지정된 뷰 컨트롤러를 현제 뷰 컨트롤러의 자식으로 추가한다. 자식 뷰 컨트롤러의 뷰를 현재 뷰 컨트롤러의 컨텐츠에 포함할 때 사용한다. 이미 추가되어 있는 경우는 제거하고 추가한다.

```swift
func addChild(_ childController: UIViewController)
```

### Parameters

- childController : 자식 컨트롤러로 추가될 컨트롤러

## didMove(toParent:)

컨테이너 뷰 컨트롤러에서 (`UIViewController`, `PageViewController`, `TabBarController` ) 뷰 컨트롤러가 추가되거나 제거된 후 호출된다.
뷰 컨트롤러는 컨테이너에 추가되는 것에 반응하려고 할 때 이 메서드를 재정의할 수 있다. 만약 addChild 를 통해 자식 뷰 컨트롤러를 추가하는 경우 didMove 메서드를 반드시 호출해야한다. 부모 컨트롤러는 addChild 알게 되는데 자식 뷰 컨트롤러 didMove 를 통해 부모 컨트롤러로 추가되는 작업이 완전히 완료되었음을 알게 된다.

```swift
func didMove(toParent parent: UIViewController?)
```

### Parameters

- parent : 부모뷰 컨트롤러, 만약 부모뷰 컨트롤러가 없으면 nil

## setViewController

표시될 뷰 컨트롤러를 설정한다.
에니메이션이 완료 된 후 표시되는 뷰 컨트롤러이다. 데이터 소스를 사용하여 사용자가 탐색할 추가 보기 컨트롤러를 제공할 수 있다.

```swift
func setViewControllers(
    _ viewControllers: [UIViewController]?,
    direction: UIPageViewController.NavigationDirection,
    animated: Bool,
    completion: ((Bool) -> Void)? = nil
)
```

### Parameters

- viewControllers : 화면에 표시할뷰 컨트롤러, 혹은 뷰 컨트롤러들
- direction : navigation 방향
  - 수평 탐색의 경우 forward 로 선택할시 오른쪽에서 왼쪽으로 바뀐다. 수직 탐색의 경우 forward 로 선택할시 하단에서 상단으로 회전한다.
  - forward
  - reverse
- animated: 전환 애니메이션 적용 여부
- 페이지 넘김 애니메이션이 완료될 때 호출되는 블록
  - 클로저 매개변수 finished : 완성 애니메이션이 끝나면 true, 스킵한 경우 false

# UIPageViewControllerDataSource

페이지 뷰의 데이터 소스 프로토콜

- `func pageViewController(UIPageViewController, viewControllerBefore: UIViewController) -> UIViewController?` : 주어진 뷰 컨트롤러 이전에 뷰 컨트롤러를 반환한다.

- `func pageViewController(UIPageViewController, viewControllerAfter: UIViewController) -> UIViewController?` : 주이진 뷰 컨트롤러 다음에 뷰 컨트로러를 반환한다.

- `func presentationCount(for: UIPageViewController) -> Int` : pageView 에 표시할 항목 수

- `func presentationIndex(for: UIPageViewController) -> Int` : 페이지 표시기에 반영할 선택된 항목의 인덱스를 반환.

# UIPageControl

각 페이지에 해당하는 가로 점을 표시하는 컨트롤이다. 사용자가 페이지 컨트롤을 탭하여 다음 또는 이전 페이지로 이동하면 컨트롤은 대리자가 처리할 `valueChanged` 에빈트를 보낸다. 그런 다음 대리자는 `currentPage` 속성을 평가하여 표시할 페이지를 결정할 수 있다. 현재 보고 있는 페이지는 흰색 점으로 표시된다.

```swift
@MainActor class UIPageControl : UIControl
```
