---
title: '[Android] How to build an Android Floating Action Button Menu'
tags:
  - Android
  - Material Design
date: 2016-11-26 13:20:42
thumbnail: '/images/how-to-build-an-android-floating-action-button-menu.png'
---


Hi,

I'm a FullStack Developer (J2EE, JS, SQL), I know Java but not explicitly Android Development guidelines.
So I currently joining the open-source team of [NewPipe : A free lightweight Youtube frontend for Android](https://github.com/TeamNewPipe/NewPipe/ "NewPipe Project") to improve my skills.

During the development of PlayList support on NewPipe a question came to mind : 
> How to make a correct menu in material design under android ?
 
I have needing using a new material menu provide by **_Floating Action Button_** (like Inbox, Hangout, ...) for `minSdkVersion=14`

## How to proceed ? 

After some search on internet, I found these [stackoverflow thread](https://stackoverflow.com/questions/30699302/android-design-support-library-fab-menu) and it's list four libs for made the job:
```
 Rapid Floating Button (wangjiegulu)
 Floating Action Button (Clans)
 Floating Action Button (makovkastar)
 Android Floating Action Button (futuresimple)
 ```
 But in the comment one person used [Android Floating Action Button (futuresimple)](https://github.com/futuresimple/android-floating-action-button) in production to more than 100K users and he never had any issues for the lib, so I choice the same of him.
 
## Adding in the code

### Edit the .gradle
You just need to add the _**Android Floating Action Button**_ lib on your gradle file
```
    compile 'com.getbase:floatingactionbutton:1.10.1'
```
### Add on XML files


#### 1. Drawable file
##### [fab_label_background.xml](https://github.com/BlenderViking/NewPipe/blob/4239599ffc7578ee5752d972327b6fc0a2294b34/app/src/main/res/drawable/fab_label_background.xml)
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="#B2000000"/>
    <padding
        android:left="16dp"
        android:top="4dp"
        android:right="16dp"
        android:bottom="4dp"/>
    <corners
        android:radius="2dp"/>
</shape>
```
#### 2. Values's files
##### [colors.xml](https://github.com/BlenderViking/NewPipe/blob/4239599ffc7578ee5752d972327b6fc0a2294b34/app/src/main/res/values/colors.xml#L37)
```xml
<!-- floating actions buttons -->
<color name="black">#000000</color>
<color name="half_black">#808080</color>
```
##### [styles.xml](https://github.com/BlenderViking/NewPipe/blob/4239599ffc7578ee5752d972327b6fc0a2294b34/app/src/main/res/values/styles.xml#L83)
```xml
<style name="menu_labels_style">
    <item name="android:background">@drawable/fab_label_background</item>
    <item name="android:textColor">@color/white</item>
</style>
```
#### 2. Layout's files

##### [floating_menu.xml](https://github.com/BlenderViking/NewPipe/blob/5b2ada744f49d056c2a786e6bf50e14c4ba2716c/app/src/main/res/layout/floating_menu.xml)
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <View
        android:id="@+id/floating_menu_background"
        android:visibility="gone"
        android:background="#55000000"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

    <com.getbase.floatingactionbutton.FloatingActionsMenu xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/multiple_actions_menu"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true"
        app:layout_anchorGravity="center_vertical|right"
        app:fab_addButtonColorNormal="@color/black"
        app:fab_addButtonColorPressed="@color/half_black"
        app:fab_addButtonPlusIconColor="@color/white"
        app:fab_labelStyle="@style/menu_labels_style"
        app:fab_expandDirection="up"
        android:layout_marginBottom="16dp"
        android:layout_marginRight="16dp"
        android:layout_marginEnd="16dp">

        <com.getbase.floatingactionbutton.FloatingActionButton
            android:id="@+id/action_add_to_queue"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:fab_icon="@drawable/ic_queue_white_24dp"
            app:fab_colorNormal="@color/black"
            app:fab_title="Add into existing queue"
            app:fab_colorPressed="@color/half_black" />

        <com.getbase.floatingactionbutton.FloatingActionButton
            android:id="@+id/action_replace_queue"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:fab_icon="@drawable/ic_headset_white_24dp"
            app:fab_colorNormal="@color/black"
            app:fab_title="Listing in background"
            app:fab_colorPressed="@color/half_black" />

    </com.getbase.floatingactionbutton.FloatingActionsMenu>
</RelativeLayout>
```

Don't forgive to add on your [parent layout](https://github.com/BlenderViking/NewPipe/blob/0daddb0be368c5eca03bb7a28ee45b2e142358e6/app/src/main/res/layout/activity_playlist_external.xml#L88) the xml inclusion of the new layout :
```xml
<include layout="@layout/floating_menu" />
```

## Add on Java Activity part

Add the following import
```java
import com.getbase.floatingactionbutton.FloatingActionButton;
import com.getbase.floatingactionbutton.FloatingActionsMenu;
```
Add create the method for init the FloatingActionButton menu (call inside your init view)
```java
private void initFloatingActionButtonMenu() {

    final FloatingActionsMenu floatingActionsMenu = (FloatingActionsMenu) findViewById(R.id.multiple_actions_menu);

    final FloatingActionButton actionAddToQueue = (FloatingActionButton) findViewById(R.id.action_add_to_queue);
    actionAddToQueue.setOnClickListener(new View.OnClickListener() {

            @Override


        public void onClick(View view) {
            floatingActionsMenu.collapse();
        }


    });

    final FloatingActionButton actionAddToQueueAndPlay = (FloatingActionButton) findViewById(R.id.action_replace_queue);
    actionAddToQueueAndPlay.setOnClickListener(new View.OnClickListener() {

            @Override
 
 
        public void onClick(View view) {
            floatingActionsMenu.collapse();
        }


    });
    
    final View backgroundOpac = findViewById(R.id.floating_menu_background);
    backgroundOpac.setOnClickListener(new View.OnClickListener() {
    
    @Override
    
    
        public void onClick(View view) {
            floatingActionsMenu.collapse();
        }


    });

    floatingActionsMenu.setOnFloatingActionsMenuUpdateListener(new FloatingActionsMenu.OnFloatingActionsMenuUpdateListener() {
        @Override
    
    
        public void onMenuExpanded() {
            backgroundOpac.setVisibility(View.VISIBLE);
        }
        @Override
    
    
        public void onMenuCollapsed() {
            backgroundOpac.setVisibility(View.GONE);
        }


    });

}

```

And it's work :)

![Floating Action Button Menu](/images/how-to-build-an-android-floating-action-button-menu-1.png "Floating Action Button Menu in NewPipe")

PS: If you needing an Android support with `minSdkVersion=4` check [here](https://github.com/str4d/android-floating-action-button). 