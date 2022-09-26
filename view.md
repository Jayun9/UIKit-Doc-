# UIView

## property 

### ClipsToBounds
정의
```swift
var clipsToBounds: Bool { get set} 
```

이 값을 true 로 설정하면 하위 view 의 경계가 view 의 경계에 맞게 잘린다. false 로 설정하면 프레임이 view의 보이는 경계를 넘어 확장되는 하위 view 가 잘리지 않는다. 

## transition
지정된 컨테이너 보기에 대한 전환 에니이션을 만든다. 

```swift 
class func transition(
    with view: UIView,
    duration: TimeInterval,
    options: UIView.AnimationOptions = [],
    animations: (() -> Void)?,
    completion: ((Bool) -> Void)? = nil
)
```

### Parameters
- view : 전환을 수행하는 container view 
- duration : 초단위로 측정된 전환 애니메이션의 지속시간
- options : 애니메이션을 수행하는 방버을 나타내는 옵션 마스크 
    - `UIView.AnimationOptions` 참고 
- animations : 지정된 view 의 적용하려는 클로저 
- compeletion : 애니메이션 시퀀스가 종료될 때 실행할 블록 개체이다. 인수로 애니메이션이 실제로 완료되었는지 여부를 나타내는 값을 가진다. 

### Discussion
이 메서드는 지정된 뷴의 상태 변경도 지원한다. animations 매개변수에서 지정한 블록에서 상태변경을 할 수 있다. 
