# Skittles
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Skittles-brightgreen.svg?style=flat)](http://android-arsenal.com/details/1/2076) [![Build Status](https://travis-ci.org/aashrairavooru/Skittles.svg)](https://travis-ci.org/aashrairavooru/Skittles)  [ ![Jcenter](https://img.shields.io/github/release/aashrairavooru/Skittles.svg?label=Jcenter) ](https://bintray.com/aashrairavooru/maven/Skittles/_latestVersion)
[
![JitPackv](https://img.shields.io/github/release/aashrairavooru/Skittles.svg?label=JitPack)](https://jitpack.io/#aashrairavooru/Skittles/)

A simple,clean api for adding PushBullet style skittles to your app for more material design glory.This library uses the <a href="https://developer.android.com/reference/android/support/design/widget/FloatingActionButton.html">FloatingActionButton</a> provided in the android design support library

<img src="art/Skittle.gif" width=196 height=350/>
<img src="art/TextSkittle.gif" width=196 height=350/>

## Guide ([Sample](sample/src/main/java/snow/skittlessample/MainActivity.java))

First some housekeeping code:

Use
[SkittleLayout](skittles/src/main/java/snow/skittles/SkittleLayout.java) as a root view in your layouts

```xml
<snow.skittles.SkittleLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/skittleLayout"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:fitsSystemWindows="true"
app:mainSkittleColor="@color/material_deep_teal_500"
app:mainSkittleIcon="@drawable/ic_android_white_18dp"
tools:context=".MainActivity">

<android.support.design.widget.AppBarLayout
android:id="@+id/appbar"
android:layout_width="match_parent"
android:layout_height="@dimen/appBarMaxHeight"
android:fitsSystemWindows="true"
android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">
...

</snow.skittles.SkittleLayout>
```

Some further housekeeping...

Declare a [SkittleBuilder](skittles/src/main/java/snow/skittles/SkittleBuilder.java),used to add skittles and pass the root SkittleLayout to it

```java
SkittleLayout skittleLayout = (SkittleLayout) findViewById(R.id.skittleLayout);
//Pass false as the second param if you don't want the menu to be closed on screen tap
SkittleBuilder skittleBuilder = SkittleBuilder.newInstance((SkittleLayout) findViewById(R.id.skittleLayout), true);

```

Now for the fun part

Add skittles to your activity/fragment

```java
skittleBuilder.addSkittle(Skittle.newInstance(ContextCompat.getColor(this, R.color.barratheon),
        ContextCompat.getDrawable(this, R.drawable.barratheon_icon)));
skittleBuilder.addSkittle(Skittle.newInstance(ContextCompat.getColor(this, R.color.lannister),
        ContextCompat.getDrawable(this, R.drawable.lannister_icon)));
```

Add [TextSkittle](skittles/src/main/java/snow/skittles/TextSkittle.java) to your activity/fragment

```java
 skittleBuilder.addSkittle(new TextSkittle.Builder("Hello", ContextCompat.getColor(this, R.color.stark),
            ContextCompat.getDrawable(this, R.drawable.stark_icon)).setTextBackground(
            ContextCompat.getColor(this, android.R.color.background_light)).build());

```

Flexible callback for clicks:

+ Add a click listener(SkittleBuilder.SkittleClickListener) to the [SkittleBuilder](skittles/src/main/java/snow/skittles/SkittleBuilder.java) object
`skittleBuilder.setSkittleListener(this);`

+ This exposes two methods for Skittle and MainSkittle click events

```java
void onSkittleClick(BaseSkittle skittle, int position); 

void onMainSkittleClick();
```
[BaseSkittle](skittles/src/main/java/snow/skittles/BaseSkittle.java) is an interface that every skittle implements

```java
public void onSkittleClick(BaseSkittle skittle, int position) {
  if(skittle instanceOf TextSkittle)
   ...
  else if(skittle instanceOf Skittle)
   ...
}
```
Here the `position` does not include the mainSkittle and starts from `0`

You can now create your very own Skittle you just have to implement the [BaseSkittle](skittles/src/main/java/snow/skittles/BaseSkittle.java), check [TextSkittle](skittles/src/main/java/snow/skittles/TextSkittle.java) or [Skittle](skittles/src/main/java/snow/skittles/Skittle.java) for further reference

## Snackbar Support
<img src="art/Snackbar.gif" width=196 height=350/>
<img src="art/SnackbarDismiss.gif" width=196 height=350/>

When using snackbars ensure that you use [SkittleContainer](skittles/src/main/java/snow/skittles/SkittleContainer.java)

```java
Snackbar.make(skittleLayout.getSkittleContainer(), "Skittle Pressed", Snackbar.LENGTH_LONG)
.show();
```

## Gradle
```groovy
dependencies{
compile 'com.rlj.library:skittles:4.1.1'
}
```

See the **[Sample](sample/src/main/java/snow/skittlessample/MainActivity.java)** and **[JavaDoc](http://aashrairavooru.github.io/Skittles/)** for further guidance

## Upcoming
+ Better support for animations
+ Option for adding skittles by xml (inspired by Navigation View)


# Taste the rainbow
![Skittles](art/Taste the rainbow.jpg)
