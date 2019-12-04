# Naming

## [ Basic Rules ]

### ✓ 기본적으로 네이밍은 아래 룰을 따른다.

- 명령/실행 -> {동사}{중요정보명사}{부사|기타} 순으로 작성한다.

``` kotlin 
😰
private fun userDataFetch()

😍
private fun fetchUserData()
```

- 상황/이벤트/콜백 -> (on){중요정보명사}{동사}{부사|기타} 순으로 작성한다.

``` kotlin 
😰
private fun onFetchUserData()

😍
private fun onUserDataFetched()
```

### ✓ 변수명/함수명은 평서문처럼 작성하고 동사/명사/접속사/전치사 등을 적극적으로 사용해 최대한 많은 의미를 담는다.

``` kotlin 
😰
private fun calculateTransitionY(view: View): Float {} /** Not recommended */

😍
private fun calculateNodeTransitionDistanceOnFocus(focusTargetView: View): Float {} /** Recommended */

private fun calculateTransitionDistanceForNodeOnFocus(focusTargetView: View): Float {} /** Recommended */
```

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

private var shouldAnimationPlayOnInitialDraw = true
```

### ✓ ~을 해야하는가? 를 나타내는 boolean 에는 is 보다는 should 를 사용한다.

``` kotlin 
😰
private var isAnimationPlay = true

private var isPlayAnimation = true

private var playAnimation = true

private var shouldPlayAnimation = true /** 명사(Animation)를 동사(Play) 보다 먼저 쓰기를 권장 */

😍
private var shouldAnimationPlay = true
```

### ✓ ~(값)을 가지고 있는가/존재하는가? 를 나타내는 boolean 에는 is 보다는 has 를 사용한다.

``` kotlin 
😰
private var isUserIdExist = true

private var checkUserIdExist = true

if(loginData.whenUserIdExist()) {
  ...
}

😍
private var hasUserData = true

if(loginData.hasUserId()) {
  ...
}
```

### ✓ Iterable 한 데이터의 변수에는 ~s, 혹은 ~List 와 같은 suffix 붙인다.

- items 라는 변수는 최대한 지양하고 해당 데이터가 무엇인지를 나타내도록 적는다.

``` kotlin 
😰
private var product = listOf<Product>

private var items = listOf<Product>

😍
private var products = listOf<Product>

private var productList = listOf<Product>
```

### ✓ 특정 값을 읽을 때는 get, 쓸 때는 set 을 사용한다.

- 네트웍이나, 룸, 메모리캐쉬 등에서 읽을 때는 fetch, 쓸 때는 publish 를 사용한다.

``` kotlin 
😰
class User constructor(private val userName: String) {
  
    fun userName() = userName

    fun userName(userName: String) {
      this.userName = userName
    }
  
}

class Repository constructor(private val retrofit: Retrofit) {
  
    fun getUser() = retrofit.getUser()
     
    fun setUser(user: User) {
      retrofit.setUser(user)
    }
     
    fun deleteUser(user: User) {
      retrofit.deletUser(user)    
    }
  
}

😍
class User constructor(private val userName: String) {
  
    fun getUserName() = userName

    fun setUserName(userName: String) {
      this.userName = userName
    }
  
}

class Repository constructor(private val retrofit: Retrofit) {
  
    fun fetchUser() = retrofit.fetchUser()
     
    fun publishUser(user: User) {
      retrofit.publishUser(user)
    }
     
    fun publishDeleteUser(user: User) {
      retrofit.publishDeleteUser(user)    
    }
  
}
```
