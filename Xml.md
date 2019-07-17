# Xml code style guide

## [Naming rules]

### ✓ 레이아웃 파일의 속성에 따라 아래와 같은 네이밍 룰을 따른다.

| 속성 | prefix_name |
| --------------- | --------------- |
| 액티비티 | activity_{name} |
| 프래그먼트 | fragment_{name} |
| 다이얼로그 프래그먼트 | dialog_fragment_{name} |
| 커스텀 View | view_{name} |
| ViewHolder | view_holder_{name} |
| include 되는 xml | include_layout_{name} |

### ✓ xml 뷰 요소들의 id 는 아래와 같은 네이밍 룰을 따른다.

- 논의 필요

## [Basic rules]

### ✓ xml 뷰 요소들 간의 공백라인은 아래와 같은 룰을 따른다.

- 기본적으로 뷰 요소들 사이에는 공백라인을 1칸 추가한다.

- 최상위 layout 의 시작과 끝에는 공백라인이 추가된다.

``` xml
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
                                                                      <!-- 이곳에 공백추가 -->
    <RelativeLayout
        android:id="@+id/root"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@android:color/background_light"
        android:orientation="vertical" />
                                                                      <!-- 이곳에 공백추가 -->
</androidx.drawerlayout.widget.DrawerLayout>
```

- 최상이 layout 이 아닌 내부 layout 과 그 layout 의 자식 뷰 사이에는 공백라인이 없어야한다.

``` xml
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:id="@+id/drawer"
        android:layout_width="500dp"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:padding="5dp"
        android:background="#ffffff"
        android:orientation="vertical"> <!-- 이처럼 아래 EditText 와 공백이 없어야 한다. -->
        <EditText
            android:id="@+id/sinod_json_edit_text"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_marginBottom="400dp"
            android:gravity="top"
            android:hint="@string/sinod_json_edit_text_hint"
            app:layout_constraintBottom_toTopOf="@+id/apply"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <Button
            android:id="@+id/apply"
            android:layout_width="match_parent"
            android:layout_height="40dp"
            android:text="@string/apply"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintStart_toStartOf="parent" />
    </androidx.constraintlayout.widget.ConstraintLayout> <!-- 이처럼 위 버튼과 공백이 없어야 한다. -->

</androidx.drawerlayout.widget.DrawerLayout>
```

- 자식이 없는 뷰 요소는 /> 으로 바로 닫는다.

``` xml
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    😰
    <androidx.constraintlayout.widget.ConstraintLayout
        android:id="@+id/bad"
        android:layout_width="500dp"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:padding="5dp"
        android:background="#ffffff"
        android:orientation="vertical">
    </androidx.constraintlayout.widget.ConstraintLayout> <!-- 이렇게 작성하지 말아야 한다. -->
  
    😍
    <androidx.constraintlayout.widget.ConstraintLayout
        android:id="@+id/good"
        android:layout_width="500dp"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:padding="5dp"
        android:background="#ffffff"
        android:orientation="vertical"/>  <!-- 올바른 사용법 -->

</androidx.drawerlayout.widget.DrawerLayout>
```

- 구글 스타일 xml 을 임포트했다면 위 룰들따라 xml 을 작성 후 command+option+L 을 눌러 코드를 reformat 한다.
    - reformat 단축키는 안드로이드 스튜디오 설정마다 개인별로 다를 수 있다.
