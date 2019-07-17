# General

## [ Basic rules ]

### ✓ 무엇을 선언할 때는 기본적으로 가시성이 가장 좁게 선언한다.

🌟뭐든지 우선 안되게 하고 나중에 필요시 되게하라. 🌟
- 변수/함수를 선언할 경우 습관적으로 private 를 붙여 선언하고 이후 외부에서 필요 시 public 으로 전환한다.
- 클래스의 경우 기본적으로 internal 을 붙여 선언한다.

``` kotlin
😰 
val badVarible = 0

class BadClass

😍
private val goodVariable = 0

internal class GoodClass
```

### ✓ CamelCase base

- 기본적으로 Camel case 를 사용한다.
- 하지만 아래와 같은 예외는 있다.
  - 테스트 코드의 실제 테스트 함수명은 snake case 로 사용한다.
  - ~테스트 코드는 한글로 작성할까 고려 중..~
    ``` kotlin
    fun this_function_return_true() { ... }
    ```
  - 테스트 코드 중 setUp 과 tearDown 함수는 Camel case 를 사용한다.
    ``` kotlin
    @Before
    fun setUp() { ... }
    
    @After
    fun tearDown() { ... }
    ```

### ✓ static / const 필드는 전부 대문자로 작성하며 snake case 를 사용한다.

``` kotlin
😰
companion object {
  private const val badConstVariable = 1
}

😍
companion object {
  private const val GOOD_CONST_VARIABLE = 1
}

```

### ✓ table-like line-up (tllu)

- 생성자에 arguments 가 많아져 코드가 길어질 경우 가독성을 높이기 위해 아래를 참조해 코드라인의 정렬을 맞춘다.
  - 예외) 생성자가 안의 arguments 가 1-3 개일 경우 그리고 그렇게 길지 않을 경우는 한 줄로 써도 무방하다.

``` kotlin
😰 
internal class BadLineUpConstructor constructor(private val resource: Resources, private val weakContext: WeakReference<Context>, private val repository: RepositoryApi, private val remoteAction: RemoteActionApi) : ParentClass {

😍
internal class GoodLineUpConstructor constructor(
    private val resource: Resources, 
    private val weakContext: WeakReference<Context>, 
    private val repository: RepositoryApi, 
    private val remoteAction: RemoteActionApi
    
) : ParentClass {

    ....

}
```

- 논리적으로 유사한 작업을 하는 코드라인들을 붙여서 작성할 경우 아래를 참조해 코드라인의 정렬을 맞춘다.
  - 예외) 라인사이에 공백라인이 있을 경우 tllu 하지 않는다. 즉, tllu 하기 싫다면 라인사이에 공백을 넣는다.
  
``` kotlin
😰
//case 1
private val badLineUp = PublishRelay<Int>.create()
private val badLineUpSecondRelay = PublishRelay<Int>.create()
private val badLineUpThirdRelay = PublishRelay<Int>.create()

//case 2
private val alsoBadLineUp            = PublishRelay<Int>.create()

private val alsoBadLineUpSecondRelay = PublishRelay<Int>.create()

private val alsoBadLineUpThirdRelay  = PublishRelay<Int>.create()

😍
//case 1
private val goodLineUp            = PublishRelay<Int>.create()
private val goodLineUpSecondRelay = PublishRelay<Int>.create()
private val goodLineUpThirdRelay  = PublishRelay<Int>.create()

//case2
private val alsoGoodLineUp = PublishRelay<Int>.create()

private val alsoGoodLineUpSecondRelay = PublishRelay<Int>.create()

private val alsoGoodLineUpThirdRelay = PublishRelay<Int>.create()
```

- kotlin 함수 콜에서 hint 도 아래를 참조해 정렬을 맞춘다.

``` kotlin
😰
loginRepository.requestLogin(
  id = id,
  password = password,
  token = token
)

😍
loginRepository.requestLogin(
  id       = id,
  password = password,
  token    = token
)
```

### ✓ 모든 컴포넌트 사이의 공백은 한칸을 사용한다. 두칸 이상 사용하지 않는다.

``` kotlin
😰
private val someVariable = 0
                                        /** 이곳에 공백라인이 두칸이면 */
                                        /** 안된다. */
private fun someFunction1() {
  ...
}
                                        /** 이곳에 공백라인이 두칸이면 */
                                        /** 안된다. */
private fun someFunction2() {
  ...
}

😍
private val someVariable = 0
                                        /** 한칸의 공백라인 만 !*/
private fun someFunction1() {
  ...
}
                                        /** 한칸의 공백라인 만 !*/
private fun someFunction2() {
  ...
}
```

### ✓ 불필요한 코멘트는 피한다.
 
- 아래와 같은 경우에만 코멘트를 작성하며 코멘트는 ``` // ``` 가 아닌 ``` /** ... */ ``` 를 사용한다.
  - 코드가 하는 작업이 변수명이나 메소드명만으로는 그 의미를 전달하기 매우 힘들 경우.
  - 불가피하게 매직상수를 사용하게 되어 그 상수의 의미를 전달할 필요가 있을 때.
  - 코드만으로는 설명할 수 없는 History 가 있을 경우.  (ex: 이 코드는 ~이슈 때문에 이렇게 짰고 ~해서 작동한다)
  - 일반적이지않은 데이터 처리의 경우. (ex: 이 데이터는 ~하게 오기 때문에 ~해서 처리해야한다)
    - 예) onMeaure의 parameter들은 여러 정보가 bitwise 돼 담겨오기 때문에 View.MesureSpec 로 unpack 해서 사용해야한다.

``` kotlin
😰 // Bad Comment 

😍 /** Good Comment */
```

### ✓ Numeric literal 의 suffix 는 대문자를 사용한다.

``` kotlin
😰 private val badFloat = 1f

😍 private val goodFloat = 1F
```

### ✓ 10만 이상의 Numeric literal 을 표현할 때는 underscore 를 사용한다.

``` kotlin
😰 private val badNumber = 111111

😍 private val goodNumber = 1_111_111
```

### ✓ Brace 를 최대한 사용한다.

``` kotlin
😰 
if(condition) 
  Log.d(TAG, "bad!") 
else 
  Log.d(TAG, "also bad!")

😍 
if(condition) {
  Log.d(TAG, "GOOD!") }
else {
  Log.d(TAG, "also GOOD!")
}
```

### ✓ 코드의 흐름은 가로보다는 세로의 흐름으로 작성한다.

- if, switch, when, for 문등은 가로로 한 줄로 쓰기보다는 세로로 작성한다.
- 예외) 단, rx operator, lamda/closure 에서는 *내부 로직이 한 줄로 작성이 가능할 경우* 한 줄로 작성한다.

``` kotlin
😰 
if(condition) { Log.d(TAG, "bad!") }

private val badOpeartorStyle = Observable.just(1, 2, 3)
  .filter {
    it == 1
  }
  .map {
    it + SOME_VALUE
  }
  
bad_lamda.setOnClickListener {
  doSomething()
}

😍 
if(condition) {
  Log.d(TAG, "GOOD!") }
else {
  Log.d(TAG, "also GOOD!")
}

private val goodOperatorStyle = Observable.just(1, 2, 3)
  .filter { it == 1 }
  .map { it + SOME_VALUE }
  
good_lamda.setOnClickListener { doSomething() }
```

### ✓ 메소드 어노테이션은 세로로 작성한다.

``` kotlin
😰 
@Provides @PerActivity
fun badAnnotating(): String { ... }

😍
@Provides @PerActivity
fun goodAnnotating(): String { ... }
```

### ✓ 필드 어노테이션은 너무 길어지지 않는 이상 기본적으로 가로로 작성한다.

``` kotlin
😰 
@Inject 
@field:Bad
lateinit var badAnnotating: String

😍
@Inject @field:Good lateinit var goodAnnotating: String
```

### ✓ Builder 패턴의 코드를 부를 때에는 메소드를 세번이상 부를 때 LF 한다.

``` kotlin
😰 
badBuilder.setInt(1)
  .build()
  
badBuilder.setInt(1).setBoolean(false).build()

😍
goodBuilder.setInt(1).build()
  
goodBuilder
  .setInt(1)
  .setBoolean(false)
  .build()
```

### ✓ 변수는 그 변수가 어떤 의미를 갖는 알 수 있도록 충분히 길게 짓는다. 

- 변수의 의미전달 때문에 너무 길어질 경우는 적당한 선에서 작성한다. 0~30 자 내외
- flag 라는 이름의 변수명은 절대 사용하지 않는다.

``` kotlin
😰 
private val index = 0 /** bad naming */

private val isCorrect = false /** bad naming */

private val isLoginDataAndNewUpdateCheckDataAndNextDataFetched = false /** bad naming */

private val flag = false /** bad naming */

😍
private val mainProblemIndex = 0 /** good naming */

private val isMainProblemCorrect = false /** good naming */

private val isAllDatasFetched = false /** good naming */
```

### ✓ 매직{넘버|스트링|...}(은)는 사용하지 않는다. 상수로 의미를 정의해서 쓴다.

``` kotlin
😰 
if(currentProblemNumber == 10) { /** bad magic number */
  completeLesson()
  navigateToResult()
}

if(problemType == "N") { /** bad magic string */
  hideHintTip()
}

😍
companion object {
  private const val MAX_PROBLEM_NUMBER = 10
  
  private const val NORMAL_PROBLEM_TYPE_PROVIDED_BY_SERVER = "N"
}

if(currentProblemNumber == DEFAULT_PROBLEM_NUMBER) { /** good */
  completeLesson()
  navigateToResult()
}

if(problemType == NORMAL_PROBLEM_TYPE_PROVIDED_BY_SERVER) { /** good */
  hideHintTip()
}
```

### ✓ 0부터 시작하는 변수는 index 라는 변수명 사용하고 1부터 시작하는 변수는 order 나 number 라는 변수명을 사용한다.

### ✓ if 조건에 여러개(3개 이상)의 조건이 필요할 경우 아래와 같이 작성한다.

``` kotlin
😰 
if(badIfCondition1 && badIfCondition1 && badIfCondigion2) {
  ...
}

😍
if(goodIfCondition &&
    goodIfCondition1 && 
    goodIfCondition2) {
  ...
}
```

### ✓ {outer|inner|nested|sealed}클래스/인터페이스의 시작과 끝 공백라인 첨가 여부는 아래 룰을 따른다.

- 최상위 outer 클래스만 클래스의 시작과 끝에 공백을 넣고 나머지는 공백을 넣지 않는다.

``` kotlin
😰 
internal class BadOuterClass {
  private val context: Context? = null /** 윗 라인과 공백라인이 있어야함 */
  
  class BadNestedClass {
  
    private val myVarialble: Int = 0 /** 위 아래 공백라인이 없어야 함 */
  
  } 
} /** 윗 라인과 공백라인이 있어야함 */

internal interface BadInterface {

  fun doSomething() /** 위 아래 공백라인이 없어야 함 */

}

😍
internal class GoodOuterClass { /** outer 클래스이므로 시작과 끝에 공백라인이 있음 */

  private val context: Context? = null
  
  class GoodNestedClass { /** nested 클래스이므로 시작과 끝에 공백라인이 없음 */
    private val myVarialble: Int = 0 
  }
  
}

internal interface GoodInterface { /** interface 이므로 시작과 끝에 공백라인이 없음 */
  fun doSomething()
}

internal sealed class GoodSealedClass { /** sealed class 이므로 시작과 끝에 공백라인이 없음 */
  class Class1( /** nested class 이므로 시작과 끝에 공백라인이 없음 */
    val variable: Int,
    val variable1: Int,
    val variable2: Int,
  ) : GoodSealedClass()
  
    class Class2(val variable: Int) : GoodSealedClass()
}
```

### ✓ 함수/람다|클로져의 시작과 끝에는 공백라인을 넣지 않는다.

``` kotlin
😰
private fun badFunction() {

  doSomething()

}

private fun alsoBadFunction() {

  doSomething()
}

private fun alsoAlsoBadFunction() {
  doSomething()
  
}

bad_lamda.setOnClickListener {

  doSomething()
  doNextThing()
  
}

😍
private fun goodFunction() {
  doSomething()
  doNextThing()
}

good_lamda.setOnClickListener {
  doSomething()
  doNextThing()
}
```
