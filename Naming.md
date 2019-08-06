# Naming

## [ Class/Interface Naming Rules ]

### ✓ 특정 기능을 하는 Interface 와 이를 상속받는 클래스가 있을 경우 아래와 같은 룰을 따른다.

- Interface 에는 Api 라는 suffix 를 붙이고 클래스에는 suffix 를 붙이지 않는다.

``` kotlin
😰
internal interface TypeConverter {
  //...
}

internal class TypeConverterImpl : TypeConverter {
  //..
}

😍
internal interface TypeConverterApi {
  //...
}

internal class TypeConverter : TypeConverterApi {
  //..
}

```


## [ Variable/Method Naming Rules ]

### ✓ 상태를 나타내는 변수는 아래와 같은 룰을 따른다.

- {중요정보명사}{동사}{기타정보}{부사}

``` kotlin
😰
private var fetchedProblemList = channel.ofData().ofType<RemoteData.Problem.Fetched>

😍
private var problemListFetched = channel.ofData().ofType<RemoteData.Problem.Fetched>
```

### ✓ 참/거짓을 나타내는 변수는 아래의 룰을 따른다.

- {is|should|has|...}{중요정보명사}{동사}{기타정보}{부사}

``` kotlin 
😰
private var problemIsCorrect = true

private var isFirstTryProblemCorrect = true

private var isEnteredEssentialInformationCorrectly = true

private var problemHasInformation = true

private var playAnimation = true

😍
private var isProblemCorrect = true

private var isProblemCorrectAtFirstTry = true

private var isEssentialInformationEnteredCorrectly = true

private var hasProblemInformation = true

private var shouldPlayAnimationOnInitialDraw = true

```

## [ MVCH Rules ]

### ✓ 
