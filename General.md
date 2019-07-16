# General

## [ Basic rules ]

### ✓ CamelCase base

- 기본적으로 Camel case 를 사용한다.
- 하지만 아래와 같은 예외는 있다.
  - 테스트 코드의 실제 테스트 함수명은 snake case 로 사용한다.
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

### ✓ 불필요한 코멘트는 피한다.
 
- 아래와 같은 경우에만 코멘트를 작성하며 코멘트는 ``` // ``` 가 아닌 ``` /** ... */ ``` 를 사용한다.
  - 코드가 하는 작업이 변수명이나 메소드명만으로는 그 의미를 전달하기 매우 힘들 경우.
  - 불가피하게 매직상수를 사용하게 되어 그 상수의 의미를 전달할 필요가 있을 때.
  - 코드만으로는 설명할 수 없는 History 가 있을 경우.  (ex: 이 코드는 ~이슈 때문에 이렇게 짰고 ~해서 작동한다)
  - 일반적이지않은 데이터 처리의 경우. (ex: 이 데이터는 ~하게 오기 때문에 ~해서 처리해야한다)
    - onMeaure의 parameter들은 여러 정보가 담겨오는 Int 이기 때문에 View.MesureSpec 로 unpack 해서 사용해야한다.

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
if(condition) Log.d(TAG, "bad!") else Log.d(TAG, "also bad!")

😍 
if(condition) {
  Log.d(TAG, "GOOD!") }
else {
  Log.d(TAG, "also GOOD!")
}
```

