# Container View Controllers
Container View Controllers 에 대해서 학습한 내용

- Whate are they?
- How do they Work?
- UINavigationController
- UITabBarController
- UIPageViewController

## Whate are they
Container View Controller 는 다른 View Controller 의 콘텐츠를 포함하거나 단일 인터페이스로 결합하는 ViewController 이다. 

## How do they Work?
View Container 안에서 다른 화면으로 이동한뒤에 다시 돌아거나, 하단 탭을바를 눌러서 다른 메뉴에 화면으로 넘어가는 것과 같은 자동할 수 있다. 

## UINavigationController
navigationController 는 화면을 탐색할 수 있게 한다. 뉴스 보기 리스트에서 아이템을 눌렀을때 뉴스의 상세 뷰로 넘어가는 등의 작업이 이에 해당한다. 가능한 작업은 크게 두가지로 나뉜다. 

- push/pop : 스택에 push pop 과 비슷하게 동작한다. 화면 전환시 push 된 화면은 이전화면에 위에 놓이게 되고, pop 하면 쌓였던 화면은 꺼내지고 이전 화면이 맨 위에 놓여서 보이게 된다. 
- presentation/dismiss : push, pop 이 이전화면을 완전히 덮는 새로운 화면을 위에 쌓는다면 presentation/dismiss 는 이전 화면 위에 새로운 창을 폴더처럼 띄어 놓는것이라 생가하면 된다. 이전 화면이 뒤에 살짝 보이게 되는데 dismiss 해서 다시 이전 화면으로 돌아갈 수 있다. modal 과 비슷하다고 생각하면 된다.

## UITabBarController
탐색할 수 있는 탭바를 생성해서 각 버튼에 화면 하나씩을 연결해 띄운다고 생각하면된다. 또한 모든 종류의 뷰 컨트롤러와 조합해서 사용할 수 있다. 네비게이션 컨트롤러가 뎁스를 늘리는 거라고 생각한다면, tabBarController 는 넓이를 늘리는 거라 생각하면 된다. 

## UIPageViewController 
온보딩 화면과 같이 뷰 컨트롤러 배열을 스와이프, 혹은 넘기는 효과로 탐색할 수 있게 한다. pageControl 를 사용하여 뷰 컨트롤러를 탐색할 수 도 있다.

## 요약 
containerView Controller 는 콘텐츠를 화면에 표시하는 방시과 콘텐츠를 분리하여 더 나은 캡슐화를 구현한다. 앱의 데이터를 표시하는 컨텐츠 컨트롤러와 달리 컨테이너 뷰 컨트롤러는 다른 뷰 컨트롤러를 표시하고 정렬하며 이들간의 탐색을 처리한다.

컨테이너 컨트롤러는 여전히 화면이면서, 자식 뷰 컨트롤러를 가짐으로써 뷰 계층을 구조를 형성한다. 

### 자식 컨트롤러 추가 
다음 단계를 따라서 child ViewController 를 추가할 수 있다. 

1. ContainerViewController 의 `addChild(\_:)` 메서드를 호출하여 자식 컨트롤러를 추가한다.
2. ContainerView 계층 구조에서 자식 controller의 view 를 subView 로 추가한다.
3. 제약 조건을 추가하여 자식 루트 뷰의 크기와 위치를 정한다.
4. 자식 뷰 컨트롤러의 `didMove(toParent:)` 를 호출하여 전환이 완료 되었음을 알린다. (컨테이너는 `addChild` 를 통해서 추가되는 사실을 알게 되고, 자식은 didMove 를 통해서 전환이 완료되었다는 것을 알게된다.)

### 자식 컨트롤러 제거
다음 단계를 따라서 childViewController 를 containerViewController 에서 제거할 수 있다.

1. 자식 뷰 컨트롤러에서 `willMove(toParent:)` 를 호출한다.
2. 자식 뷰의 루트 뷰의 대한 제약사항을 제거하거나 비활성화 한다.
3. 자식의 루트 뷰에서 `removeFromSuperview()` 를 호출하여 뷰 계층에서 제거한다.
4. 자식의 `removeFromParent()` 메서드를 호출하여 컨테이너-자식 관계의 끝을 마무리한다.


