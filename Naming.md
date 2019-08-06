# Naming

## [ Class Naming Rules ]

### ✓ 

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
