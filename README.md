# AndroidBasicBoilerplateSolution
SpeedUp The Idea Development Process

## Android Toolbar With Color Change BoilerPlater

> root/build.gradle

```gradle

apply plugin: 'com.android.application'

android {
    compileSdkVersion 28
    defaultConfig {
        applicationId "io.example.appname"
        minSdkVersion 24
        targetSdkVersion 28
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])

    implementation 'com.android.support:appcompat-v7:28.0.0'
    implementation 'com.android.support:design:28.0.0'
    implementation 'com.android.support:cardview-v7:28.0.0'
    implementation 'com.android.support:support-v4:28.0.0'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    implementation 'com.google.android.material:material:1.0.0'
    implementation 'com.squareup.picasso:picasso:2.71828'

    implementation 'androidx.appcompat:appcompat:1.1.0'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    implementation "com.android.support:support-core-utils:28.0.0"

    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
    implementation 'com.google.android.material:material:1.0.0'
}

```


> MainActivity.java

```java


import androidx.appcompat.app.ActionBarDrawerToggle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.drawerlayout.widget.DrawerLayout;

import android.content.res.Configuration;
import android.os.Bundle;
import android.view.MenuItem;
import android.view.View;

public class MainActivity extends AppCompatActivity {

    Toolbar mToolbar;
    DrawerLayout mDrawer;
    ActionBarDrawerToggle mDrawerToggle;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mToolbar = findViewById(R.id.toolbar);
        mDrawer = findViewById(R.id.home_drawer);

        setSupportActionBar(mToolbar);

        // set the toolbar title
        if (getSupportActionBar() != null) {
            getSupportActionBar().setTitle(R.string.app_name);
            getSupportActionBar().setDisplayHomeAsUpEnabled(true);
            getSupportActionBar().setDisplayShowHomeEnabled(true);

            mDrawerToggle = new ActionBarDrawerToggle(this, mDrawer, mToolbar, R.string.app_name, R.string.app_name) {

                public void onDrawerClosed(View view) {
                    supportInvalidateOptionsMenu();
                }

                public void onDrawerOpened(View drawerView) {
                    supportInvalidateOptionsMenu();
                }
            };

            mDrawerToggle.setDrawerIndicatorEnabled(true);
            mDrawer.setDrawerListener(mDrawerToggle);
            mDrawerToggle.syncState();

        }

    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        if (item.getItemId() == android.R.id.home) {
            onBackPressed();
        }
        return super.onOptionsItemSelected(item);
    }

    @Override
    protected void onPostCreate(Bundle savedInstanceState) {
        super.onPostCreate(savedInstanceState);
        mDrawerToggle.syncState();
    }

    @Override
    public void onConfigurationChanged(Configuration newConfig) {
        super.onConfigurationChanged(newConfig);
        mDrawerToggle.onConfigurationChanged(newConfig);
    }

}

```

> activity_main.xml

```XML

<?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/home_drawer"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:context=".MainActivity">

    <androidx.coordinatorlayout.widget.CoordinatorLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@android:color/white">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="@android:color/white"
            android:orientation="vertical">

            <include layout="@layout/toolbar" />

            <!--            ScrollerView-->

        </LinearLayout>

    </androidx.coordinatorlayout.widget.CoordinatorLayout>

    <com.google.android.material.navigation.NavigationView
        android:id="@+id/home_drawer_navView"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:background="@android:color/white"
        app:headerLayout="@layout/navigation_drawer_header"
        app:itemTextAppearance="@style/SansMediumTextViewStyle"
        app:menu="@menu/drawer_menu" />

</androidx.drawerlayout.widget.DrawerLayout>

```

> menu/drawer_menu.xml

```XML

<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <!--        android:icon="@drawable/ic_license_plate"-->
    <item
        android:id="@+id/company_repo"
        android:icon="@drawable/ic_globe"
        android:title="Company Repository" />

    <item
        android:id="@+id/library"
        android:icon="@drawable/ic_stock"
        android:title="Library" />

    <item
        android:id="@+id/notifications"
        android:icon="@drawable/ic_notification"
        android:title="Notifications" />

    <group android:id="@+id/danger_zone">
        <item
            android:id="@+id/payments"
            android:icon="@drawable/ic_payments"
            android:title="Payments" />
        <item
            android:id="@+id/settings"
            android:icon="@drawable/ic_settings"
            android:title="Settings" />
        <item
            android:id="@+id/readme"
            android:icon="@drawable/ic_rate_us"
            android:title="Readme" />
        <item
            android:id="@+id/logout"
            android:icon="@drawable/ic_logout"
            android:title="Logout" />
    </group>

</menu>

```

> values/colors.xml

```XML

<resources>
    <color name="colorPrimary">#fff</color>
    <color name="colorPrimaryDark">#fff</color>
    <color name="colorAccent">#000</color>
</resources>

```

> values/styles.xml

```XML

<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimary</item>
        <item name="colorAccent">@color/colorAccent</item>

        <item name="colorControlNormal">#000</item>
        <item name="android:windowLightStatusBar">true</item>
        <item name="android:statusBarColor">@color/colorPrimary</item>
        <item name="android:windowDrawsSystemBarBackgrounds">true</item>
        <item name="android:windowTranslucentNavigation">false</item>
        <item name="android:navigationBarColor">#000</item>

    </style>

    <style name="AppToolbar" parent="ThemeOverlay.AppCompat.Dark.ActionBar">
        <item name="android:textColorPrimary">@color/colorAccent</item>
        <item name="android:textColorSecondary">@color/colorAccent</item>
    </style>

</resources>

```

> layout/navigation_drawer_header.xml

```XML

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginTop="25dp"
    android:orientation="vertical"
    android:padding="10dp">

    <TextView
        android:id="@+id/textView8"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginEnd="8dp"
        android:fontFamily="sans-serif-thin"
        android:text="@string/app_name"
        android:textAlignment="center"
        android:textColor="@android:color/black"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>

```

> layout/toolbar.xml

```XML

<com.google.android.material.appbar.AppBarLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/appBarLayout"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:elevation="0dp">

    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:minHeight="?attr/actionBarSize"
        android:theme="@style/AppToolbar" />

</com.google.android.material.appbar.AppBarLayout>

```
