# Android Toolbar 工具栏演示

## 简介

本 Demo 演示 Toolbar 的基本用法，展示如何创建 Material Design 工具栏。

## 基本原理

Toolbar 是 Material Design 提供的工具栏组件，替代了早期的 ActionBar。它更灵活，可以放置在屏幕任意位置，支持自定义布局。

Toolbar 的特点：
- 可自定义位置（顶部、底部）
- 支持添加标题、菜单、搜索等
- 可以与 ActionBar 共存或替代它
- 支持折叠效果

## 启动和使用

### 环境要求
- Android Studio
- JDK 17
- Gradle 8.x

### 安装和运行

1. 用 Android Studio 打开项目
2. 连接 Android 设备或模拟器
3. 点击 Run 运行

### 使用方法
- 运行后将看到顶部显示的 Toolbar

## 教程

### 什么是 Toolbar？

Toolbar 是 Android 5.0 引入的 Material Design 组件，作为 ActionBar 的现代替代品。它提供了更大的灵活性，可以放置在任意位置，并支持丰富的自定义功能。

### 基本用法

1. 在布局中添加 Toolbar：

```xml
<androidx.appcompat.widget.Toolbar
    android:id="@+id/toolbar"
    android:layout_width="match_parent"
    android:layout_height="?attr/actionBarSize"
    android:background="?attr/colorPrimary" />
```

2. 设置为 ActionBar：

```kotlin
val toolbar = findViewById<Toolbar>(R.id.toolbar)
setSupportActionBar(toolbar)
supportActionBar?.title = "标题"
```

### 设置菜单

1. 创建菜单资源文件（res/menu/menu_main.xml）：

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/action_search"
        android:icon="@android:drawable/ic_menu_search"
        app:showAsAction="ifRoom"
        android:title="搜索" />
</menu>
```

2. 在 Activity 中处理菜单：

```kotlin
override fun onCreateOptionsMenu(menu: Menu): Boolean {
    menuInflater.inflate(R.menu.menu_main, menu)
    return true
}

override fun onOptionsItemSelected(item: MenuItem): Boolean {
    return when (item.itemId) {
        R.id.action_search -> true
        else -> super.onOptionsItemSelected(item)
    }
}
```

### 添加导航图标

```kotlin
supportActionBar?.setDisplayHomeAsUpEnabled(true)
supportActionBar?.setHomeAsUpIndicator(android.R.drawable.ic_menu_revert)
```

## 关键代码详解

### MainActivity.kt

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // 1. 获取 Toolbar 组件
        val toolbar = findViewById<Toolbar>(R.id.toolbar)

        // 2. 将 Toolbar 设置为 Activity 的 ActionBar
        // 这会让 Toolbar 具有 ActionBar 的功能
        setSupportActionBar(toolbar)

        // 3. 设置标题
        // 通过 supportActionBar 设置标题
        supportActionBar?.title = "Toolbar 演示"
    }
}
```

### activity_main.xml

```xml
<!-- 根布局：垂直线性布局 -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <!-- Toolbar 组件 -->
    <!-- 使用 ?attr/actionBarSize 作为高度，自动适配 -->
    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        <!-- 使用主题的 colorPrimary 作为背景色 -->
        android:background="?attr/colorPrimary" />

    <!-- 内容区域 -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Toolbar 工具栏演示"
        android:gravity="center"
        android:padding="32dp" />
</LinearLayout>
```

### Toolbar vs ActionBar

| 特性 | Toolbar | ActionBar |
|------|---------|-----------|
| 位置 | 任意 | 固定顶部 |
| 自定义 | 完全自定义 | 有限 |
| 动画 | 支持 | 不支持 |
| 折叠 | 支持 | 不支持 |
