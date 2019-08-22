# Kotlin code style guide

## [Class component rules]

### ✓ 클래스 내부의 요소들은 아래와 같은 정렬을 따른다.

- package + import statements
- two empty lines
- typealias definitions(if exist)
- class/interface definition
- extra constructors(if exist)
- companion object definition
- interface(callback) definition
- nested/inner class definition(if exist)
- abstract methods(if exist)
- concrete members(if exist)
- init definition(if required)
- lifecycle related methods with basic order(if required)
- concreate method
  - override
  - public
  - private
- interface/class implementation members(if exist)

``` kotlin
😍
package code.style.guide

import i.will.get.audi.r8.eventually


typealias MyCustomInt = Int

internal abstract class MyCustomLayout constructor(
    private val context: Context,
    private val attrs: AttributeSet? = null

) : FrameLayout(context, attrs) {

  constructor(context: Context, attrs: AttributeSet? = null, extra: Int) : this(context, attrs, extra)
  
  constructor(context: Context, attrs: AttributeSet? = null, extra: Int, extra1: Int) : this(context, attrs, extra)
  
  companion object {
    private const val MAX_LAYOUT_WIDTH  = 100F
    private const val MAX_LAYOUT_HEIGHT = 100F
  }

  interface Listener {
    fun onButtonClicked()
  }
  
  class ViewState(val profileImageBitmap: Bitmap, val state: Entry)
  
  sealed class Entry {
    class Open : Entry()
    
    class Lock : Entry() 
  }
  
  abstract fun hasRootView(): Boolean
  abstract fun getRootView(): View
  
  private lateinit var viewState: ViewState
  
  private var listener: Listener? = null
  
  init {
    initializeViews()
  }
  
  override fun onMeasure(widthMeasureSpec: Int, heightMeasureSpec: Int) {
    ...
    
    processMeasure()
  }

  override fun onLayout(changed: Boolean, left: Int, top: Int, right: Int, bottom: Int) {
    ...
  }

  override fun onDraw(canvas: Canvas?) {
    ...
  }

  fun setViewState(viewState: ViewState) {
    this.viewState = viewState
    
    ...
  }
  
  fun setListener(listener: Listener) {
    this.listener = listener
  }
  
  fun changeProfileImage(bitmap: Bitmap) {
    ...
  }
  
  private fun initilizeViews() {
    ...
  }
  
  private fun processMeasure() {
    processMeasureRunnable.run()
  }
  
  private val processMeasureRunnable = Runnable { ... }

}
```

## [Basic rules]

### ✓ enum 은 대문자로 시작해 camel case 를 사용한다.

``` kotlin
😰
enum BadEnum {
  BAD_ENUM,
  alsoBadEnum
}

😍
enum GoodEnum {
  GoodEnum,
  AlsoGoodEnum
}
```

### ✓ Colon(:) 은 아래의 룰에 따른다.

- 리턴 값을 의미할 경우 suffix space 만 넣고 prefix space 는 넣지 않는다.
- 상속/구현을 의미할 경우 prefix/suffix spaces 를 모두 넣는다.

``` kotlin
😰
fun bad() : String {
  return "a"
}

class Bad constructor(context: Context): FrameLayout(context)

😍
fun good(): String {
  return "a"
}

class Good constructor(context: Context) : FrameLayout(context)
```

### ✓ 생성자는 아래와 같이 작성한다.

- 상속/구현 라인과 생성자라인에 사이에 LF 한다.
  - 단 데이타를 담는 sealed class 안의 클래스들에는 LF 하지 않는다.
- sealed class 가 아닌 다른 class 에는 생성자 앞에 constructor 키워드를 붙인다.

``` kotlin
😰
internal class BadClass ( /** constructor 키워드가 있어야 한다. */
    private val context: Context,
    private val resources: Resource
) : FrameLayout(context) { /** 윗 라인에 공백라인을 추가한다. */

  private val variable: Int = 0

  ...
  
}

😍
internal class GoodClass constructor(
    private val context: Context,
    private val resources: Resource
    
) : FrameLayout(context) {

  private val variable: Int = 0
  
  ...
  
}

😰
internal sealed class LooknFeel {
  class TopBar(
    val userName: String,
    val age: Int,
                                                // <-- 여기에 LF 하지 않는다.
  ) : LooknFeel()
  
  class BottomBar : LooknFeel()
}

😍
internal sealed class LooknFeel {
  class TopBar(
    val userName: String,
    val age: Int,
  ) : LooknFeel()
  
  class BottomBar : LooknFeel()
}
```

### ✓ 빈 함수의 경우 Unit 을 리턴한다.

``` kotlin
😰
private fun badEmptyFunction() {
}

😍
private fun goodEmptyFunction() = Unit
```

### ✓ 빈 클래스의 경우 Brace 를 생략한다.

``` kotlin
😰
internal class BadEmptyclass {
}

internal class AlsoBadEmptyclass {}

😍
internal class GoodEmptyclass
```

### ✓ data class 를 사용하지 않는다.

- kotlin 은 class 앞에 data keyword 를 붙여 data class 로써 편의함수(equal, hash, copy)등을 자동포함하도록 하는 기능이 있다.
- 하지만 이를 사용하지 않는다.
- 그 이유에 대해서는 이곳에 서술하기엔 길어지므로 lead programmer 에게 문의
  - 간단하게 설명하자면 [기본적으로 안되게 하는 철학](https://github.com/taenguree/android-code-style-guide/blob/master/General.md#%EB%AD%90%EB%93%A0%EC%A7%80-%EC%9A%B0%EC%84%A0-%EC%95%88%EB%90%98%EA%B2%8C-%ED%95%98%EA%B3%A0-%EB%82%98%EC%A4%91%EC%97%90-%ED%95%84%EC%9A%94%ED%95%A0-%EB%95%8C-%EB%90%98%EA%B2%8C%ED%95%98%EB%9D%BC-)에 위배되기 때문이다.

### ✓ 변수명만으로 타입의 의미를 표현하기 힘든 경우 typealias 를 적극적으로 사용한다.

``` kotlin
😰
private val badVariable = hashMapOf<Int, String>()

😍
private typealias PictureIndex = Int
private typealias PictureUrl   = String

private val goodVariable = hashMapOf<PictureIndex, PictureUrl>()
```

### ✓ optional 변수에 대한 unwarpping(!!) 을 적극적으로 사용한다.

- optional 인 변수가 특정순간에는 확실히 값이 있어야 한다라고 확신한다면 !! 을 적극적으로 사용한다.
- 버그로 인해 해당 변수가 그 순간에 null 이라면 앱이 죽을 것이고 crashlytics 로 리포트가 전송돼 개발자가 빠르게 인지할 수 있다.
  - 앱이 절대로 죽어서는 안되는 비지니스라면 해당하지 않는다.
  - 앱을 죽이지 않고도 리포트를 crashlytics 수준으로 받을 수 있는 내부 인프라가 있다면 !! 를 사용하지 않아도 좋다.

### ✓ optional?.let { ... } 보다는 if 문을 사용한다.

``` kotlin
😰
someVariable?.let { /** not recommended */
  ...
}

😍
if(someVariable != null) { /** recommended */
  ...
}
```

### ✓ Rx operator 는 아래와 같은 정렬을 사용한다.

- 한 두개의 operator 를 사용해 한 줄에 짧게 끝날 경우 한 줄로 작성한다.
- operator 여러개일 경우 LF 해서 사용한다.

``` kotlin
😰
private val badRxOperatorStyle = observable
  .filter { it == 1} /** 한 줄에 충분히 쓸 수 있을 만큼 많이 짧으므로 한 줄로 작성한다. */

private val alsoBadRxOperatorStyle = observable.filter { /** operator 여러개일 경우 LF 해서 사용한다. */
    it == 1
  }.map {
    it + SOME_VALUE
  }

private val alsoBadRxOperatorStyle = observable
  .filter {
    it == 1 /** 오퍼레이터 안의 로직이 한 줄로 충분히 작성하능 할 경우 한 줄로 작성한다. */
  }
  .map { 
    it + SOME_VALUE 
  }

😍
private val goodRxOperatorStyle = observable.filter { it == 1}

private val alsoGoodRxOperatorStyle = observable
  .filter { it == 1 }
  .map { it + SOME_VALUE }
```

### ✓ 데이터를 담는 클래스에 기본값을 지양한다.

- 기본값을 무조건 쓰지 말라는 것은 아니고 최대한 지양한다.
  - 기본값을 넣게되면 모든 변수가 생성자에 넣을 수 있게 되고 이는 잘못된 데이터 초기화와 잘못된 시점에서의 초기화를 야기한다.
- 명확한 기본값이라면 넣어도 상관없다.

``` kotlin
😰
internal class NotRecommendedUserClass constructor(
    private val id: String       = "",
    private val password: String = "",
            var type: UserType   = UserType.New()
)

😍
internal class RecommendedUserClass constructor(
    private val id: String,
    private val password: String
    
) {

  private lateinit var type: UserType
  
  fun setUserType(type: UserType) {
    this.type = type
  }
  
  fun getUserType() = type

}
```

### ✓ arguments hint 를 적극적으로 사용한다.

- primitive 타입의 arguments 에는 최대한 hint 를 사용한다.
- arguments 에 넣는 변수 이름과 arguments 의 이름이 동일한 경우는 굳이 hint 를 쓸 필요는 없으나 써도 무방하다.

``` kotlin
😰
loginRepository.checkSession(true, token) /** not recommended */

😍
loginRepository.checkSession(isLoggedIn = true, token = token) /** recommended */

loginRepository.login(id, password) /** well.. it's fine */

loginRepository.login( /** recommended */
    id       = id, 
    password = password
) 
```



