# Android(with Kotlin) Chapter 5 ~ Chapter 14

## 목차 
1. [Chapter 5.](#chapter-5-기타-레이아웃)
2. [Chapter 7.](#chapter-7-메뉴와-대화-상자)
3. [Chapter 8.](#chapter-8-파일처리)
4. [Chapter 10.](#chapter-10-액티비티와-인텐트)
5. [Chapter 12.](#chapter-12-데이터-저장과-관리)
6. [Chapter 13.](#chapter-13-멀티미디어와-구글-지도)
7. [Chapter 14.](#chapter-14-서비스와-브로드캐스트-리시버)


# Chapter 5. 기타 레이아웃

Chapter 5의 36p 시작하도록한다.

## 테이블레이아웃
 ----
 위젯을 표 형태로 배치할 때 주로 사용됨
 **`<TableRow>`** 와 함께 사용된다.   
 - 행의 수 : `TableRow`의 수
 - 열의 수 : `TableRow` 안에 포함된 위젯의 수

특이점 : TableLayout은 행단위 병합이 힘들다.

## 테이블레이아웃의 속성
----
1. layout_span : **열을 합쳐서 표시하라는 의미**
   - ex. layout_span="2"는 현재 셀부터 2개의 셀을(열) 합쳐 표시하라는 것.

2. layout_column : **지정된 열에 현재 위젯을 표시**
3. stretchColumns : : 레이아웃 자체에 설정하는 속성이며, 지정된 열의 너비를 늘리라는 의미.
    - ex. stretchColumns = "*"는 각 셀을 모두 같은 크기로 확장하여 전체 화면이 꽉차는 효과를 낸다.

### 2 X 5 표에 버튼 배치하기 예제

~~~XML
<TableLayout>
    <!-- 너비, 높이 생략 -->

    <!-- 0번째 열 -->
    <TableRow>
        <!-- 버튼 1 -->
        <!-- 버튼 2 -->
        <!-- 버튼 3 -->
        <!-- 버튼 4 -->
        <!-- 버튼 5 -->
    </TableRow>
    
    <!-- 1번째 열 -->
    <TableRow>
        <!-- 버튼 7 속성으로 layout_column = "1" -->
        <!-- 버튼 8 -->
        <!-- 버튼 9 속성으로 layout_span = "2"-->
    </TableRow>
</TableLayout>
~~~
어떤 모습일지는 스스로 생각해보자

### 테이블레이아웃 소스코드 중 일부 안내
---
1. `internal`키워드 : 같은 패키지면 접근 가능. (접근 지정자)
2. `arrayOf`키워드 : 리스트를 만들어준다.(단, 제네릭 타입 생략시 동적바인딩을 하기 때문에 모든 타입 허용함.)
3. `EditText`위젯 : EditText에 적힌 글자는 Data로 인식하지 않는다.(단순 픽셀로 인식) 하지만 EditeText.text.toString()이러한 작업을 거치면 Data의 의미가 생긴다.

## 그리드레이아웃
----
테이블레이아웃처럼 **표 형태로 배치할 때 사용하지만 조금 더 직관적이다**  
**행 확장을 간단하게 할 수 있어서 유연한 화면 구성에 적합함**

## 그리드레이아웃의 속성
----
1. rowCount : 행의 수 (테이블레이아웃은 TableRow의 수)
2. columnCount : 열의 수(테이블레이아웃은 TableRow내부 위젯의 수)
3. orientation : 그리드를 수평 OR 수직방향으로 우선할 것인지 설정
4. layout_rowSpan : **행을 지정된 수 만큼 확장(병합)함**(테이블레이아웃과 큰 차이점)
5. layout_columnSpan : **열을 지정된 수 만큼 확장**(테이블레이아웃은 layout_span으로 가능)
6. layout_row : 자신이 위치할 행 번호
7. layout_column : 자신이 위치할 열 번호
8. layout_gravity : 행 또는 열이 확장되었을 때 위젯을 꽉채우는 효과를 냄.(**없으면 확장해도 크기 변화 X**)

**1,2,3,4,5번은 중요함.**

### 그리드 레이아웃 예제

~~~XML
<GridLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:columnCount="4"
    android:rowCount="2" >

    <Button
        android:layout_column="0"
        android:layout_gravity="fill_vertical"
        android:layout_row="0"
        android:layout_rowSpan="2"
        android:text="1" />

    <Button
        android:layout_column="1"
        android:layout_columnSpan="2"
        android:layout_gravity="fill_horizontal"
        android:layout_row="0"
        android:text="2" />

    <Button
        android:layout_column="3"
        android:layout_row="0"
        android:text="3" />

    <Button
        android:layout_column="1"
        android:layout_row="1"
        android:text="4" />

    <Button
        android:layout_column="2"
        android:layout_row="1"
        android:text="5" />

    <Button
        android:layout_column="3"
        android:layout_row="1"
        android:text="6" />

</GridLayout>
~~~
어떤 모습일지는 스스로 생각해보자

## 프레임레이아웃
-----
**단순히 레이아웃 안의 위젯을 왼쪽 상단부터 겹쳐서 출력** (탭위젯 등과 혼용할 때 유용) 

## 프레임레이아웃 속성
---
1. foreground : 프레임레이아웃의 전경 이미지를 지정
2. foregroundGravity : 전경 이미지 위치 지정.

### 프레임레이아웃 예시

~~~xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:foreground="@drawable/dog"
    android:foregroundGravity="center|fill_horizontal"> 
    <RatingBar
        android:id="@+id/ratingBar1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <ImageView
        android:id="@+id/imageView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/ic_launcher" />

    <CheckBox
        android:id="@+id/checkBox1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="CheckBox" />

</FrameLayout>
~~~
아마 화면의 왼쪽 상단에 RatingBar, ImageView, CheckBox가 겹쳐있을 것임.


# Chapter 7. 메뉴와 대화 상자

메뉴에는 2가지 종류가 있다.
1. 옵션 메뉴 : 흔히 오른쪽 상단의 아이콘을 눌렀을 때 동작하는 것
   - 옵션 목록 많으면 자동으로 스크롤기능 제공

2. 컨텍스트 메뉴 : 보통 위젯을 롱클릭해서 나오는 메뉴


## XML을 이용한 옵션 메뉴

옵션 메뉴 설정 순서는 다음과 같다.

1. 메뉴 폴더 생성 및 메뉴 XML 파일 생성/편집
2. Kotlin코딩(`onCreateOptionsMenu()`) : 메뉴 파일 등록
3. Kotlin코딩(`onOptionItemSelected()`) : 메뉴 선택 시 동작할 내용 코딩

### XML 형식

~~~XML
<Menu>
    <item
        android:id=".,,."
        android:title = "항목 1"/>
    <item
        android:id="..."
        android:title="항목 2"/>
</Menu>
~~~

**참고로 메뉴에서 여러항목을 묶고싶다면 \<group>...\</group>을 사용해 처리한다.**

### OnCreateOptionsMenu() 메서드
----
앱이 실행되면 메뉴의 내용을 XML파일에서 자동으로 읽어옴  
메소드에 코딩할 내용은 다음과 같이 거의 고정되어 있음

~~~Kotlin
override fun onCreateOptionsMenu(menu: Menu?) : Boolean {
    super.onCreateOptionsMenu(menu)
    var mInflater = menuInflater //메뉴 레이아웃을 메모리에 로드
    //Inflater는 전개자를 의미함. 
    mInflater.inflate(R.menum.메뉴id, meun) // 메모리의 메뉴의 인스턴스 생성
    return true
}
~~~

### onOptionsItemSelected() 메소드
----
메뉴를 선택했을 때 어떤 동작을 할 것인지 작성하는 영역임  
**메뉴는 항목이 여러 개 나오기 대문에 보통 when문을 사용** 

~~~Kotlin
override fun onOptionsItemSelected(item : MenuItem) : Boolean {
    when(item.itemId){
        R.id.항목1아이디 -> {
            //항목1 선택시 할 동작
            return true
        }
        R.id.항목2아이디 -> {
            //항목2 선택시 할 동작
            return true
        }
    }
    return false
}
~~~


## Kotlin 코드만 이용한 옵션 메뉴
----
Kotlin 코드만 이용해서 옵션 메뉴를 구현한다.  
**단, `onCreateOptionsMenu(), onOptionsItemSelected()`를 사용하지 않는 것은 아니다.**

즉, 레이아웃(XML)없이 바로 구현하는 것이다.

~~~Kotlin
override fun onCreateOptionsMenu(menu: Menu?) : Boolean {
    super.onCreateOptionsMenu(menu)

    menu!!.add(0,1,0 "배경색(빨)")
    menu!!.add(0,2,0 "배경색(파)")
    menu!!.add(0,3,0 "배경색(초)")
    // 그룹 ID, 항목 ID, 순번
    // 즉, XML의 메뉴레이아웃ID, 항목id, 순서를 의미한다.
    // 순번이 0인 경우 추가된 순서대로 나타난다.

    var sMenu : SubMenu = menu.addSubMenu("버튼 변경 >>")
    sMenu.add(0, 4, 0, "버튼 45도 회전")
    sMenu.add(0, 5, 0, "버튼 2배 확대")

    return true
}
override fun onOptionsItemSelected(item : MenuItem) : Boolen{
    when(item.itemId){
        1->{
            ....
            return true
        }
        2->{
            ....
            return true
        }
        2->{
            ....
            return true
        }
        3->{
            ....
            return true
        }
        4->{
            ....
            return true
        }
        5->{
            ....
            return true
        }
    }
    return false
}
~~~


## XML을 이용한 컨텍스트 메뉴
----
**컨텍스트 메뉴는 옵션 메뉴와 달리 여러 위젯에 메뉴를 만들어 줄 수 있어서 별도의 작업이 추가됨.**

1. 메뉴 폴더 생성 및 **위젯의 메뉴 XML 파일 생성/편집**
2. Kotlin코딩 : `onCreate()` 내부에 `registerForContextMenu()`로 등록(메뉴를 사용할 위젯 등록)
3. Kotlin코딩 : `onCreateContextMenu()` 메소드 오버라이딩(메뉴 XML 등록)
4. Kotlin코딩 : `onContextItemSelected()` 메소드 오버라이딩(이벤트 리스너)

큰 차이점은 `regusterForContextMenu()`라는 메서드가 생긴 점.  
그리고 컨텍스트 메뉴니까 메서드 이름이 ContextMenu라는 점.

### onCreateContextMenu() 메소드
----
**컨텍스트 메뉴 XML 파일은 컨텍스트 메뉴가 나오게 할 위젯마다 별도의 파일로 만들어야 함.**

위젯별로 컨텍스트 메뉴가 맵핑되어야 하니까 if문을 통해서 등록한다.

~~~Kotlin
override fun onCreateContextMenu(menu : ContextMenu?, v : View?, menuInfo : ContextMenu.ContextMenuInfo?){
    super.onCreateContextMenu(menu, v, menuInfo)

    var mInflater = this.menuInflater // 메뉴 객체 생성
    if(v === 위젯1){
        // === 의미 : 참조값 비교(주소 비교)
        mInflater.inflate(R.menu.첫번째메뉴XML파일, menu)
    }
    if(v === button2){
        mInflater.inflate(R.menu.두번째메뉴XML파일, menu)
    }
}
~~~

## 전체적인 컨텍스트 메뉴 코드
----

baselayout.xml
~~~XML
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/baseLayout"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:gravity="center_horizontal"
    android:orientation="vertical" >

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="배경색 변경" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="버튼 변경" />

</LinearLayout>
~~~

menu1.xml  
~~~xml
<menu xmlns:android="http://schemas.android.com/apk/res/android" >

    <item
        android:id="@+id/itemRed"
        android:title="배경색 (빨강)">
    </item>
    <item
        android:id="@+id/itemGreen"
        android:title="배경색(초록)">
    </item>
    <item
        android:id="@+id/itemBlue"
        android:title="배경색(파랑)">
    </item>

</menu>  
~~~
menu2.xml

~~~xml
<menu xmlns:android="http://schemas.android.com/apk/res/android" >

    <item
        android:id="@+id/subRotate"
        android:title="버튼 45도 회전"/>
    <item
        android:id="@+id/subSize"
        android:title="버튼 2배 확대"/>

</menu>
~~~

MainActivity.kt
~~~Kotlin
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import android.widget.LinearLayout

class MainActivity : AppCompatActivity() {
    lateinit  var baseLayout : LinearLayout
    lateinit  var button1 : Button
    lateinit  var button2 : Button
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        title = "배경색 바꾸기(컨텍스트 메뉴)"
        baseLayout = findViewById<LinearLayout>(R.id.baseLayout) as LinearLayout
        button1 = findViewById<Button>(R.id.button1) as Button
        registerForContextMenu(button1) // 위젯에 메뉴 등록
        button2 = findViewById<Button>(R.id.button2) as Button // as 키워드 : 타입 보장(이 코드에서는 필요없긴함)
        registerForContextMenu(button2) // 등록
    }
    
    override fun onCreateContextMenu(menu: ContextMenu?,v: View?,menuInfo: ContextMenu.ContextMenuInfo? ) {
        super.onCreateContextMenu(menu, v, menuInfo)

        var mInflater = this.menuInflater // 메뉴 레이아웃을 메모리에 로드시킨다(사용할 준비)
        if (v === button1) { // v가 버튼1이면 아래 메뉴 연결
            menu!!.setHeaderTitle("배경색 변경")
            mInflater.inflate(R.menu.menu1, menu) // 위젯이 선택되어야 메뉴 객체를 만든다.
        }
        if (v === button2) { // v가 버튼2이면 아래 메뉴 연결
            mInflater.inflate(R.menu.menu2, menu)
        }
    }

    override fun onContextItemSelected(item: MenuItem) : Boolean {
        when (item.itemId) {
            R.id.itemRed -> {
                baseLayout.setBackgroundColor(Color.RED)
                return true
            }
            R.id.itemGreen -> {
                baseLayout.setBackgroundColor(Color.GREEN)
                return true
            }
            R.id.itemBlue -> {
                baseLayout.setBackgroundColor(Color.BLUE)
                return true
            }
            R.id.subRotate -> {
                button2.rotation = 45f
                return true
            }
            R.id.subSize -> {
                button2.scaleX = 2f
                return true
            }
        }
        return false
    }   
}

~~~

## Kotlin 코드만 이용한 컨텍스트 옵션 메뉴

~~~Kotlin
class MainActivity : AppCompatActivity() {

    lateinit var baseLayout : LinearLayout
    lateinit var button1 : Button
    lateinit var button2 : Button

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        title = "배경색 바꾸기"
        baseLayout = findViewById<LinearLayout>(R.id.baseLayout)

        button1 = findViewById<Button>(R.id.button1)
        registerForContextMenu(button1) // 위젯에 컨텍스트 메뉴 등록
        button2 = findViewById<Button>(R.id.button2)
        registerForContextMenu(button2) // 위젯에 컨텍스트 메뉴 등록
    }

    override fun onCreateContextMenu(menu: ContextMenu?, v: View?, menuInfo: ContextMenu.ContextMenuInfo?) {
        super.onCreateContextMenu(menu, v, menuInfo)

        // XML이 없기 때문에 별도의 Inflater는 필요없다.
        if(v === button1){ 
            menu!!.setHeaderTitle("배경색 변경") // 메뉴 이름 설정
            menu.add(0,1,0,"빨") // 항목 추가
            menu.add(0,2,0,"초") // 항목 추가
            menu.add(0,3,0,"파") // 항목 추가
        }
        if(v === button2){
            menu!!.setHeaderTitle("버튼 회전") 
            menu.add(0,4,0,"45도")
            menu.add(0,5,0,"2배 확대")

        }
    }

    override fun onContextItemSelected(item: MenuItem): Boolean {
        super.onContextItemSelected(item)
        when(item.itemId){
            1-> {
                baseLayout.setBackgroundColor(Color.RED)
            }
            2->{
                baseLayout.setBackgroundColor(Color.GREEN)
            }
            3->{
                baseLayout.setBackgroundColor(Color.BLUE)
            }
            4->{
                button2.rotation = 45f
            }
            5->{
                button2.scaleX = 2f
            }
        }
        return false
    }
}
~~~

## 토스트(Toast)
----
화면에 잠깐 나타났다가 사라지는 메시지를 의미함.

~~~Kotlin
Toast.makeText(Context context, String message, int duration).show()
~~~
- context : 현재 액티비티(화면)을 표시하기 위해 주로 `this`키워드 사용
  - 버튼 클릭시 내부 클래스에서 토스트를 출력하기 위해 `applicationContext`사용

- duration : 화면에 나타나는 시간
    - `Toast.LENGTH_LONG` /  `Toast.LENGTH_SHORT` 중 하나 사용

- .show() : 생성된 토스트를 화면에 보여주기 위함.

> 토스트 메시지는 기본적으로 화면 중앙에 위치함
> 하지만 위치를 변경할 수 있음
> ~~~Kotlin
> Toast.setGravity(int gravity, int xOffset, int yOffset)
> ~~~

## 기본 대화상자(dialog)
----
화면에 메시지를 나타낸 후 확인이나 취소 등 사용자 선택을 받을 때 사용
1. 대화상자 생성 : `AlertDialog.Builder` 클래스로 생성
2. 용도에 따른 설정
3. 대화상자 화면 출력(.show())

예시
~~~Kotlin
class MainActivity : AppCompatActivity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        var button1 = findViewById<Button>(R.id.button1)

        button1.setOnClickListener {
            var dlg = AlertDialog.Builder(this@MainActivity) // 대화상자 객체 생성
            dlg.setTitle("제목입니다") // 대화상자 이름 설정
            dlg.setMessage("이곳이 내용입니다") // 대화상자 내용 설정
            dlg.setIcon(R.mipmap.ic_launcher) // 대화장사 아이콘 설정
            dlg.show() // 대화상자 출력
        }
    }
}
~~~

### setPositiveButton() 메소드를 활용해서 확인 버튼 생성
---
`setPositiveButton("문자열", 람다식)`형태로 작성함

~~~Kotlin
button1.setOnClickListener {
        var dlg = AlertDialog.Builder(this@MainActivity)
        dlg.setTitle("제목입니다")
        dlg.setMessage("이곳이 내용입니다")
        dlg.setIcon(R.mipmap.ic_launcher)
        dlg.setPositiveButton("확인", null) // 확인 버튼 생성됨
        // 취소 버튼을 추가하려면
        // setNegativeButton() 메소드 추가
        dlg.show()
    }
~~~
현재는 람다식 부분에 **null**을 입력했으므로 \<확인>을 클릭해도 별도의 동작이 없다.

확인 버튼에 람다식 넣기 예시
~~~Kotlin
button1.setOnClickListener {
        var dlg = AlertDialog.Builder(this@MainActivity)
        dlg.setTitle("제목입니다")
        dlg.setMessage("이곳이 내용입니다")
        dlg.setIcon(R.mipmap.ic_launcher)
        dlg.setPositiveButton("확인") 
        { 
            // 람다식 시작
            // which는 어떤 항목을 선택했는지 정보를 담고있음(현재는 고를게 없음)
            dialog, which ->
            Toast.makeText(this@MainActivity,
                "확인을 눌렀네요", Toast.LENGTH_SHORT).show()
        }
        dlg.show()
    }
~~~

대화상자에 리스트 형태의 목록 출력하기
~~~Kotlin
 button1.setOnClickListener {
        var versionArray = arrayOf("오레오", "파이", "큐(10)") // 대화상자에 표시할 리스트
        var dlg = AlertDialog.Builder(this@MainActivity)
        dlg.setTitle("좋아하는 버전은?")
        dlg.setIcon(R.mipmap.ic_launcher)
        dlg.setItems(versionArray)
        {  // 항목을 누르면 버튼 이름이 변경됨
            dialog, which ->
            button1.text = versionArray[which]
        }
        dlg.setPositiveButton("닫기", null)
        dlg.show()
    }
~~~        

~~~Kotlin
button1.setOnClickListener {
        var versionArray = arrayOf("오레오", "파이", "큐(10)")
        var dlg = AlertDialog.Builder(this@MainActivity)
        dlg.setTitle("좋아하는 버전은?")
        dlg.setIcon(R.mipmap.ic_launcher)
        
        dlg.setSingleChoiceItems(versionArray, 0) // 항목 선택시 대화상자가 사라지는 것을 방지해줌.
                                                  // setItems()와 차이점은 파라미터가 2개임(문자열 배열, 초기 선택 인덱스)
        { 
            dialog, which ->
            button1.text = versionArray[which]
        }
        dlg.setPositiveButton("닫기", null)
        dlg.show()
    }
~~~        

~~~Kotlin
button1.setOnClickListener {
        var versionArray = arrayOf("오레오", "파이", "큐(10)")
        var checkArray = booleanArrayOf(true, false, false) //
        var dlg = AlertDialog.Builder(this@MainActivity)
        dlg.setTitle("좋아하는 버전은?")
        dlg.setIcon(R.mipmap.ic_launcher)
        dlg.setMultiChoiceItems(versionArray, checkArray) // 여러 개를 동시에 선택할 경우 사용
                                                          // checkArray의 boolean값은 처음 선택된 상태를 의미
                                                          // 없으면 Error
        { 
            dialog, which, isChecked ->
            button1.text = versionArray[which]
        }
        dlg.setPositiveButton("닫기", null)
        dlg.show()
    }
~~~    

# Chapter 8. 파일처리
----
내장 메모리 : 앱을 종료했다가 다시 실행할 때 사용했던 곳부터 이어서 작업하고 싶은 경우 **내장 메모리**에 파일을 저장하고 읽어옴
> 내장 메모리 저장 위치는 : ```/data/data/패키지명/files 폴더``` 

파일 읽기 : Context 클래스의 `openFileInput()` 메소드 사용
> `FileInputStream을` 반환

파일 쓰기 : Context 클래스의 `openFileOutput()` 메소드 사용
> `FielOutputStream을` 반환

내장 메모리에서 파일을 읽거나 쓰는 일반적인 절차

1. `openFileOutput()`, `openFileInput()`으로 파일 열기 : 반환값 `FileOutputStream` or `FileIntputStream` 반환
2. `read()` 또는 `write()`로 파일 읽기/쓰기
3. `Close()`로 파일 닫기 : 리소스 해제

파일 처리의 기본 Kotlin 코드
~~~Kotlin
class MainActivity : Activity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var btnRead : Button  = findViewById<Button>(R.id.btnRead)
        var btnWrite : Button = findViewById<Button>(R.id.btnWrite)

        btnWrite.setOnClickListener {
            
            var outFs : FileOutputStream = openFileOutput("file.txt", Context.MODE_PRIVATE)// 알아서 /data/data/패키지명/files/file.txt라고 인식함
            var str = "쿡북 안드로이드" 
            outFs.write(str.toByteArray()) // str을 바이트타입 배열로 타입 캐스팅
            outFs.close()
            Toast.makeText(applicationContext, "file.txt가 생성됨", Toast.LENGTH_SHORT).show()
        }

        btnRead.setOnClickListener {
            try {
                  var inFs : FileInputStream = openFileInput("file.txt") // /data/data/패키지명/files/file.txt를 읽음
                  // var inFs = openFileInput("file.txt") 됨
                  var txt = ByteArray(30) // 읽은 텍스트를 담을 바이트배열 생성
                  inFs.read(txt) // 읽기는 별도로 캐스팅 하지않음
                  var str = txt.toString(Charsets.UTF_8) // 문자열로 변경
                  Toast.makeText(applicationContext, str, Toast.LENGTH_SHORT).show()
                  inFs.close()
            } catch (e : IOException) {
                  Toast.makeText(applicationContext, "파일 없음", Toast.LENGTH_SHORT).show()
            }
        }
    }
}
~~~

## raw 폴더 파일 처리
----
/res/raw 폴더에 필요한 파일을 저장하여 사용하는 방법으로 `openRawResource()`메소드 사용
> 내장 메모리에서 파일을 읽을 땐 `openFileInput()`메소드를 활용함.  
> 따라서, 내장 메모리 관련 클래스인 `FileInputStream` 클래스가 아닌 `InputStream` 클래스 사용

Tip. **/res/raw는 프로젝트에 포함된 폴더이므로 **읽기전용**으로 사용가능**  
     **파일 쓰기는 내장 메모리 or SD카드를 사용해야함.**

/res/raw 파일 읽기
~~~Kotlin
class MainActivity : AppCompatActivity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var btnRead : Button
        var edtRaw : EditText
        btnRead = findViewById<Button>(R.id.btnRead)
        edtRaw = findViewById<EditText>(R.id.edtRaw)

        btnRead.setOnClickListener {
            var inputS = resources.openRawResource(R.raw.raw_test) // openFileInput과 다른 raw폴더의 파일을 읽기 위한 메서드임 때문에 인자로 리소스가 들어감.
            var txt = ByteArray(inputS.available()) // 파일에 읽을 것이 있는지 확인 (Byte 수를 리턴해줌)
            // Byte 수를 리턴으니까 파일에 있는 데이터 길이만큼 배열이 생성됨
            inputS.read(txt) // 읽기
            edtRaw.setText(txt.toString(Charsets.UTF_8)) // 위젯에 쓰기
            inputS.close()
        }
    }
}
~~~

## SD카드에서 파일 읽기
-----
> SD카드를 사용할 수 있도록 퍼미션 및 application에 관련 속성을 추가해야함.    
> /res/raw는 읽기만 가능하고 SD카드 및 내장 메모리는 읽기 쓰기 모두 가능하다. 

SD카드에서 파일 읽기 Kotlin 코드
~~~Kotlin
class MainActivity : AppCompatActivity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        ActivityCompat.requestPermissions(this, arrayOf(android.Manifest.permission.WRITE_EXTERNAL_STORAGE), Context.MODE_PRIVATE) // 권한 획득

        var btnRead : Button
        var edtSD : EditText
        btnRead = findViewById<Button>(R.id.btnRead)
        edtSD = findViewById<EditText>(R.id.edtSD)

        btnRead.setOnClickListener {

            // /res/raw파일이 아니라 SD카드를 읽기 위해 FileInputStream 클래스 이용
            var inFs = FileInputStream("/storage/emulated/0/sd_test.txt") 
            var txt = ByteArray(inFs.available())
            inFs.read(txt)
            edtSD.setText(txt.toString(Charsets.UTF_8))
            inFs.close()
        }
    }
}
~~~

## SD카드에서 폴더 및 파일 생성
-----
~~~Kotlin
class MainActivity : AppCompatActivity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        ActivityCompat.requestPermissions(this, arrayOf(android.Manifest.permission.WRITE_EXTERNAL_STORAGE), Context.MODE_PRIVATE)

        var btnMkdir : Button
        var btnRmdir : Button
        btnMkdir = findViewById<Button>(R.id.btnMkdir)
        btnRmdir = findViewById<Button>(R.id.btnRmdir) 

        var strSDpath = Environment.getExternalStorageDirectory().absolutePath // 외부 저장소의 최상위 절대 경로를 가져옴
        var myDir = File("$strSDpath/mydir") // 폴더를 만들 경로 설정

        btnMkdir.setOnClickListener {
            myDir.mkdir() // 폴더 생성
        }

        btnRmdir.setOnClickListener { 
            myDir.delete() // 폴더 삭제
        }
    }
}
~~~

## 특정 폴더의 하위 폴더 및 파일 목록
----
> `File.listFiles()` 메소드 : 지정한 폴더의 하위 폴더 및 파일 목록에 접근함

~~~Kotlin
class MainActivity : Activity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var btnFilelist : Button
        var edtFilelist : EditText
        btnFilelist = findViewById<Button>(R.id.btnFilelist)
        edtFilelist = findViewById<EditText>(R.id.edtFilelist)

        btnFilelist.setOnClickListener {
            var sysDir = Environment.getRootDirectory().absolutePath // 시스템 폴더의 최상위 절대 경로를 가져옴
            var sysFiles = File(sysDir).listFiles() // 시스템 폴더에 있는 모든 파일들을 리스트로 만듬

            var strFname: String
            for (i in sysFiles.indices) {
                if (sysFiles[i].isDirectory == true) // 파일 타입에따라 분기
                    strFname = "<폴더> " + sysFiles[i].toString()
                else
                    strFname = "<파일> " + sysFiles[i].toString()

                edtFilelist.setText(edtFilelist.text.toString() + "\n" + strFname)
            }
        }
    }
}
~~~

## 커스텀 위젯, 커스텀 뷰 만들기
----
~~~Kotlin
class myPictureView(context: Context, attrs: AttributeSet?) : View(context, attrs) {
    var imagePath : String? = null

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)
        try {
            if (imagePath != null) {
                var bitmap = BitmapFactory.decodeFile(imagePath) // 파일 가져옴
                canvas.scale(2f, 2f, 0f, 0f) // 비트맵 확대
                canvas.drawBitmap(bitmap!!, 0f, 0f, null) // 그리기
                bitmap!!.recycle() // 메모리 해제
            }
        } catch ( e : Exception) {
        }
    }
}
~~~

커스텀 뷰 적용하기
~~~XML
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal" >

        <Button
            android:id="@+id/btnPrev"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text=" 이전 그림 " />

        <Button
            android:id="@+id/btnNext"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text=" 다음 그림 " />
    </LinearLayout>
    <!-- 커스텀 뷰 적용 모습 (패키지.클래스) -->
    <com.cookandroid.project8_2.myPictureView
        android:id="@+id/myPictureView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

</LinearLayout>
~~~

# Chapter 10. 액티비티와 인텐트

지금까지는 MainActivity의 View에서만 변경되는 방식라면, 이제는 액티비티 사이에 통신하는 방법을 학습힌다.

## 안드로이드의 4대 컴포넌트
---
1. 액티비티
    - 화면을 구성하는 **가장 기본적인 컴포넌트**
2. 서비스
   - 눈에 보이는 화면과 상관없이 **백그라운드에서 동작하는 컴포넌트**
   - 로컬에서 동작하는 서비스는 3가지 단계를 거친다.
       - 생성 -> 시작 -> 종료
3. 브로드캐스트 리시버
   - 문자 메시지도착, 배터리 방전, SD카드 탈부착 등 방송 메시지가 발생하면 반응함.  
    ex. 배터리가 얼마 없을 때 경고 및 소리를 발생시키는 것.
4. 콘텐트 프로바이더
    - **응용 프로그램 사이에 데이터를 공유하기 위한 컴포넌트** (인텐트랑은 다른 개념임)
    - 자신의 데이터를 **외부에 공개하려면** 콘텐트 프로바이더를 만들어야함.

## 액티비티의 개요
----
현재 액티비티를 끝내는 방법 : `finish()` 메소드 활용(인텐트가 변경되기전 Activity로 돌아감.)  

인텐트? : 안드로이드 4대 컴포넌트가 **서로 데이터를 주고받기 위한 메시지 객체**

MainActivity에서 SecondActivity를 호출하는 방법
~~~Kotlin
var btnNewActivity = finViewById<Button>(R.id.btnNewActivity)
btnNewActivity.setOnClickListener{
    var intent = Intent(applicationContext, SecondActivity::calss.java) // 명시적 인텐트라고 부름
    // applicationContext == this
    // SecondActivity::calss.java 이동할 목적지 액티비티
    startActivity(intent)
    // 액티비티 시작
}
~~~

> **반드시 `AndroidManifest.xml`에 새로운 액티비티를 등록시켜야함**

### 명시적 인텐트
----
명시적 인텐트는 **다른 액티비티의 이름을 명확히 지정할 때 사용**
~~~Kotlin
var intent = Intent(applicationContext, SecondActivity::calss.java) 
startActivity(intent)
~~~

`Intent()`생성자의 두 번째 파라미터에서는 액티비티 클래스를 넘길 수 있으며 **그 전에 생성한(명시된)** SecondActivity로 정확히 지정함.  
즉, 명확하게 SecondAcitvity라고 지정했기 때문에 명시적 인텐트라고 부름.  

**일반적으로 명시적 인텐트는 사용자가 새로운 액티비티를 직접 생성하고 호출할 때 사용**

### 명시적 인텐트 데이터 넣기

보내는 쪽 : `putExtra()`  
받는 쪽 : 데이터 타입에 따라 다름(`getStringExtra()`, `getIntExtra()`, `getBooleanExtra()`등)

> 다수의 같은 타입 위젯에 이벤트 리스너 작성하는 방법
> ~~~Kotlin
>  for (i in imageId.indices) {
>            image[i] = findViewById<ImageView>(imageId[i])
>            image[i]!!.setOnClickListener {
>                // 투표수 증가.
>                voteCount[i]++
>                Toast.makeText(applicationContext,imgName[i] + ": 총 " + voteCount[i] + " 표", Toast.LENGTH_SHORT).show()
>            }
>        }
> ~~~

인텐트를 활용해서 다른 액티비티로 데이터 전송
~~~Kotlin
btnFinish.setOnClickListener {
    var intent = Intent(applicationContext, ResultActivity::class.java) // 명시적 인텐트
    intent.putExtra("VoteCount", voteCount) // 데이터이름, 변수
    intent.putExtra("ImageName", imgName) 
    startActivity(intent)
}
~~~

다른 액티비티에서 데이터 읽기
~~~Kotlin
class ResultActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)
        setContentView(R.layout.result)
        title = "투표 결과"

        // 앞 화면에서 보낸 투표 결과 값을 받는다.
        var intent = intent //인텐트 객체 생성
        var voteResult = intent.getIntArrayExtra("VoteCount") // 전송한 데이터 이름을 통해서 데이터 읽음
        var imageName = intent.getStringArrayExtra("ImageName")
        
    }
}
~~~


### 양방향 액티비티
----
지금 까지는 단방향 데이터 전송을 해봤음.(main -> second)

양방향 액티비티는 아래와 같다.
1. 메인 액티비티에서 `putExtra()`로 인텐트에 데이터를 넣는 것은 동일
2. 세컨드 액티비티에서 **데이터를 돌려 받기 위해 `startActivityForResult()` 메소드 사용**
3. 세컨드 액티비티에서 `finish()`로 끝내기 전에 메인 액티비티에 돌려줄 인텐트를 생성하여 `putExra()` 데이터를 넣어서 `setResult()`로 돌려준다.
4. 메인 액티비티에서 `onActivityResult()` 메소드를 오버라이딩하고 `getExra()`로 돌려받은 데이터 사용

> 뭔말인지 모르겠다.

메인 액티비티.kt
~~~Kotlin
class MainActivity : AppCompatActivity() {
    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        title = "메인 액티비티"

        var btnNewActivity = findViewById<Button>(R.id.btnNewActivity) 
        btnNewActivity.setOnClickListener {
            var edtNum1 = findViewById<EditText>(R.id.edtNum1) 
            var edtNum2 = findViewById<EditText>(R.id.edtNum2) 

            var intent = Intent(applicationContext, SecondActivity::class.java) // 명시적 인텐트
            intent.putExtra("Num1", Integer.parseInt(edtNum1.text.toString())) // Num1 이름으로 데이터 전송
            intent.putExtra("Num2", Integer.parseInt(edtNum2.text.toString())) // Num2 이름으로 데이터 전송
            startActivityForResult(intent, 0) // 단방향은 startActivity였다
            // 양방향 통신을 위해서 새 액티비티를 열어주는 것과 동시에 결과값 전달을 진행함.
            // 0 이라는 숫자의 의미는 어떤 Activity인지 식별하는 TAG같은 것이라 생각하면 됨.
        }
    }

    // 데이터 돌려받기
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {

        super.onActivityResult(requestCode, resultCode, data)
        
        if(requestCode == 0){ // startActivityForResult(intent, 0)에서 보냈던 activity식별 값 확인
            // resultCode : setResult()에서 보낸 값(세컨드 액티비티에서 보낸 값)
            if (resultCode == Activity.RESULT_OK) {
                var hap = data!!.getIntExtra("Hap", 0)
                Toast.makeText(applicationContext, "합계 :$hap", Toast.LENGTH_SHORT).show()
            }
        }
    }
}
~~~


세컨드 액티비티.kt
~~~Kotlin
class SecondActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)
        setContentView(R.layout.second)
        title = "Second 액티비티"

        var inIntent = intent
        var hapValue = inIntent.getIntExtra("Num1", 0) + inIntent.getIntExtra("Num2", 0) // 데이터 받아서 바로 연산

        var btnReturn = findViewById<Button>(R.id.btnReturn) 
        btnReturn.setOnClickListener {
            var outIntent = Intent(applicationContext, MainActivity::class.java) //명시적 인텐트 (세컨드 -> 메인)
            outIntent.putExtra("Hap", hapValue) // Hap이름으로 데이터 전송
            setResult(Activity.RESULT_OK, outIntent) // 성공 코드와 함께 인텐트 전송
            // 실패의 경우 Activity.RESULT_CANCEL로 설정
            finish()
        }
    }
}
~~~

### 암시적 인텐트
----
**약속된 액션을 지정해서 프로그램 실행**  
ex. 전화번호를 인텐트로 넘긴 후 전화 걸기 프로그램 실행

~~~Kotlin
var intent = Intent(Intent.ACTION_DIAL, Uri.parse("tel : 119"))
// 1번 인자는 지정한 액션, 2번 인자는 보낼 데이터
startActivity(intent)
~~~

명시적 인텐트와 암시적 인텐트 차이 비교하기
~~~Kotlin
var ExplicitIntent = Intent(applicationContext, SecondActivity::class.java) // 명시적 인텐트
var ImplicitIntent = Intent(Intent.ACTION_DIAL, Uri.parse("tell : 119")) // 암시적 인텐트
~~~

전화걸기 및 웹사이트 이동 예시
~~~Kotlin

// 전화 걸기
var callUri = Uri.parse("tel : 010-1234-5678")
var intent = Intent(Intent.ACTION_DIAL, callUri)

// 웹사이트 이동
var webUri = Uri.parse("http://www.naver.com")
var intent = Intent(Intent.ACTION_VIEW, webUri)

~~~

### Uniform Resource Identifier(Uri)
----

착각하기 쉬운 Uri/Url에 대해서 잠깐 이야기한다.

Uri - 웹 기술에서 사용하는 논리적 또는 물리적 **리소스를 식별하는 고유한 문자열**을 의미.  
Url - 흔히 웹 주소라고 말하며 리소스가 어디있는지 알려주는 **위치**를 의미함.



## 액티비티 생명주기
---

[액티비티 실행]
1. `onCreate()` : **앱 실행 최초 1회 실행됨**
2. `onStart()` : 다른 액티비티가 사용이 종료된 경우 `onRestart()`과정을 거친 후 실행 됨.
3. `onResume()` 

[액티비티 종료]
1. `onPause()`
2. `onStop()`
3. `onDestroy() `: 액티비티 종료시에만 호출됨 (다른 액티비트를 요청하면 `onPause()`, `onStop()` 수행하고 다른 액티비로 전환됨)

세컨드 액티비티 종료 후 메인 액티비티로 넘어가는 과정  
=> `onRestart()`, `onStart()`, `onResume()`가 순차적으로 수행된 후 메인 액티비티로 넘어온다.

<details>
<summary>안드로이드 액티비티 생명주기</summary>
<div markdown = "1">

![안드로이드 액티비티 생명주기](https://kairo96.gitbooks.io/android/content/pic2/2-4-1-1.jpg)

</div>
</details>

> 컨텐트 프로바이저, 브로드캐스팅은 생명주기가 없다.



### 액티비티 생명주기 확인방법(Logcat)
----

~~~Kotlin

Log.d(태그, 내용) // debug ==> 상태 확인용
Log.e(태그, 내용) // error ==> 에러 보고용
Log.v(태그, 내용) // varbose ==> 상세한 설명
Log.w(태그, 내용) // warn ==> 경고
Log.i(태그, 내용) // info ==> 정보
Log.wtf(태그, 내용) // what the fuck(x) what a terrible failure(o)
~~~

### 액티비티 생명주기 정리

1. 앱 최초 1회 실행 : `onCreate()` -> `onStart()` -> `onResume()` -> 메인 액티비티 실행됨
2. 메인 액티비티 종료 : `onPause()` -> `onStop()` -> `onDestroy()` -> 앱 종료 
3. 메인 액티비티 -> 세컨트 액티비티 : `onPause()` -> `onStop()` ->  세컨트 액티비티 실행됨
4. 세컨트 액티비티 종료 : `onRestart()` -> `onStart()` -> `onResume()` : 메인 액티비 실행됨


> `onDestroy()`는 뒤로가기로 액티비티를 종료해도 발동되며 이후 똑같은 액티비티를 실행시 `onCreate()`가 호출됨


# Chapter 12. 데이터 저장과 관리
-----

데이터베이스 구축 4단계

1. 데이터베이스 생성
2. 테이블 생성
3. 데이터 입력
4. 데이터 조회 및 활용
   
## SQLite에서 데이터베이스 구축
----
명령 프롬프트에서 SQLite접속 준비하기

~~~Bash
abd root
abd shell
cd /data/data/com.cookandroid.project12_1
ls -1
mkdir databases
cd databases
pwd
~~~

1단계 데이터베이스 생성
~~~sql
sqlite3 naverDB
~~~

2단계 테이블 생성
~~~sql
CREATE TABLE 테이블이름(열이름1 데이터형식, 열이름2, 데이터형식, ....);
~~~

3단계 데이터 입력
~~~sql
INSERT INTO 테이블이름 VALUES(값1, 값2, ... );
~~~

4단계 데이터 조회 및 활용
~~~sql
SELECT 열이름1, 열이름2, ... FROM 테이블이름 WHERE 조건;
SELECT * FROM 테이블이름
SELECT * FROM 테이블이름 WHERE 조건;
~~~

## SQLite 프로그래밍
----

<details>
<summary>SQLite 관련 클래스의 동작</summary>
<div markdown = "1">

![SQLite 관련 클래스의 동작](https://mblogthumb-phinf.pstatic.net/20150711_259/zxy826_1436585795198rkntH_JPEG/1.PNG?type=w800)

</div>
</details>

안드로이드 앱 개발을 위한 SQLite 동작 방식  
- `SQLiteOpenHelper` 클래스, `SQLiteDatabase` 클래스, `Curor` 인터페이스 활용

1. `SQLiteOpenHelper` :  DB생성, Table 생성(DB생성, 테이블 생성, 테이블 삭제 후 다시 생성 등)
2. `SQLiteDatabase` : 쿼리문 실행(Insert, Update, Delete, DB닫기, Select 실행 후 커서 변경)
3. `Curor` : Row(행)단위 인덱싱(커서의 첫 행으로 이동, 커서의 마지막 행 이동, 다음 행 이동)

이 3가지가 모두 있어야 동작한다.

### 단계별 Kotlin에 적용하기

1. 데이터베이스 열기
~~~Kotlin
SQLiteDatabase sqliteDB = null;
sqliteDB = SQLiteDatabase.openOrCreateDatabase("sample.db", null);
~~~

2. 테이블 만들기
~~~Kotlin
String sql = "CREATE TABLE ...." ;
sqliteDB.execSQL(sql);
~~~

3. 데이터 추가
~~~Kotlin
String sql = "INSERT INTO ... ";
sqliteDB.execSQL(sql);
~~~

4. 데이터 수정
~~~Kotlin
String sql = "UPDATE ... ";
sqliteDB.execSQL(sql);
~~~

5. 데이터 삭제
~~~Kotlin
String sql = "DELETE FROM ... ";
sqliteDB.execSQL(sql);
~~~

6. 데이터 조회
~~~Kotlin
Cursor cursor = sqliteDB.rawQuery("SELECT ...", null);
while(cursor.moveToNext()){
    ...

}
~~~

7. 테이블 삭제
~~~Kotlin
String sql = "DROP TABLE ...";
sqliteDB.execSQL(sql);
~~~

`SQLiteOpenHelper` 구조 이해

> CustomerDatabase
> >DatabaseHelper extends SQLiteOpenHelper
> > > onCreate()  
> > > onOpen()  
> > > onUpgrade()  


### Kotlin 코드 작성
----

`SQLiteOpenHelper` 클래스에서 상속받은 클래스를 정의한 후 생성자 수정하기

~~~Kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }

    // SQLiteOpenHelper을 상속받아서 재정의                     //context, DB이름, 커서, 버전
    inner class myDBHelper(context: Context) : SQLiteOpenHelper(context, "groupDB", null, 1) {

        // 테이블을 생성하는 기능 코딩
        override fun onCreate(p0: SQLiteDatabase?) {
            p0!!.execSQL("CREATE TABLE  groupTBL ( gName CHAR(20) PRIMARY KEY, gNumber INTEGER);")
        }

        // 테이블을 삭제한 후 다시 생성
        override fun onUpgrade(p0: SQLiteDatabase?, p1: Int, p2: Int) {
            //p1과 p2는 버전을 의미하며 두 버전이 달라야 동작함.
            p0!!.execSQL("DROP TABLE IF EXISTS groupTBL") // 쿼리문 실행
            onCreate(p0) //다시 생성
        }
    }
}
~~~

본격적인 SQLite Kotlin으로 작업하기
~~~Kotlin
myHelper = myDBHelper(this)

btnInit.setOnClickListener {
    sqlDB  = myHelper.writableDatabase // 쓰기모드로 DB오픈
    myHelper.onUpgrade(sqlDB, 1, 2) // 1, 2 숫자가 달라야 Upgrade진행됨
    sqlDB.close() // DB 닫기
}
~~~

~~~Kotlin
btnInsert.setOnClickListener {
    sqlDB = myHelper.writableDatabase // 쓰기모드로 오픈

    // 삽입 쿼리문 작성(보통은 try-catch랑 같이 쓰임)
    sqlDB.execSQL("INSERT INTO groupTBL VALUES ( '" 
            + edtName.text.toString() + "' , "
            + edtNumber.text.toString() + ");")
    sqlDB.close() // 닫기
    Toast.makeText(applicationContext, "입력됨", Toast.LENGTH_SHORT).show() // 토스트 메시지
}
~~~

SQLite 데이터 읽기
~~~Kotlin
btnSelect.setOnClickListener {

    sqlDB = myHelper.readableDatabase // 읽기모드
    var cursor: Cursor // 커서 선언
    cursor = sqlDB.rawQuery("SELECT * FROM groupTBL;", null) // 행 전체 읽어옴
 
    var strNames = "그룹이름" + "\r\n" + "--------" + "\r\n"
    var strNumbers = "인원" + "\r\n" + "--------" + "\r\n"

    while (cursor.moveToNext()) { // 다음 커서로 계속 이동한다(EOF까지)
        strNames += cursor.getString(0) + "\r\n" // 커서가 가르키는 행의 0번째 열 파싱
        strNumbers += cursor.getString(1) + "\r\n" // 커서가 가르키는 행의 1번째 열 파싱
    }

    edtNameResult.setText(strNames) // editText에 입력
    edtNumberResult.setText(strNumbers)

    cursor.close() // 커서 종료
    sqlDB.close() // DB종료
}
~~~

# Chapter 13. 멀티미디어와 구글 지도
구글 지도는 생략.

## 오디오
---
MediaPlayer 클래스 : 음악 및 동영상을 재생해주는 기능
MediaPlayer의 메소드에는 `play(), pause(), stop()`이 있음

간단한 음악재생 앱 만들기
~~~Kotlin
class MainActivity : Activity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var mPlayer: MediaPlayer // MediaPlayer객체 생성
        mPlayer = MediaPlayer.create(this, R.raw.song1) // 재생할 음악 선택
 
        var switch1 = findViewById<Switch>(R.id.switch1)
        switch1.setOnClickListener {
            if (switch1.isChecked == true)
                mPlayer.start() // 재생
            else
                mPlayer.stop() // 중지
        }
    }
}
~~~

응용 : SD카드의 mp3파일을 목록으로 출력한 후 선택한 곡 재생하기
~~~Kotlin
class MainActivity : Activity() {

    var listViewMP3: ListView? = null
    lateinit var btnPlay: Button
    lateinit var btnStop: Button
    lateinit var tvMP3: TextView
    lateinit var pbMP3: ProgressBar

    lateinit var mp3List: ArrayList<String>
    lateinit var selectedMP3: String

    var mp3Path = Environment.getExternalStorageDirectory().path + "/" // mp3파일 경로 읽음
    lateinit var mPlayer: MediaPlayer // 재생 플래이어 객체 생성
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        title = "간단 MP3 플레이어"
        ActivityCompat.requestPermissions(this, arrayOf(android.Manifest.permission.WRITE_EXTERNAL_STORAGE), Context.MODE_PRIVATE) // 권한 얻기

        // SDCard의 파일을 읽어서 리스트뷰에 출력
        mp3List = ArrayList() // 가변적 문자열

        val listFiles = File("/sdcard/").listFiles() // mp3Path 경로에 있는 모든 파일을 list로 만듬

        var fileName: String
        var extName: String

        for (file in listFiles!!) { // list 순회
            fileName = file.name
            extName = fileName.substring(fileName.length - 3) // 음악 이름 뒤에 확장자명 추출
            if (extName == "mp3")
            // 확장명이 mp3일 때만 추가함.
                mp3List.add(fileName)
        }

        var listViewMP3 = findViewById<ListView>(R.id.listViewMP3)
        var adapter = ArrayAdapter(this, android.R.layout.simple_list_item_single_choice, mp3List) // 화면에 표시되는 재생목록 중에 하나만 선택가능하도록 함.
        listViewMP3.choiceMode = ListView.CHOICE_MODE_SINGLE // 싱글 초이스 모드
        listViewMP3.adapter = adapter
        listViewMP3.setItemChecked(0, true) // 초기값으로 첫 아이템을 체크 상태로

        listViewMP3.setOnItemClickListener{ arg0, arg1, arg2, arg3 ->
            /*
            * arg0 : 상위 어댑터 뷰
            * arg1 : 클릭한 raw 뷰
            * arg2 : 클릭한 위치
            * arg3 : 클릭한 위치 (Long타입)*/
            selectedMP3 = mp3List[arg2]
        }
        selectedMP3 = mp3List[0]

        btnPlay = findViewById<Button>(R.id.btnPlay)
        btnStop = findViewById<Button>(R.id.btnStop)
        tvMP3 = findViewById<TextView>(R.id.tvMP3)
        pbMP3 = findViewById<ProgressBar>(R.id.pbMP3)

        btnPlay.setOnClickListener {
            mPlayer = MediaPlayer() // 플레이어 객체 생성
            mPlayer.setDataSource(mp3Path + selectedMP3) // 경로 + file 이름
            mPlayer.prepare() // 초기화 상태로 준비해야함.
            mPlayer.start()
            btnPlay.isClickable = false
            btnStop.isClickable = true
            tvMP3.text = "실행중인 음악 :  $selectedMP3"
            pbMP3.visibility = View.VISIBLE
        }

        btnStop.setOnClickListener {
            mPlayer.stop()
            mPlayer.reset()
            btnPlay.isClickable = true
            btnStop.isClickable = false
            tvMP3.text = "실행중인 음악 :  "
            pbMP3.visibility = View.INVISIBLE
        }
        btnStop.isClickable = false

    }
}
~~~
## 프로그레스바, 시크바
----
프로그레스바 : 작업의 진행 상태를 확인할 경우 사용  
시크바 : 음악이나 동영상 재생의 위치를 지정할 때 많이 활용
 
~~~XML
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:layout_margin="20dp"
    android:orientation="vertical" >

    <!-- 프로그레스바 -->
    <!-- max : 최대 값 -->
    <!-- progress : 현재 값 -->
    <ProgressBar
        android:id="@+id/progressBar1"
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:max="100"
        android:progress="20" />

    <Button
        android:id="@+id/btnInc"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="10씩 증가" />

    <Button
        android:id="@+id/btnDec"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="10씩 감소" />

    <TextView
        android:id="@+id/tvSeek"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:textSize="20dp" />
    <!-- 시크바 -->
    <SeekBar
        android:id="@+id/seekBar1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

</LinearLayout>
~~~

프로그레스바 Kotlin 코딩
~~~Kotlin
class MainActivity : AppCompatActivity() {

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var pb1: ProgressBar
        var btnInc: Button
        var btnDec: Button

        pb1 = findViewById<ProgressBar>(R.id.progressBar1)
        btnInc = findViewById<Button>(R.id.btnInc)
        btnDec = findViewById<Button>(R.id.btnDec)

        // 프로그레스바 값 증가시킴
        btnInc.setOnClickListener {
            pb1.incrementProgressBy(10)
        }

        // 프로그레스바 값 감소시킴(감소 전용 메소드는 별도로 없고 +-를 통해서 조절)
        btnDec.setOnClickListener {
            pb1.incrementProgressBy(-10)
        }

        var tvSeek = findViewById<TextView>(R.id.tvSeek)
        var seekBar1 = findViewById<SeekBar>(R.id.seekBar1)

        seekBar1.setOnSeekBarChangeListener(object : SeekBar.OnSeekBarChangeListener {
            override fun onStopTrackingTouch(seekBar: SeekBar) {} // 드래그 중 발생하는 이벤트
            override fun onStartTrackingTouch(seekBar: SeekBar) {} // 최초 탭하여 드래그 시작시 발생할 이벤트

            // 드래그 멈추면 발생할 이벤트
            //시크바 View, 변경된 값, 사용자에 의한 변경인지(True) | 코드에 의한 변경인지(False)
            override fun onProgressChanged(seekBar: SeekBar, progress: Int, fromUser: Boolean) {
                tvSeek.text = "진행률 : $progress %"
            }
        })

    }
}
~~~
## Thread(스레드)
---
동시에 여러 작업을 수행하기 위해 사용되는 개념  
**멀티스레드(Multi-Thread), 혹은 경량 프로세스라고 함.**  

![스레드와 함수 차이](data:image/jpeg;base64,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)   
함수는 하나의 작업이 종료되어야 다음 작업이 진행됨, 스레드는 하나의 작업이 끝나기 전에 다른 작업을 동시 진행이 가능함.

### 스레드 기본 예제
~~~XML
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:layout_margin="10dp"
    android:orientation="vertical" >

    <SeekBar
        android:id="@+id/pb1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:max="100"
        android:progress="10" />

    <SeekBar
        android:id="@+id/pb2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:max="100"
        android:progress="30" />


    <Button
        android:id="@+id/button1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="스레드 시작" />

</LinearLayout>
~~~

~~~Kotlin 
class MainActivity : AppCompatActivity() {
    lateinit var pb1: ProgressBar
    lateinit var pb2: ProgressBar
    lateinit var btn: Button

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        pb1 = findViewById<ProgressBar>(R.id.pb1)
        pb2 = findViewById<ProgressBar>(R.id.pb2)
        btn = findViewById<Button>(R.id.button1)

        // 동작하지 않는다.(내부적으로 값은 증가하지면 UI가 실시간으로 반영x) => 스레드 필요
        btn.setOnClickListener {
            for (i in 0..99) {
                pb1.progress = pb1.progress + 2
                pb2.progress = pb1.progress + 1
                SystemClock.sleep(100) // 0.1초 의미
            }
        }
    }
}
~~~

-----
스레드 사용하기
~~~Kotlin
object : Thread() {
    override fun run(){
        // 실행문 작성
    }
}.start() // 기본 스레드는 start() 필수
~~~

스레드를 적용해서 다시 코딩하기
~~~Kotlin
class MainActivity : Activity() {
    lateinit var pb1: ProgressBar
    lateinit var pb2: ProgressBar
    lateinit var btn: Button

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        pb1 = findViewById<ProgressBar>(R.id.pb1)
        pb2 = findViewById<ProgressBar>(R.id.pb2)
        btn = findViewById<Button>(R.id.button1)

        btn.setOnClickListener {
            object : Thread(){ // 기본 스레드 적용
                override fun run(){ // 스레드 실행시 동작할 이벤트 작성
                    for (i in 0..99) {
                        pb2.progress = pb2.progress + 2
                        SystemClock.sleep(100)
                    }
                }
            }.start() // 스레드 시작

            object : Thread(){
                override fun run(){
                    for (i in 0..99) {
                        pb1.progress = pb1.progress + 1
                        SystemClock.sleep(100)
                    }
                }
            }.start()
        }
    }
}
~~~

### UI스레드 예제
---
기본 스레드는 스레드에서 필요한 내용 계산은 가능하지만 위젯을 변경할 수는 없음(ex. TextView에 값을 변경한다)
때문에 안드로이드는 UI스레드를 제공한다.

뭔가 이상한 코드.kt
~~~Kotlin
class MainActivity : Activity() {
    lateinit var btn: Button
    lateinit var pb1: ProgressBar
    lateinit var pb2: ProgressBar
    lateinit var tv1: TextView
    lateinit var tv2: TextView

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        pb1 = findViewById<ProgressBar>(R.id.pb1)
        pb2 = findViewById<ProgressBar>(R.id.pb2)
        btn = findViewById<Button>(R.id.button1)

        tv1 = findViewById<TextView>(R.id.tv1)
        tv2 = findViewById<TextView>(R.id.tv2)

        btn.setOnClickListener {
            object : Thread() {
                override fun run() {
                    for(i in pb1.progress .. 99 ) {
                        pb1.progress = pb1.progress + 2
                        tv1.text = "1번 진행률 : " + pb1.progress + "%" // 이부분에서 앱이 터질 것이다.
                        SystemClock.sleep(100)
                    }
                }
            }.start()

            object : Thread() {
                override fun run() {
                    for (i in pb2.progress..99) {
                        pb2.progress = pb2.progress + 1
                        tv2.text = "2번 진행률 : " + pb2.progress + "%"
                        SystemClock.sleep(100)
                    }
                }
            }.start()
        }

    }
}
~~~
**Only the original thread that created a view hierarchy can touch its views. 라는 에러를 던질 것임**  
이유는 다름아니라 기본 스레드는 위젯의 내용을 변경시킬 수 없기 때문이다.

이를 해결하고자 기본스레드 내부에 UI스레드를 추가한다.
~~~Kotlin
runOnUiThread{
    // 위젯을 변경하는 코드를 이곳에 넣는다.
} // 기본 스레드와 다르게 .start()없이 동작한다. (기본 스레드 내부에 있어서 스레드가 동작한다고 가정하기 떄문)
~~~

동작하는 코드 
~~~Kotlin
class MainActivity : AppCompatActivity() {

    lateinit var btn: Button
    lateinit var pb1: ProgressBar
    lateinit var pb2: ProgressBar
    lateinit var tv1: TextView
    lateinit var tv2: TextView

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        pb1 = findViewById<ProgressBar>(R.id.pb1)
        pb2 = findViewById<ProgressBar>(R.id.pb2)
        btn = findViewById<Button>(R.id.button1)

        tv1 = findViewById<TextView>(R.id.tv1)
        tv2 = findViewById<TextView>(R.id.tv2)

        btn.setOnClickListener { 
            object : Thread() { // 기본 스레드
                override fun run() { // 실행문 
                    for(i in pb1.progress .. 99 ) {
                        pb1.progress = pb1.progress + 2
                        runOnUiThread { // UI스레드 동작
                            pb1.progress = pb1.progress + 2
                            tv1.text = ("1번 진행률 : " + pb1.progress + "%")
                        }
                        SystemClock.sleep(100)
                    }
                }
            }.start() // 스레드 시작

            object : Thread() {
                override fun run() {
                    for (i in pb2.progress..99) {
                        runOnUiThread {
                            pb2.progress = pb2.progress + 1
                            tv2.text = ("2번 진행률 : " + pb2.progress + "%")
                        }
                        SystemClock.sleep(100)
                    }
                }
            }.start()
        }

    }
}
~~~

# Chapter 14. 서비스와 브로드캐스트 리시버

액티비티 생명주기와 달리 서비스는 다른 생명주기를 가지며, 브로드캐스트 리시버와 콘텐트 프로바이더는 생명주기가 없다.

## 서비스 
----
서비스 : **화면 없이 동작하는 프로그램을 뜻함.**  
   - ex. 데몬, 백그라운드 프로세스

> 서비스 생명주기 
> > `onStartService()`(서비스 요청) -> 시작 -> `onCreate()` -> `onStartCommand()` -> 서비스 동작 -> `onStopService()`(서비스 중지 요청) -> `onDestroy()` -> 종료
> > > 원격 인터페이스 호출의 경우 `onStartCommand()`가 아닌 `onBind()`가 동작함. **단, onBind()는 무조건 작성되어야함**

1. `onStartService()` : 메인 액티비티에서 호출해야함.
2. `onStartCommand()` : **Service 클래스를 상속받는 클래스에서 호출됨.**
3. `onStopService()`:
4. `onBind()` :**Service 클래스를 상속받는 클래스에 항상 작성되어야함** 하지만 필요없다면 ```return null```처리를 함.

## 생명주기 관찰

메인 액티비티에서 음악 재생 버튼을 누른 경우  
onCreate -> onStart -> onResume -> StartService 순서로 호출하게 됨

이때 Service 클래스를 상속받는 클래스의 경우  
onCreate -> onStartCommand 순서로 호출하게 된다. (액티비티의 생명주기와 달리 이놈은 서비스의 생명주기이기 때문에 살짝 다름)
> 액티비티 생명주기는 최초 실행시 onCreate -> onStart -> onResume 순서를 반드시 따름.  
> 서비스의 경우 onCreate -> onStartCommand이다.  

### Kotlin 예제 보기


MainActivity.kt
~~~Kotlin
class MainActivity : Activity() {

    lateinit var btnStart : Button
    lateinit var btnStop : Button

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.i(TAG, "onCreate()")
        setContentView(R.layout.activity_main)

        btnStart = findViewById(R.id.btnStart)
        btnStop = findViewById(R.id.btnStop)
        var intent = Intent(this, SecondActivity::class .java) // 명시적 인텐트

        btnStart.setOnClickListener {
            startService(intent) // 서비스 시작
            Log.i(TAG, "StartService()")
        }

        btnStop.setOnClickListener {
            stopService(intent) // 서비스 종료
            Log.i(TAG, "StopService()")
        }
    }

    override fun onRestart() {
        super.onRestart()
        Log.i(TAG, "onRestart()")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.i(TAG, "onDestroy()")
    }

    override fun onPause() {
        super.onPause()
        Log.i(TAG, "onPause()")
    }

    override fun onStop() {
        super.onStop()
        Log.i(TAG, "onStop()")
    }

    override fun onStart() {
        super.onStart()
        Log.i(TAG, "onStart()")
    }

    override fun onResume() {
        super.onResume()
        Log.i(TAG, "onResume()")
    }
    companion object{
        var TAG  = "메인 액티비티"
    }
}
~~~

ServiceActivity.kt
~~~Kotlin

//서비스 클래스를 상속받는다.
class SecondActivity : android.app.Service() {

    lateinit var mp : MediaPlayer // 음악 재생을 위한 객체 생성

    // 다른 구성요소가 서비스에 바인드되고자 하는 경우 사용
    // onBind는 항상 구현해야하지만 사용하지 않을 경우 return null을 하면됨
    override fun onBind(p0: Intent?): IBinder? {
        return null
    }

    // 서비스 시작 명령을 내림.
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        Log.i("서비스 테스트", "onStartCommand()")
        mp = MediaPlayer.create(this, R.raw.song1) // 음악을 재생할 화면과 음악 파일 선택
        mp.isLooping = true // 음악 반복재생 설정
        mp.start() // 재생
        return super.onStartCommand(intent, flags, startId)
    }

    override fun onCreate() {
        Log.i("서비스 테스트", "onCreate()")
        super.onCreate()
    }

    override fun onDestroy() {
        Log.i("서비스 테스트", "onDestroy()")
        mp.stop() // 음악 중지 코드
        super.onDestroy()
    }

}
~~~

## 브로드캐스트 리시버
----
문자 메시지도착, 배터리 방전, 배터리 상태 확인 등 **신호를 받아서 처리하는 것이 브로드캐스트임.**  
참고로 이들은 `ACTION`이라 부르며 `ACTION`은 암묵적 intent였다.  

[배터리 상태와 관련된 액션]
1. ACTION_BATTERY_CHANGED : 배터리 상태 변경
2. ACTION_BATTERY_LOW : 배터리가 거의 방전
3. ACTION_BATTERY_OKAY : 방전에서 정상 수준으로 돌아온 경우

### Kotlin 예제 보기

MainActivity.kt
~~~Kotlin
class MainActivity : Activity() {
    lateinit var ivBattery: ImageView
    lateinit var edtBattery: EditText

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        title = "배터리 상태 체크"

        ivBattery = findViewById<ImageView>(R.id.ivBattery)
        edtBattery = findViewById<EditText>(R.id.edtBattery)

    }

    // 브로그캐스트 객채 생성
    var br: BroadcastReceiver = object : BroadcastReceiver() {
        //이때 인자로 넘어오는 intent의 경우 android os가 onResume을 넣어줌
        override fun onReceive(context: Context, intent: Intent) {
            var action = intent.action // android os가 액션을 넘김
            if (action == Intent.ACTION_BATTERY_CHANGED) { // 배터리 상태 변경
                var remain = intent.getIntExtra(BatteryManager.EXTRA_LEVEL, 0) //배터리 잔량 확인 (key값, 초기값)
                edtBattery.setText("현재 충전량 : $remain\n")

                // 잔량에 따른 작업
                if (remain >= 90)
                    ivBattery.setImageResource(R.drawable.battery_100)
                else if (remain >= 70)
                    ivBattery.setImageResource(R.drawable.battery_80)
                else if (remain >= 50)
                    ivBattery.setImageResource(R.drawable.battery_60)
                else if (remain >= 10)
                    ivBattery.setImageResource(R.drawable.battery_20)
                else
                    ivBattery.setImageResource(R.drawable.battery_0)

                // 배터리 충전 중 액션 
                var plug = intent.getIntExtra(BatteryManager.EXTRA_PLUGGED, 0)
                when (plug) {
                    0 -> edtBattery.append("전원 연결 : 안됨")
                    BatteryManager.BATTERY_PLUGGED_AC -> edtBattery.append("전원 연결 : 어댑터 연결됨")
                    BatteryManager.BATTERY_PLUGGED_USB -> edtBattery.append("전원 연결 : USB 연결됨")
                }
            }
        }
    }
    override fun onPause() {
        super.onPause()
        unregisterReceiver(br) // 브로드캐스트 등록 해제
    }
    
    // 인텐트 필터를 생성(매니페스트에 작성하는 작업을 대체하는 것임 신경쓰지말자)
    // 인텐트 필터에 있는 액션, 서비스만 동작 가능함
    override fun onResume() {
        super.onResume()
        var iFilter = IntentFilter()
        iFilter.addAction(Intent.ACTION_BATTERY_CHANGED)
        registerReceiver(br, iFilter) // 객체, 액션이 추가된 필터
    }
}
~~~

## 콘텐트 프로바이더
----
**안드로이드는 보안상 앱에서 사용하는 데이터를 외부에서 접근할 수 없다.**  
떄문에 외부 앱에서 사용하도록 하려면 콘텐트 프로바이더를 만들어야함.(`ContentResolver`클래스 사용)
> 여담으로 피싱 앱이 동작하는 원리가 이런 콘텐트 프로바이더를 활용해서 정보를 빼감.

URI(Uniform Resource Identifier) : 콘텐트 프로바이더에서 제공하는 데이터에 접근하기 위한 주소("content://패키지명/경로/아이디" 형식)  

----
### 안드로이드에서 제공하는 콘텐트 프로바이더

1. 전화 기록
2. 연락처
3. 이미지 목록
4. 동영상 목록

----

인텐트와 차이점
> 인텐트 : 액티비티 <-------> 액티비티  
> 콘텐트 프로바이더 : 앱 <--------> 앱

### Kotlin 코드 예시

~~~Kotlin
class MainActivity : Activity() {
    lateinit var btnCall: Button
    lateinit var edtCall: TextView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        ActivityCompat.requestPermissions(this, arrayOf(Manifest.permission.READ_CALL_LOG), Context.MODE_PRIVATE) 
        // 권한 요청 팝업(매니페스트에 권한을 등록해둬도 코드는 필요함)

        btnCall = findViewById<Button>(R.id.btnCall)
        edtCall = findViewById<TextView>(R.id.edtCall)
        btnCall.setOnClickListener {
            edtCall.setText(findCallHistory())
        }
    }

    // 전화 기록 파싱
    fun findCallHistory(): String {

        var callSet = arrayOf(CallLog.Calls.DATE, CallLog.Calls.TYPE, CallLog.Calls.NUMBER, CallLog.Calls.DURATION)

        // 콘텐트 프로바이더에게 명령
        var c = contentResolver.query(CallLog.Calls.CONTENT_URI, callSet, null, null, null)

        if ( c!!.count == 0 ) // 통화기록이 0개
            return "통화기록 없음"

        var callBuff = StringBuffer() // 최대 100 통화 저장(StringBuffer의 특징)
        callBuff.append("\n날짜 : 구분 : 전화번호 : 통화시간\n\n")
        c.moveToFirst() // DB에서 커서를 의미함( 처음에는 -1번 행에 위치해서 이동시켜야함)
        do {
            var callDate = c.getLong(0) // 0번 컬럼
            var datePattern = SimpleDateFormat("yyyy-MM-dd")
            var date_str = datePattern.format(Date(callDate))
            callBuff.append("$date_str:")
            if (c.getInt(1) == CallLog.Calls.INCOMING_TYPE)
                callBuff.append("착신 :")
            else
                callBuff.append("발신 :")
            callBuff.append(c.getString(2) + ":")
            callBuff.append(c.getString(3) + "초\n")
        } while (c.moveToNext())

        c.close()
        return callBuff.toString()
    }
}
~~~
