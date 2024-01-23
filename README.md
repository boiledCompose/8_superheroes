## Scaffold

`Scaffold` 컴포저블은 다양한 구성요소와 기타 화면 요소를 위한 슬롯을 제공한다.

### contentPadding

- `Scaffold`에는 일반 `content` 후행 람다가 존재하며, 해당 람다는 콘텐츠 루트에 적용해야 하는 `PaddingValue` 인스턴스를 수신한다.

- `PaddingValue`는 상단과 하단 바가 존재하면 `content`를 오프셋하는 역할을 맡는다. 

```kotlin
Scaffold(/* ... */) { contentPadding ->
    // Screen content
    Box(modifier = Modifier.padding(contentPadding)) { /* ... */ }
}
```
<br>

### topBar & bottomBar

- `topBar`는 상단 앱 바의 슬롯을 제공하는 속성으로 `TopAppBar`를 사용할 수 있다.
- `bottomBar`는 하단 앱 바 슬롯을 제공하며 `BottomAppBar`를 사용할 수 있다.
  - `bottomBar`의 경우 `BottomNavigation`과 같은 다른 머티리얼 구성요소에 사용할 수 있다.
```kotlin
Scaffold(
    topBar = {
        TopAppBar { /* Top app bar content */ }
    },
    bottomBar = {
        BottomAppBar { /* Bottom app bar content */ }
    }
) {
    // Screen content
}
```
