# RoundCorners
比较常用的ViewGroup和View的圆角实现，一发治好设计的圆角病。

### [Demo](https://fir.im/gfhw)

### 效果预览

|![](images/07.png)|![](images/01.png)|![](images/02.png)|
|---|---|---|
|![](images/04.png)|![](images/05.png)|![](images/06.png)|
|![](images/03.png)|![](images/08.png)|![](images/09.png)|

### 特点
* LinearLayout、RelativeLayout、FrameLayout支持圆角
* ImageView、TextView、View支持圆角
* 支持圆形图片：CircleImageView
* 支持边框，不遮挡图片
* 使用xml进行配置，使用简单
* ......

### 基本用法
**Step 1. 添加JitPack仓库**
在项目根目录下的 `build.gradle` 中添加仓库:
``` gradle
allprojects {
    repositories {
        ...
        maven { url "https://jitpack.io" }
    }
}
```
**Step 2. 添加项目依赖**
``` gradle
dependencies {
    implementation 'com.github.KuangGang:RoundCorners:1.0.2'
}
```
**Step 3. 在布局文件中添加需要的RoundCorners**
```
<com.kproduce.roundcorners.CircleImageView
    android:layout_width="200dp"
    android:layout_height="200dp"
    android:src="@mipmap/ic_test"
    app:rStrokeColor="@android:color/holo_red_dark"
    app:rStrokeWidth="5dp" />

<com.kproduce.roundcorners.RoundImageView
    android:layout_width="200dp"
    android:layout_height="200dp"
    android:scaleType="centerCrop"
    android:src="@mipmap/ic_test"
    app:rRadius="30dp"/>

<com.kproduce.roundcorners.RoundTextView
    android:layout_width="200dp"
    android:layout_height="100dp"
    android:background="@android:color/holo_blue_dark"
    android:gravity="center"
    android:text="Hello!"
    android:textColor="@android:color/white"
    android:textSize="40sp"
    app:rRightRadius="30dp" />

<com.kproduce.roundcorners.RoundRelativeLayout
    android:layout_width="200dp"
    android:layout_height="200dp"
    app:rTopRightRadius="30dp"
    app:rBottomRightRadius="30dp"
    app:rStrokeColor="@android:color/holo_green_dark"
    app:rStrokeWidth="5dp">

    <View
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@android:color/holo_blue_dark" />
</com.kproduce.roundcorners.RoundRelativeLayout>

<com.kproduce.roundcorners.RoundTextView
    android:layout_width="200dp"
    android:layout_height="100dp"
    android:background="@android:color/holo_blue_dark"
    android:gravity="center"
    android:text="Hello!"
    android:textColor="@android:color/white"
    android:textSize="40sp"
    app:rLeftRadius="50dp"
    app:rRightRadius="50dp"/>
……
```

### 支持的属性、方法
|属性名|含义|默认值
|---|---|---|
|rRadius|统一设置四个角的圆角半径|0dp
|rLeftRadius|左边两个角圆角半径|0dp
|rRightRadius|右边两个角圆角半径|0dp
|rTopRadius|上边两个角圆角半径|0dp
|rBottomRadius|下边两个角圆角半径|0dp
|rTopLeftRadius|左上角圆角半径|0dp
|rTopRightRadius|右上角圆角半径|0dp
|rBottomLeftRadius|左下角圆角半径|0dp
|rBottomRightRadius|右下角圆角半径|0dp
|rStrokeWidth|边框宽度|0dp
|rStrokeColor|边框颜色|Color.WHITE

### 原理浅解
[Android View的绘制流程](https://github.com/KuangGang/RoundCorners)。
View的绘制看一下这篇文章即可，代码版本比较早，但是逻辑基本相同。
1. 使用Path的addRoundRect方法，将需要剪切的圆角半径进行设置。
2. 所有View和ViewGroup的绘制都需要经过draw方法，在draw结束之后使用第一步的Path进行画布切割。
3. 注意在draw中减少创建对象次数。

### 版本记录
|版本号|更新内容|
|---|---|
|1.0.2|1.增加边框<br>2.增加RoundButton/RoundViewPager|
|1.0.1|1.修复低版本系统圆角View黑框问题<br>2.增加CircleImageView|
|1.0.0|First Version|
