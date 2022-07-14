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

``` kotlin
😍
package code.style.guide

import i.will.get.audi.r8.eventually


typealias MyCustomInt = Int

internal abstract class MyCustomLayout constructor(
    private val context: Context,
    private val attrs: AttributeSet? = null

) : FrameLayout(context, attrs) {

//  constructor(context: Context, attrs: AttributeSet? = null, extra: Int) : super(context, attrs, extra)
  
//  constructor(context: Context, attrs: AttributeSet? = null, extra: Int, extra1: Int) : super(context, attrs, extra)
  
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

}
```

- 안드로이드 View/Layout 과 관련된 클래스일 경우 복원 코드와 관련해서는 아래와 같은 예외가 있다.
  - onRestoreInstanceState, onSaveInstanceState 가 라이프사이클 관련된 함수이지만 클래스 하단에 나오게 된다.
  
``` kotlin
😍
internal class MyLayout constructor(
        context: Context,
        attrs: AttributeSet? = null

) : FrameLayout(context, attrs) {

    interface Listener {
        // TODO 외부로 응답 줄 콜백 함수 정의
    }

    @Parcelize
    class LooknFeel : Parcelable

    private var listener: Listener? = null

    init {
        LayoutInflater.from(context).inflate(R.layout.view_my, this, true)

        initializeListener()
    }
    
    fun setLooknFeel(looknFeel: LooknFeel) {
        this.looknFeel = looknFeel
        
        // TODO 
    }
    
    fun setListener(listener: Listener) {
        this.listener = listener
    }

    private fun initializeListener() {
        // TODO
    }
    
    override fun onRestoreInstanceState(state: Parcelable?) {
        if(state is SavedState) {
            super.onRestoreInstanceState(state.superState)

            looknFeel = state.looknFeel

            looknFeel?.let(this::setLooknFeel)
        } else {
            super.onRestoreInstanceState(state)
        }
    }

    override fun onSaveInstanceState(): Parcelable? {
        val parcelable = super.onSaveInstanceState()

        if(parcelable == null) {
            return parcelable
        }

        return SavedState(parcelable).apply {
            this.looknFeel = this@MyLayout.looknFeel
        }
    }
    
    private class SavedState : View.BaseSavedState {
        companion object {
            @JvmField
            val CREATOR = object : Parcelable.Creator<SavedState> {
                override fun createFromParcel(source: Parcel): SavedState {
                    return SavedState(source)
                }

                override fun newArray(size: Int): Array<SavedState?> {
                    return arrayOfNulls(size)
                }
            }
        }

        var looknFeel: LooknFeel? = null

        constructor(superState: Parcelable) : super(superState)

        private constructor(source: Parcel) : super(source) {
            this.looknFeel = source.readParcelable(LooknFeel::class.java.classLoader)
        }

        override fun writeToParcel(out: Parcel, flags: Int) {
            super.writeToParcel(out, flags)

            out.writeParcelable(looknFeel, flags)
        }
    }

}
```

## [Basic rules]

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

``` kotlin
😰
internal class BadClass constructor(
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

### ✓ 데이터를 담는 클래스는 생성자 앞에 constructor 키워드를 붙이지 않고 기능을 하는 클래스의 생성자 앞에는 constructor 키워드를 붙인다.

- 아무런 argument 가 없을 경우 constructor 키워드를 생략한다.

``` kotlin
😰
internal class User constructor(val userName: String, val age: Int)

internal class RemoteAction (private val retrofit: Retrofit) {

  //...

}

internal class RemoteAction constructor() {

  //...

}

😍
internal class User (val userName: String, val age: Int)

internal class RemoteAction constructor(private val retrofit: Retrofit) {

  //...

}

internal class RemoteAction {

  //...

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

### ✓ data class 는 아래와 같은 조건에서만 사용한다.

- 모든 변수가 Immutable 일 경우 (var, MutableList, MutableSet 등등이 포함되면 data class 를 사용하지 않는다.)

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
- 예외) 중요성이 낮은 tiny 한 ui element 의 값에는 ? 를 사용해도 무방하다.

### ✓ Rx operator 는 아래와 같은 정렬을 사용한다.

- 한 두개의 operator 를 사용해 한 줄에 짧게 끝날 경우 한 줄로 작성한다.
- operator 가 여러개일 경우 LF 해서 사용한다.

``` kotlin
😰
private val badRxOperatorStyle = observable
  .filter { it == 1} /** 한 줄에 충분히 쓸 수 있을 만큼 많이 짧으므로 한 줄로 작성한다. */

private val alsoBadRxOperatorStyle = observable.filter { /** operator 여러개일 경우 줄바꿈해서 사용한다. */
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

### ✓ 데이터를 담는 클래스에 기본값을 지향한다.

- 다만 명확한 기본값으로 넣도록 한다.
- Table like 정렬을 하지 않는다.

``` kotlin
😍
internal class NotRecommendedUserClass constructor(
    private val id: String = "",
    private val password: String = "",
            var type: UserType = UserType.New()
)
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

### ✓ 함수 코드내에서 하나의 의미있는 단위로 묶을 수 있는 코드는 함수로 다시 정의해 사용한다.

- 필수는 아니며 권고사항.

``` kotlin
😍
fun bind() {
  //...
  
  fun getProgressSpannableText(): SpannableString {
      val solvedProblemCountLength = progressText.split("/").first().length

      val spannableString = SpannableString(progressText)

      spannableString.setSpan(ForegroundColorSpan(ContextCompat.getColor(context, R.color._4FC3F7)), 0, solvedProblemCountLength, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)

      return spannableString
  }

  tv_solving_progress.text = getProgressSpannableText()
  
  //...
}
```

