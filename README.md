## [Scaffold](https://developer.android.com/jetpack/compose/layouts/material?hl=ko#scaffold) 

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

## 유용한 기능: 상태바 색상 바꾸기
```kotlin
/**
 * Theme.kt
 */
fun AppTheme(
    ...
) {
    ...
    val view = LocalView.current
    if (!view.isInEditMode) {
        SideEffect{
            setUpEdgeToEdge(view, darkTheme)
        }
    }
}

/**
 * Sets up edge-to-edge for the window of this [view]. The system icon colors are set to either
 * light or dark depending on whether the [darkTheme] is enabled or not.
 */
private fun setUpEdgeToEdge(view: View, darkTheme: Boolean) {
    val window = (view.context as Activity).window
    WindowCompat.setDecorFitsSystemWindows(window, false)
    window.statusBarColor = Color.Transparent.toArgb()
    val navigationBarColor = when {
        Build.VERSION.SDK_INT >= 29 -> Color.Transparent.toArgb()
        Build.VERSION.SDK_INT >= 26 -> Color(0xFF, 0xFF, 0xFF, 0x63).toArgb()
        // Min sdk version for this app is 24, this block is for SDK versions 24 and 25
        else -> Color(0x00, 0x00, 0x00, 0x50).toArgb()
    }
    window.navigationBarColor = navigationBarColor
    val controller = WindowCompat.getInsetsController(window, view)
    controller.isAppearanceLightStatusBars = !darkTheme
    controller.isAppearanceLightNavigationBars = !darkTheme
}
```
