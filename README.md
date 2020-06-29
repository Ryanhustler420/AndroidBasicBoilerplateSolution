# AndroidBasicBoilerplateSolution
SpeedUp The Idea Development Process

## Android Toolbar & Side Drawer With Color Change BoilerPlater

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
            mDrawer.addDrawerListener(mDrawerToggle);
            mDrawerToggle.syncState();

        }
        
        
        setNavigationViewListener();

    }
    
        @Override
        public void onBackPressed() {
            if (mDrawer.isDrawerOpen(GravityCompat.START)) {
                mDrawer.closeDrawer(GravityCompat.START);
                return;
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
    
    @Override
    public boolean onNavigationItemSelected(@NonNull MenuItem menuItem) {
        if (!isAboutToMoveAnotherActivity) {
            switch (menuItem.getItemId()) {
                case R.id.company_repo:
                    showToast("company Repo");
                    break;
                case R.id.library:
                    showToast("library activity");
                    break;
            }
        }
        return true;
    }
    
    public void setNavigationViewListener() {
        NavigationView navigationView = findViewById(R.id.home_drawer_navView);
        navigationView.setNavigationItemSelectedListener(this);
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

## Pinch To Zoom Image

[library](https://github.com/stfalcon-studio/FrescoImageViewer)


> root/build.gradle

```gradle

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])

    implementation 'com.android.support:appcompat-v7:28.0.0'
    implementation 'com.android.support:design:28.0.0'
    implementation 'com.android.support:cardview-v7:28.0.0'
    implementation 'com.android.support:support-v4:28.0.0'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    implementation 'com.google.android.material:material:1.0.0'
    implementation 'com.squareup.picasso:picasso:2.71828'

    // Image Zooming
    implementation 'com.github.stfalcon:frescoimageviewer:0.5.0'
    implementation 'com.facebook.fresco:fresco:1.9.0'
    
    implementation 'androidx.appcompat:appcompat:1.1.0'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    implementation "com.android.support:support-core-utils:28.0.0"

    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
    implementation 'com.google.android.material:material:1.0.0'
}

```

> activity_main.xml

```XML

<Button
    android:id="@+id/load_img_button"
    android:layout_width="200dp"
    android:layout_height="100dp"
    android:layout_gravity="center_horizontal"
    android:text="Load Image" />

```

> controller/AndroidManifest.xml

```XML

<uses-permission android:name="android.permission.INTERNET" />

<application android:name=".controller.AppController"> </application>

```

> MainActivity.java

```java

package io.raisehand.raisehandrepositoryenv;

import androidx.appcompat.app.ActionBarDrawerToggle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.drawerlayout.widget.DrawerLayout;

import android.content.res.Configuration;
import android.os.Bundle;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;

import com.facebook.drawee.backends.pipeline.Fresco;
import com.stfalcon.frescoimageviewer.ImageViewer;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        /*
         new ImageViewer.Builder<>(this, images)
        .setStartPosition(startPosition)
        .hideStatusBar(false)
        .allowZooming(true)
        .allowSwipeToDismiss(true)
        .setBackgroundColorRes(colorRes)
        //.setBackgroundColor(color)
        .setImageMargin(margin)
        //.setImageMarginPx(marginPx)
        .setContainerPadding(this, dimen)
        //.setContainerPadding(this, dimenStart, dimenTop, dimenEnd, dimenBottom)
        //.setContainerPaddingPx(padding)
        //.setContainerPaddingPx(start, top, end, bottom)
        .setCustomImageRequestBuilder(imageRequestBuilder)
        .setCustomDraweeHierarchyBuilder(draweeHierarchyBuilder)
        .setImageChangeListener(imageChangeListener)
        .setOnDismissListener(onDismissListener)
        .setOverlayView(overlayView)
        .show();
        * */

        Button load_img_button = findViewById(R.id.load_img_button);

        ArrayList<String> imagesUrl = new ArrayList<>();
        imagesUrl.add("https://avatars2.githubusercontent.com/u/25275856?s=460&v=4");

        load_img_button.setOnClickListener(v ->
                new ImageViewer.Builder<>(this, imagesUrl)
                        .setStartPosition(0)
                        .show());

    }

}


```

> controller/AppController.java

```java

import android.app.Application;

import com.facebook.drawee.backends.pipeline.Fresco;
import com.facebook.imagepipeline.core.ImagePipelineConfig;
import com.facebook.imagepipeline.decoder.SimpleProgressiveJpegConfig;

public class AppController extends Application {

    private static AppController instance;

    @Override
    public void onCreate() {
        super.onCreate();
        instance = this;

        // if you expect to open really large images, use configuration below for better performance
        ImagePipelineConfig config = ImagePipelineConfig.newBuilder(this)
                .setProgressiveJpegConfig(new SimpleProgressiveJpegConfig())
                .setResizeAndRotateEnabledForNetwork(true)
                .setDownsampleEnabled(true)
                .build();

        // initialize Fresco in your Application class
        Fresco.initialize(this, config);
    }

    public static AppController getInstance() {
        return instance;
    }
}


```

## Implementing Log Manager Using Splunk Mint

> build.gradle

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
        multiDexEnabled true
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility = 1.8
        targetCompatibility = 1.8
    }
    allprojects {
        repositories {
            maven { url "https://jitpack.io" }
        }
    }
}

repositories {
    maven {
        url uri('mint-plugin-repo-5.2.5')
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    
    // error testing library
    implementation 'com.splunk:mint-android-sdk:5.2.5' 


    implementation 'com.android.support:appcompat-v7:28.0.0'
    implementation 'com.android.support:design:28.0.0'
    implementation 'com.android.support:cardview-v7:28.0.0'
    implementation 'com.android.support:support-v4:28.0.0'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'

    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
    implementation 'com.google.android.material:material:1.0.0'
}


```

> Paste The  **mint-plugin-repo-5.2.5.jar** file to app level not inside **libs**. using Project view instead of android view in side inspecter

> MainActivity.java

```java

    import com.splunk.mint.Mint;

    // https://docs.splunk.com/Documentation/MintAndroidSDK/latest/DevGuide/Requirementsandinstallation
    new Thread() {
        @Override
        public void run() {
            super.run();
            // Set the application environment
            Mint.setApplicationEnvironment(Mint.appEnvironmentStaging);
            Mint.initAndStartSession(getApplication(), "API Key");
        }
    }.start();

```

## Light Status Bar

```java

    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
        getWindow().getDecorView().setSystemUiVisibility(View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR);
    }

```

## Custome Toast

> toast.xml

```xml

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/toast_layout_root"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="@dimen/padding_small_8dp">

    <androidx.cardview.widget.CardView
        android:id="@+id/base_card"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:cardBackgroundColor="@color/colorAccent"
        app:cardCornerRadius="@dimen/card_cornerRadius_25dp"
        app:cardElevation="@dimen/card_elevation_15dp"
        app:cardUseCompatPadding="true">

        <TextView
            android:id="@+id/text"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:fontFamily="sans-serif-medium"
            android:padding="@dimen/padding_medium_16dp"
            android:text="@string/app_name"
            android:textColor="@color/colorPrimary" />

    </androidx.cardview.widget.CardView>

</LinearLayout>

```

> MainActivity.java

```java

public class MainActivity extends AppCompatActivity {

    LayoutInflater inflater;
    View toastLayout;
    TextView toastText;
    Toast toast;
    
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
            
            initToastLayout();
            
            new Handler().postDelayed(new Runnable() {
                @Override
                public void run() {
                    showToast("Stay Positive", 1);    
                }
             }, 2000);
            
            new Handler().postDelayed(new Runnable() {
                @Override
                public void run() {
                    showToastWithColor("Stay Cool", 1, R.color.green);
                }
             }, 4000);
        }
    }
    
    // Don't use this function at all. this is to initialize the toast layout and inflate for you to use. 
    private void initToastLayout() {
        inflater = getLayoutInflater();
        toastLayout = inflater.inflate(R.layout.toast, findViewById(R.id.toast_layout_root));
        toastText = toastLayout.findViewById(R.id.text);
        toast = new Toast(getApplicationContext());
        toast.setGravity(Gravity.BOTTOM, 0, 0);
        toast.setView(toastLayout);
    }

    // call this when  you want to show custom toast message., well we can change the color of background. but later. we will implement this.
    protected void showToast(String message, int duration) {
        toastText.setText(message);
        toast.setDuration(duration > 0 ? Toast.LENGTH_LONG : Toast.LENGTH_SHORT);
        toast.show();
    }

    protected void showToastWithColor(String message, int duration, int colorInRes) {
        CardView cardView = toastLayout.findViewById(R.id.base_card);
        cardView.setCardBackgroundColor(ContextCompat.getColor(getApplicationContext(), colorInRes));
        toastText.setText(message);
        toast.setDuration(duration > 0 ? Toast.LENGTH_LONG : Toast.LENGTH_SHORT);
        toast.show();
    }

}

```

## Use Custom Font

> Make A Directory In Project View. **src > main > assets > fonts** paste your .ttf files

```java

    AssetManager am = getApplicationContext().getAssets();

    Typeface typeface = Typeface.createFromAsset(am, String.format(Locale.US, "fonts/%s", "ProductSans-Light.ttf"));
    TextView flavour = findViewById(R.id.flavour);
    TextView indexFigure = findViewById(R.id.indexFigure);

    flavour.setTypeface(typeface);
    indexFigure.setTypeface(typeface);

```

> For [entire application](https://www.coderefer.com/android-custom-font-entire-application/)

## Algolia Endless RecyclerView Implementation


```javaScript

/*********************************/
/* This is the structure of POJO */
/*********************************/

{
  "userId": 1,
  "id": 2,
  "title": "quis ut nam facilis et officia qui",
  "completed": false,
  "objectID": "23725092"
}

```


> AlgoliaTest.java

```java


import android.content.Context;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ProgressBar;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import com.algolia.search.saas.Client;
import com.algolia.search.saas.CompletionHandler;
import com.algolia.search.saas.Index;
import com.algolia.search.saas.Query;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.util.ArrayList;
import java.util.concurrent.atomic.AtomicInteger;

public class AlgoliaTest extends CommonAttributesActivity {

    ProgressBar mProgressBar;
    RecyclerView my_recycler_view;
    TodoAdapter todoAdapter;
    EndlessRecyclerOnScrollListener endlessRecyclerOnScrollListener;

    // Algolia Test Suit Section.
    Client client = new Client("YOUR_APP_ID", "YOUR_API_KEY");
    Index index = client.getIndex("testing"); // using testing index for testing purpose.
    Query query;

    // Meta Data Tracker Variables.
    AtomicInteger currentPage = new AtomicInteger();
    AtomicInteger totalPages = new AtomicInteger();
    int hitsPerPage = 20;
    int nextChunkLoadingThreshold = 4;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_algolia_test);

        mProgressBar = findViewById(R.id.loading_progressbar);

        // Resetting Data's
        currentPage.set(0);
        totalPages.set(0);

        // Init the Todo: Adapter and recyclerView.
        LinearLayoutManager linearLayoutManager = new LinearLayoutManager(getApplicationContext());
        todoAdapter = new TodoAdapter(getApplicationContext());

        my_recycler_view = findViewById(R.id.my_recycler_view);
        my_recycler_view.setLayoutManager(linearLayoutManager);
        my_recycler_view.setAdapter(todoAdapter);
        my_recycler_view.addOnScrollListener(setUpEndlessRecyclerView(linearLayoutManager));
        endlessRecyclerOnScrollListener.setVisibleThreshold(nextChunkLoadingThreshold);

        // Set The Query
        // Set if Any Query Available. Or Put That In Separate Method would be nice.
        // Loading All Data Using "" Empty String
        query = new Query("").setHitsPerPage(hitsPerPage);

        // Get The Data First Time.
        io();
    }

    public void io() {
        query.setPage(currentPage.get());
        index.searchAsync(query, handler);
    }

    public CompletionHandler handler = (jsonObject, e) -> {
        try {
            assert jsonObject != null;

            // Set TotalPages
            totalPages.set(jsonObject.getInt("nbPages"));

            // Check If THe Data is not right or has no "hits".length() == 0 then return;
            JSONArray jsonArray = jsonObject.getJSONArray("hits");

            if (jsonArray != null && jsonArray.length() <= 0) {
                mProgressBar.setVisibility(View.GONE);
                waitIAmDoingSomething = false;
                if (todoAdapter.getItemCount() > 0) {
                    showToast("That\'s All", 1); // this is just custome toast message cover with API.
                } else {
                    showToast("Shoot: No Match Found", 1);
                }
                return;
            }

            // While In This Section, We'll Fet the data and put inside recyclerView.
            // Create An ArrayList To Store The Received Data using Loop.
            ArrayList<Todo> todos = new ArrayList<>();

            if (jsonArray != null) {
                for (int i = 0; i < jsonArray.length(); i++) {
                    JSONObject data = jsonArray.getJSONObject(i);
                    todos.add(new Todo(data.getInt("userId"), data.getInt("id"), data.getString("title"), data.getBoolean("completed")));
                }
            }

            // Put Inside RecyclerView And Set Mandatory Data's
            todoAdapter.addTodos(todos);
            mProgressBar.setVisibility(View.GONE);

        } catch (JSONException ex) {
            ex.printStackTrace();
        }
    };

    private EndlessRecyclerOnScrollListener setUpEndlessRecyclerView(LinearLayoutManager linearLayoutManager) {
        endlessRecyclerOnScrollListener = new EndlessRecyclerOnScrollListener(linearLayoutManager) {
            @Override
            public void onLoadMore(int current_page) {
                // Load More From Here.
                if (current_page <= totalPages.get()) {
                    mProgressBar.setVisibility(View.VISIBLE);
                    currentPage.set(current_page);
                    io();
                }
            }
        };
        endlessRecyclerOnScrollListener.setVisibleThreshold(hitsPerPage);
        return endlessRecyclerOnScrollListener;
    }

    // POJO Class

    class Todo {
        private int userId;
        private int id;
        private String title;
        private boolean completed;

        Todo(int userId, int id, String title, boolean completed) {
            this.userId = userId;
            this.id = id;
            this.title = title;
            this.completed = completed;
        }

        public int getUserId() {
            return userId;
        }

        public void setUserId(int userId) {
            this.userId = userId;
        }

        public int getId() {
            return id;
        }

        public void setId(int id) {
            this.id = id;
        }

        public String getTitle() {
            return title;
        }

        public void setTitle(String title) {
            this.title = title;
        }

        public boolean isCompleted() {
            return completed;
        }

        public void setCompleted(boolean completed) {
            this.completed = completed;
        }
    }

    class TodoAdapter extends RecyclerView.Adapter<TodoAdapter.ViewHolder> {

        private Context context;
        private ArrayList<Todo> todos;

        TodoAdapter(Context context) {
            this.context = context;
            this.todos = new ArrayList<>();
        }

        public void addTodo(Todo todo) {
            this.todos.add(todo);
            notifyDataSetChanged();
        }

        public void addTodos(ArrayList<Todo> todo) {
            this.todos.addAll(todo);
            notifyDataSetChanged();
        }

        @NonNull
        @Override
        public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
            View view = LayoutInflater.from(context).inflate(R.layout.todo_single_card, null);
            return new ViewHolder(view);
        }

        @Override
        public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
            Todo todo = todos.get(position);
            holder.todo_title.setText(String.format("Title: %s", todo.getTitle()));
            holder.todo_id.setText(String.format("ID: %s", todo.getId()));
            holder.todo_completed.setText(String.format("Completed: %s", todo.isCompleted() ? "YES" : "NO"));
        }

        @Override
        public int getItemCount() {
            return todos.size();
        }

        public class ViewHolder extends RecyclerView.ViewHolder {

            TextView
                    todo_title,
                    todo_id,
                    todo_completed;

            ViewHolder(@NonNull View itemView) {
                super(itemView);
                todo_title = itemView.findViewById(R.id.todo_title);
                todo_id = itemView.findViewById(R.id.todo_id);
                todo_completed = itemView.findViewById(R.id.todo_completed);
            }
        }
    }

}


```

> EndlessRecyclerOnScrollListener.java

**Src: ** [Medium](https://medium.com/@sidhanth/android-pagination-for-algolia-recyclerviews-searches-8d7b16d9cee2)

```java


import androidx.annotation.NonNull;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

public abstract class EndlessRecyclerOnScrollListener extends RecyclerView.OnScrollListener {

    public static String TAG = EndlessRecyclerOnScrollListener.class.getSimpleName();

    private int previousTotal = 0; // The total number of items in the dataset after the last load
    private boolean loading = true; // True if we are still waiting for the last set of data to load.
    private int visibleThreshold = 0; // The minimum amount of items to have below your current scroll position before loading more.
    private int firstVisibleItem, visibleItemCount, totalItemCount;

    private int current_page = 0;
    private int total_pages = 0;

    private LinearLayoutManager mLinearLayoutManager;

    EndlessRecyclerOnScrollListener(LinearLayoutManager linearLayoutManager) {
        this.mLinearLayoutManager = linearLayoutManager;
    }

    void setVisibleThreshold(int threshold) {
        this.visibleThreshold = threshold;
    }

    void setCurrent_page(int current_page) {
        this.current_page = Math.max(current_page, 0);
    }

    void setTotal_Pages(int total_pages) {
        this.total_pages = Math.max(total_pages, 0);
    }

    public void reset(int previousTotal, boolean loading) {
        this.previousTotal = previousTotal;
        this.loading = loading;
    }

    @Override
    public void onScrolled(@NonNull RecyclerView recyclerView, int dx, int dy) {
        super.onScrolled(recyclerView, dx, dy);

        visibleItemCount = recyclerView.getChildCount();
        totalItemCount = mLinearLayoutManager.getItemCount();
        firstVisibleItem = mLinearLayoutManager.findFirstVisibleItemPosition();

        if (loading) {
            if (totalItemCount > previousTotal) {
                loading = false;
                previousTotal = totalItemCount;
            }
        }

        if (!loading && (totalItemCount - visibleItemCount)
                <= (firstVisibleItem + visibleThreshold)) {
            // End has been reached

            // Do something
            current_page++;

            onLoadMore(current_page);

            loading = true;
        }

    }

    public abstract void onLoadMore(int current_page);
}

```

> activity_algolia_test.xml

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".AlgoliaTest">
    
    <com.google.android.material.appbar.AppBarLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:id="@+id/appBarLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:elevation="@dimen/card_elevation_no">

        <androidx.appcompat.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:minHeight="?attr/actionBarSize"
            android:theme="@style/AppToolbar" />

        <ProgressBar
            android:id="@+id/loading_progressbar"
            style="?android:attr/progressBarStyleHorizontal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="-7dp"
            android:backgroundTint="@color/colorPrimary"
            android:indeterminate="true"
            android:indeterminateTint="@color/colorAccent"
            android:max="100"
            android:visibility="gone" />

    </com.google.android.material.appbar.AppBarLayout>

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/my_recycler_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:scrollbars="vertical" />

</LinearLayout>

```

> todo_single_card.xml

```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="8dp">

    <TextView
        android:id="@+id/todo_title"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textColor="@color/colorAccent"
        android:textSize="20sp"
        android:textStyle="bold" />

    <TextView
        android:id="@+id/todo_id"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="14sp"
        android:textStyle="bold" />

    <TextView
        android:id="@+id/todo_completed"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="14sp"
        android:textStyle="bold" />

</LinearLayout>

```

## Firebase Multiple Incertion and Update

```java

    private class System32 {
        private String name;
        private String path;

        public System32() {
        }

        public System32(String name, String path) {
            this.name = name;
            this.path = path;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getPath() {
            return path;
        }

        public void setPath(String path) {
            this.path = path;
        }
    }

    public FirebaseDatabase db;

    db = FirebaseDatabase.getInstance();
    
    Map<String, Object> path_value = new HashMap<>();
    System32 system32 = new System32("virus", "c://users/timeMachine/.AS32");
    path_value.put("temp/system32", system32);
    path_value.put("temp/system64", system32);
    db.getReference().updateChildren(path_value);
    
```

## Debounce Functionality

```java

import android.os.Handler;
import android.view.View;

public class DebounceFunctionality implements View.OnClickListener {
    private IAfterDelay iAfterDelay;
    private long last_time_button_click = 0;
    private Handler handler;
    private long delay;

    public DebounceFunctionality(long delay, IAfterDelay iAfterDelay) {
        this.handler = new Handler();
        this.delay = delay;
        this.iAfterDelay = iAfterDelay;
    }

    @Override
    public void onClick(View view) {
        iAfterDelay.loading(true);
        handler.removeCallbacks(execute);
        last_time_button_click = System.currentTimeMillis();
        handler.postDelayed(execute, delay);
    }

    public interface IAfterDelay {
        void fire();
        void loading(boolean state);
    }

    private Runnable execute = () -> {
        if (System.currentTimeMillis() > (last_time_button_click + delay - 500)) {
            if (iAfterDelay != null) {
                iAfterDelay.loading(false);
                iAfterDelay.fire();
            }
        }
    };
}

```

## all country Name and Locale Code.

> Please keep in mind that countries can change over time (add/remove, they change their name, etc.); so from my point of view it is not a good idea to hard code a country list

```java

import java.util.Map;
 import java.util.TreeMap;


 public class CountryCodes {
     final Map<String, String> map = new TreeMap<String, String>   (String.CASE_INSENSITIVE_ORDER);
    public CountryCodes() {

     map.put("Andorra, Principality Of", "AD");
     map.put("United Arab Emirates", "AE");
     map.put("Afghanistan, Islamic State Of", "AF");
     map.put("Antigua And Barbuda", "AG");
     map.put("Anguilla", "AI");
     map.put("Albania", "AL");
     map.put("Armenia", "AM");
     map.put("Netherlands Antilles", "AN");
     map.put("Angola", "AO");
     map.put("Antarctica", "AQ");
     map.put("Argentina", "AR");
     map.put("American Samoa", "AS");
     map.put("Austria", "AT");
     map.put("Australia", "AU");
     map.put("Aruba", "AW");
     map.put("Azerbaidjan", "AZ");
     map.put("Bosnia-Herzegovina", "BA");
     map.put("Barbados", "BB");
     map.put("Bangladesh", "BD");
     map.put("Belgium", "BE");
     map.put("Burkina Faso", "BF");
     map.put("Bulgaria", "BG");
     map.put("Bahrain", "BH");
     map.put("Burundi", "BI");
     map.put("Benin", "BJ");
     map.put("Bermuda", "BM");
     map.put("Brunei Darussalam", "BN");
     map.put("Bolivia", "BO");
     map.put("Brazil", "BR");
     map.put("Bahamas", "BS");
     map.put("Bhutan", "BT");
     map.put("Bouvet Island", "BV");
     map.put("Botswana", "BW");
     map.put("Belarus", "BY");
     map.put("Belize", "BZ");
     map.put("Canada", "CA");
     map.put("Cocos (Keeling) Islands", "CC");
     map.put("Central African Republic", "CF");
     map.put("Congo, The Democratic Republic Of The", "CD");
     map.put("Congo", "CG");
     map.put("Switzerland", "CH");
     map.put("Ivory Coast (Cote D'Ivoire)", "CI");
     map.put("Cook Islands", "CK");
     map.put("Chile", "CL");
     map.put("Cameroon", "CM");
     map.put("China", "CN");
     map.put("Colombia", "CO");
     map.put("Costa Rica", "CR");
     map.put("Former Czechoslovakia", "CS");
     map.put("Cuba", "CU");
     map.put("Cape Verde", "CV");
     map.put("Christmas Island", "CX");
     map.put("Cyprus", "CY");
     map.put("Czech Republic", "CZ");
     map.put("Germany", "DE");
     map.put("Djibouti", "DJ");
     map.put("Denmark", "DK");
     map.put("Dominica", "DM");
     map.put("Dominican Republic", "DO");
     map.put("Algeria", "DZ");
     map.put("Ecuador", "EC");
     map.put("Estonia", "EE");
     map.put("Egypt", "EG");
     map.put("Western Sahara", "EH");
     map.put("Eritrea", "ER");
     map.put("Spain", "ES");
     map.put("Ethiopia", "ET");
     map.put("Finland", "FI");
     map.put("Fiji", "FJ");
     map.put("Falkland Islands", "FK");
     map.put("Micronesia", "FM");
     map.put("Faroe Islands", "FO");
     map.put("France", "FR");
     map.put("France (European Territory)", "FX");
     map.put("Gabon", "GA");
     map.put("Great Britain", "UK");
     map.put("Grenada", "GD");
     map.put("Georgia", "GE");
     map.put("French Guyana", "GF");
     map.put("Ghana", "GH");
     map.put("Gibraltar", "GI");
     map.put("Greenland", "GL");
     map.put("Gambia", "GM");
     map.put("Guinea", "GN");
     map.put("Guadeloupe (French)", "GP");
     map.put("Equatorial Guinea", "GQ");
     map.put("Greece", "GR");
     map.put("S. Georgia & S. Sandwich Isls.", "GS");
     map.put("Guatemala", "GT");
     map.put("Guam (USA)", "GU");
     map.put("Guinea Bissau", "GW");
     map.put("Guyana", "GY");
     map.put("Hong Kong", "HK");
     map.put("Heard And McDonald Islands", "HM");
     map.put("Honduras", "HN");
     map.put("Croatia", "HR");
     map.put("Haiti", "HT");
     map.put("Hungary", "HU");
     map.put("Indonesia", "ID");
     map.put("Ireland", "IE");
     map.put("Israel", "IL");
     map.put("India", "IN");
     map.put("British Indian Ocean Territory", "IO");
     map.put("Iraq", "IQ");
     map.put("Iran", "IR");
     map.put("Iceland", "IS");
     map.put("Italy", "IT");
     map.put("Jamaica", "JM");
     map.put("Jordan", "JO");
     map.put("Japan", "JP");
     map.put("Kenya", "KE");
     map.put("Kyrgyz Republic (Kyrgyzstan)", "KG");
     map.put("Cambodia, Kingdom Of", "KH");
     map.put("Kiribati", "KI");
     map.put("Comoros", "KM");
     map.put("Saint Kitts & Nevis Anguilla", "KN");
     map.put("North Korea", "KP");
     map.put("South Korea", "KR");
     map.put("Kuwait", "KW");
     map.put("Cayman Islands", "KY");
     map.put("Kazakhstan", "KZ");
     map.put("Laos", "LA");
     map.put("Lebanon", "LB");
     map.put("Saint Lucia", "LC");
     map.put("Liechtenstein", "LI");
     map.put("Sri Lanka", "LK");
     map.put("Liberia", "LR");
     map.put("Lesotho", "LS");
     map.put("Lithuania", "LT");
     map.put("Luxembourg", "LU");
     map.put("Latvia", "LV");
     map.put("Libya", "LY");
     map.put("Morocco", "MA");
     map.put("Monaco", "MC");
     map.put("Moldavia", "MD");
     map.put("Madagascar", "MG");
     map.put("Marshall Islands", "MH");
     map.put("Macedonia", "MK");
     map.put("Mali", "ML");
     map.put("Myanmar", "MM");
     map.put("Mongolia", "MN");
     map.put("Macau", "MO");
     map.put("Northern Mariana Islands", "MP");
     map.put("Martinique (French)", "MQ");
     map.put("Mauritania", "MR");
     map.put("Montserrat", "MS");
     map.put("Malta", "MT");
     map.put("Mauritius", "MU");
     map.put("Maldives", "MV");
     map.put("Malawi", "MW");
     map.put("Mexico", "MX");
     map.put("Malaysia", "MY");
     map.put("Mozambique", "MZ");
     map.put("Namibia", "NA");
     map.put("New Caledonia (French)", "NC");
     map.put("Niger", "NE");
     map.put("Norfolk Island", "NF");
     map.put("Nigeria", "NG");
     map.put("Nicaragua", "NI");
     map.put("Netherlands", "NL");
     map.put("Norway", "NO");
     map.put("Nepal", "NP");
     map.put("Nauru", "NR");
     map.put("Neutral Zone", "NT");
     map.put("Niue", "NU");
     map.put("New Zealand", "NZ");
     map.put("Oman", "OM");
     map.put("Panama", "PA");
     map.put("Peru", "PE");
     map.put("Polynesia (French)", "PF");
     map.put("Papua New Guinea", "PG");
     map.put("Philippines", "PH");
     map.put("Pakistan", "PK");
     map.put("Poland", "PL");
     map.put("Saint Pierre And Miquelon", "PM");
     map.put("Pitcairn Island", "PN");
     map.put("Puerto Rico", "PR");
     map.put("Portugal", "PT");
     map.put("Palau", "PW");
     map.put("Paraguay", "PY");
     map.put("Qatar", "QA");
     map.put("Reunion (French)", "RE");
     map.put("Romania", "RO");
     map.put("Russian Federation", "RU");
     map.put("Rwanda", "RW");
     map.put("Saudi Arabia", "SA");
     map.put("Solomon Islands", "SB");
     map.put("Seychelles", "SC");
     map.put("Sudan", "SD");
     map.put("Sweden", "SE");
     map.put("Singapore", "SG");
     map.put("Saint Helena", "SH");
     map.put("Slovenia", "SI");
     map.put("Svalbard And Jan Mayen Islands", "SJ");
     map.put("Slovak Republic", "SK");
     map.put("Sierra Leone", "SL");
     map.put("San Marino", "SM");
     map.put("Senegal", "SN");
     map.put("Somalia", "SO");
     map.put("Suriname", "SR");
     map.put("Saint Tome (Sao Tome) And Principe", "ST");
     map.put("Former USSR", "SU");
     map.put("El Salvador", "SV");
     map.put("Syria", "SY");
     map.put("Swaziland", "SZ");
     map.put("Turks And Caicos Islands", "TC");
     map.put("Chad", "TD");
     map.put("French Southern Territories", "TF");
     map.put("Togo", "TG");
     map.put("Thailand", "TH");
     map.put("Tadjikistan", "TJ");
     map.put("Tokelau", "TK");
     map.put("Turkmenistan", "TM");
     map.put("Tunisia", "TN");
     map.put("Tonga", "TO");
     map.put("East Timor", "TP");
     map.put("Turkey", "TR");
     map.put("Trinidad And Tobago", "TT");
     map.put("Tuvalu", "TV");
     map.put("Taiwan", "TW");
     map.put("Tanzania", "TZ");
     map.put("Ukraine", "UA");
     map.put("Uganda", "UG");
     map.put("United Kingdom", "UK");
     map.put("USA Minor Outlying Islands", "UM");
     map.put("United States", "US");
     map.put("Uruguay", "UY");
     map.put("Uzbekistan", "UZ");
     map.put("Holy See (Vatican City State)", "VA");
     map.put("Saint Vincent & Grenadines", "VC");
     map.put("Venezuela", "VE");
     map.put("Virgin Islands (British)", "VG");
     map.put("Virgin Islands (USA)", "VI");
     map.put("Vietnam", "VN");
     map.put("Vanuatu", "VU");
     map.put("Wallis And Futuna Islands", "WF");
     map.put("Samoa", "WS");
     map.put("Yemen", "YE");
     map.put("Mayotte", "YT");
     map.put("Yugoslavia", "YU");
     map.put("South Africa", "ZA");
     map.put("Zambia", "ZM");
     map.put("Zaire", "ZR");
     map.put("Zimbabwe", "ZW");

    }

     public String getCode(String country){
     String countryFound = map.get(country);
     if(countryFound==null){
             countryFound="UK";
     }
     return countryFound;
     }
}

```

## Setup menu Item On Toolbar

```java

@Override
public boolean onCreateOptionsMenu(Menu menu) {
    // Inflate the menu; this adds items to the action bar if it is present.
    getMenuInflater().inflate(R.menu.main_menu, menu);
    return true;
}

```
> Listener on menu items when clicked

```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    // Handle item selection
    switch (item.getItemId()) {
        case R.id.action_add:
            addSomething();
            return true;
        case R.id.action_settings:
            startSettings();
            return true;
        default:
            return super.onOptionsItemSelected(item);
    }
}
```

## Repeat Code Execution For X Times and Till y Seconds

```java

Timer timer = new Timer();
int begin = 0;
int timeInterval = 1000;
timer.schedule(new TimerTask() {
    int counter = 0;
    public void run() {
        counter++;
        System.out.println("fuck");
        if (counter >= 20) {
            timer.cancel();
        }
    }
}, begin, timeInterval);

```

## Location (Coordinates) [From This Library](https://github.com/delight-im/Android-SimpleLocation)

> MyLocation.java

```java

package io.raisehand.raisehandrepositoryenv.network;

import android.content.Context;
import android.os.Handler;

import im.delight.android.location.SimpleLocation;
import io.raisehand.raisehandrepositoryenv.model.Coordinates;

@SuppressWarnings("unused")
public class MyLocation {
    private Context context;
    private boolean locationReady, updatePaused;
    private SimpleLocation simpleLocation;
    private Coordinates coordinates;
    private boolean requireFineGranularity;
    private boolean passiveMode;
    private long updateIntervalInMilliseconds; // this should be less than 'autoUpdateStopAfterMilliseconds' variable...
    private long autoUpdateStopAfterMilliseconds = 5000; // 5 Seconds by Default
    private int timesRefresh = 0;

    public MyLocation(Context context, boolean requireFineGranularity, boolean passiveMode, long updateIntervalInMilliseconds, boolean requireNewLocation) {
        this.context = context;
        this.requireFineGranularity = requireFineGranularity;
        this.passiveMode = passiveMode;
        this.updateIntervalInMilliseconds = updateIntervalInMilliseconds;
        this.simpleLocation = new SimpleLocation(context, requireFineGranularity, passiveMode, updateIntervalInMilliseconds, requireNewLocation);
        this.coordinates = new Coordinates(0, 0);
        this.locationReady = false; // not mandatory but still setting reset value flag.
    }

    public void startLocationUpdate(boolean wantToStopUpdateAutomatically) {
        if (!canDeviceAccessLocation()) {
            SimpleLocation.openSettings(context);
        } else {
            resumeLocationUpdate();
            simpleLocation.setListener(() -> {
                setCoordinates(new Coordinates(simpleLocation.getLatitude(), simpleLocation.getLongitude()));
                locationReady = true;
                timesRefresh++;
            });
            if (wantToStopUpdateAutomatically)
                new Handler().postDelayed(this::pauseLocationUpdate, autoUpdateStopAfterMilliseconds);
        }
    }

    // make the device update its location
    private void resumeLocationUpdate() {
        if (simpleLocation != null) {
            updatePaused = false;
            simpleLocation.beginUpdates();
        }
    }

    // stop location updates (saves battery)
    private void pauseLocationUpdate() {
        if (simpleLocation != null) {
            updatePaused = true;
            simpleLocation.endUpdates();
        }
    }

    // call this method after constructor call or before getCurrentLocationCoordinates() call
    public void setAutoUpdateStopAfterMilliseconds(long autoUpdateStopAfterMilliseconds) {
        this.autoUpdateStopAfterMilliseconds = autoUpdateStopAfterMilliseconds;
    }

    private boolean canDeviceAccessLocation() {
        return simpleLocation.hasLocationEnabled();
    }

    public boolean isRequireFineGranularity() {
        return requireFineGranularity;
    }

    public boolean isPassiveMode() {
        return passiveMode;
    }

    public long getUpdateIntervalInMilliseconds() {
        return updateIntervalInMilliseconds;
    }

    public Coordinates getCoordinates() {
        return coordinates;
    }

    private void setCoordinates(Coordinates coordinates) {
        this.coordinates = coordinates;
    }

    public boolean isLocationReady() {
        return locationReady;
    }

    public boolean isUpdatePaused() {
        return updatePaused;
    }

    public boolean isEnoughRefineLocation() {
        int refreshLeastTime = 2;
        return timesRefresh > refreshLeastTime;
    }

}

```
> MainActivity.java

```java

public class MainActivity extends AppCompatActivity {

    MyLocation myLocation;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        long interval = 1000 * 5;
        myLocation = new MyLocation(getApplicationContext(), true, false, interval, true);
        myLocation.setAutoUpdateStopAfterMilliseconds(interval * 10); // 25 Seconds after getting as precise coordinates as possible...
        myLocation.startLocationUpdate(true);
        
        anyBtn.setOnClickListener(e -> {
            if (myLocation.isLocationReady() && (myLocation.isEnoughRefineLocation() || myLocation.isUpdatePaused())) {
                Log.d("XXX", "lat:" + myLocation.getCoordinates().getLat() + ", " + "lng:" + myLocation.getCoordinates().getLng());
            } else {
                showToast("Fetching Your Location");
            }
        });
        
    }
    
}

```

## Internet Checker [Library](https://github.com/novoda/merlin)

> InternetConnectionChecker.java

```java

package io.example.app.network;

import android.content.Context;
import android.widget.Toast;

import com.novoda.merlin.Connectable;
import com.novoda.merlin.Disconnectable;
import com.novoda.merlin.Endpoint;
import com.novoda.merlin.Merlin;
import com.novoda.merlin.ResponseCodeValidator;

@SuppressWarnings("unused")
public class InternetConnectionChecker {
    private Context context;
    private Merlin merlin;
    private String endPoint = "https://www.google.com";
    private boolean isConnected;

    public InternetConnectionChecker(Context context) {
        this.context = context;
        this.merlin = new Merlin.Builder().withConnectableCallbacks().withDisconnectableCallbacks().build(context);
        this.isConnected = false;
    }

    public void startCheckingInternetConnection() {
        if (merlin != null) {
            merlin.bind();
            runInternetStateChecker();
        }
    }

    public void stopCheckingInternetConnection() {
        if (merlin != null) merlin.unbind();
    }

    private void runInternetStateChecker() {
        if (merlin != null) {
            merlin.registerConnectable(connected);
            merlin.registerDisconnectable(disconnected);
        }
    }

    private Connectable connected = () -> {
        // we are connected
        isConnected = true;
        Toast.makeText(context, "You are Connected", Toast.LENGTH_LONG).show();
    };

    private Disconnectable disconnected = () -> {
        // we are disconnected
        isConnected = false;
        Toast.makeText(context, "Ah! you are Disconnected", Toast.LENGTH_LONG).show();
    };

    public boolean isEndPointValid() {
        ResponseCodeValidator validator = responseCode -> responseCode == 200;
        merlin.setEndpoint(Endpoint.from(endPoint), validator);
        return validator.isResponseCodeValid(200);
    }

    public String getEndPoint() {
        return endPoint;
    }

    public void setEndPoint(String endPoint) {
        this.endPoint = endPoint;
    }

    public boolean isConnected() {
        return isConnected;
    }
}

```
> MainActivity.java

```java

public class MainActivity extends AppCompatActivity {

    InternetConnectionChecker internetConnectionChecker;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        internetConnectionChecker = new InternetConnectionChecker(getApplicationContext());

        // we can check
        internetConnectionChecker.isConnected();

    }
    
    
    @Override
    protected void onPause() {
        if (internetConnectionChecker != null)
            internetConnectionChecker.stopCheckingInternetConnection();
        super.onPause();
    }
    
    @Override
    protected void onResume() {
        if (internetConnectionChecker != null)
            internetConnectionChecker.startCheckingInternetConnection(); // will bind the merlin, because of anroid lifecycle
        super.onResume();
    }
   
}
```
## Retrofit Internet Boilerplate

```gradle

    implementation 'com.google.code.gson:gson:2.8.6'

    /* Used for server calls */
    implementation 'com.squareup.okio:okio:2.4.3'
    implementation 'com.squareup.retrofit2:retrofit:2.7.1'
    implementation 'com.facebook.stetho:stetho:1.5.1'
    implementation 'com.facebook.stetho:stetho-okhttp3:1.5.1'

    // https://stackoverflow.com/a/35238185
    implementation 'com.squareup.retrofit2:adapter-rxjava2:2.7.1'
    implementation 'com.squareup.retrofit2:converter-gson:2.7.1'

    // Used to debug your Retrofit connections
    // Do not upgrade as it will require increasing minSdkVersion to 21
    //noinspection GradleDependency
    implementation 'com.squareup.okhttp3:logging-interceptor:3.12.3'

```


> RetrofitFactory.java

```java


import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

import io.raisehand.raisehandrepositoryenv.utils.helperUtils.Constants;
import retrofit2.Retrofit;
import retrofit2.adapter.rxjava2.RxJava2CallAdapterFactory;
import retrofit2.converter.gson.GsonConverterFactory;

public class RetrofitFactory {

    public static Retrofit instance = null;

    public static Retrofit getInstance() {
        if (instance == null) {

            Gson gson = new GsonBuilder().setLenient().create();

            String BASE_URL = Constants.BACKEND_API_BASE_URL; // http://example.herokuapp.com/
            instance = new Retrofit.Builder()
                    .baseUrl(BASE_URL)
                    .addConverterFactory(GsonConverterFactory.create(gson))
                    .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
                    .build();
        }

        return instance;
    }

}

```

> BackendApiRoutes.java

```java


import io.raisehand.raisehandrepositoryenv.utils.helperUtils.Constants;
import io.reactivex.Observable;
import okhttp3.ResponseBody;
import retrofit2.http.Field;
import retrofit2.http.FormUrlEncoded;
import retrofit2.http.GET;
import retrofit2.http.POST;
import retrofit2.http.Path;

public interface BackendApiRoutes {

    @GET(Constants.ROUTE_VERSION + "/wake_up_server")
    Observable<ResponseBody> wakeupServer();

    @POST(Constants.ROUTE_VERSION + "/contributors/pricing")
    @FormUrlEncoded
    Observable<ResponseBody> getPlans(@Field("price_request_permission_code") String price_request_permission_code,                                                         @Field("currency_code") String currency_code, @Field("country") String country);

    @POST(Constants.ROUTE_VERSION + "/{planName}")
    @FormUrlEncoded
    Observable<ResponseBody> makeChargePlan(@Path("planName") String planName, @Field("username") String username,                                                                 @Field("description") String description, @Field("customerId") String customerId,                                                     @Field("permissionCode") String permissionCode, @Field("currency_code") String                                                         currency_code);

}

```
> MainActivity.java

```java

    private final BackendApiRoutes mBackendApiRoutes = RetrofitFactory.getInstance().create(BackendApiRoutes.class);
    private final CompositeDisposable mCompositeDisposable = new CompositeDisposable();
    
    // inside onCreate
    mCompositeDisposable.add(mBackendApiRoutes
        .getPlans(
                LocalDB.getAppConstants().getNODEJS_SERVER_PRICE_REQUEST_PERMISSION(),
                HelperClass.getCurrencyCodeFromBaseCurrency(companyFirstChunk.getBaseCurrency()),
                LocalDB.getSavedUser().getCountry())
        .subscribeOn(Schedulers.io())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(responseBody -> {}, , throwable -> showToast(throwable.getMessage())));
        
```
