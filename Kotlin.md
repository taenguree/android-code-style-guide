# Kotlin code style guide

## [Class component rules]

### ✓ 클래스 내부의 요소들은 아래와 같은 정렬을 따릅니다.

- package + import statements
- two empty lines
- typealias definitions(if exist)
- class/interface definition
- extra contructors(if exist)
- companion object definition
- interface(callback) definition
- nested/inner class definition(if exist)
- concrete members(if exist)
- abstract methods(if exist)
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

import i.want.to.get.audi.r8
import but.it.is.very.expensive


typealias MyCustomInt = Int

internal abstract class MyCustomLayout(
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
  
  init {
    initializeViews()
  }
  
  private lateinit var viewState: ViewState
  
  private var listener: Listener? = null
  
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

### ✓ : 은 아래의 룰에 따릅니다.

- 리턴 값을 의미할 경우 suffix space 를 넣지 않습니다.
- 상속/구현을 의미할 경우 prefix/suffix spaces 를 모두 넣습니다.

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
