# UITextField
사용자 입력을 받아서 표시하는 View, 로그인 로그아웃 과 같은 곳에서 ID와 password 를 받는등의 작업에서 사용된다. 

## Delegate 
UITextFieldDelegate -> TextField 관련 작업을 정의하고 구현한다. 

### textFieldShouldReturn
정의 

```swift 
optional func textFieldShouldReturn(_ textField: UITextField) -> Bool
```

textField 가 return 이 눌렸을때 return 을 처리할지 여부를 결정한다. 

- parameters

textField -> 리턴이 눌린 textField 

- Return Value 
textField 가 return 에 기본동작을 구현하는 경우 true, 아닌경우 false 

textField 가 return 을 누를때마다 호출되기 때문에 return 이 눌렸을때 작업을 여기서 정의할 수 있다. 또한 return 을 눌렀을때 키보드를 닫는 등의 작업을 하고 싶다면 `resumeFirstResponder()` 메서드를 호출할 수 있다. 

### textFieldShouldEndEditing
정의 
``` swift 
optional func textFieldShouldEndEditing(_ textField: UITextField) -> Bool
```

textField 가 편집을 그만둘지 여부를 결정한다. 

- parameters
textField -> 편집이 종료될 텍스트 필드이다. 

- Return Value 
편집을 중지해야 하는 경우 true 이고 계속해야 하는 경우 false 이다. false 를 반환하면 textField 가 유효한 값이 포함될 때 까지 사용자가 다른 컨트롤로 전환 할 수 없다. 이를 활용하여 아이디 유효성 검증 같은것을 해서 사용자에게 보여주는 등의 작업을 할 수 있다. 

### textFieldDidEndEditing
정의 
```swift 
optional func textFieldDidEndEditing(_ textField: UITextField)
```

편집이 중지됬을때 호출된다. 

- parameters
textField -> 편집이 종료된 textField

- 편집이 중료됬을때 작업을 여기서 수행할 수 있다. 아이디에 유효성 검증 정보를 편집하는 중의 보여줬다가 편집이 끝나면 감추는 작업을 여기서 하면된다. 만약 `textFieldDidEndEditing(_:reason:)` 도 구현한 경우 우선적으로 이 메서드를 호출한다. 


## textField
textField 가 사용할 수 있는 메서드 

### endEditing
textField 에서 focus 가 맞춰져서 키보드가 올라가져 있는 뷰를 first Responder 라고 한다. endEditing 을 사용해서 firstResponder 를 계속 할지 여부를 결정할 수 있다. 

```swift
func endEditing(_ force: Bool) -> Bool
```

- parameters 
강제로 first responder 에서 사임하려면 true를 지정한다. 

- Return Value
뷰가 첫번째 응답자 상태를 사임하면 true 이고 그렇지 않으면 false 이다. 




