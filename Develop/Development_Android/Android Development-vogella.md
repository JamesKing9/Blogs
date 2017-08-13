# Glossary

entry ..... 实体



---

# developer.android.google

[android.google](https://developer.android.com/index.html) 

# Chapter 1:  Platform Architecture



# Chapter 2:  App Components



## 2.1  Intents and Intent Filters



## 2.2  Activities



### Try It Out:  Use `LauncherActivity` develop the list to launch the `Activity`



```java
public class ManiActivity extends LauncherActivity {
  	String[] names = {"Set app's arguments", "check the breed of soldier"};
  	Class<?>[] clazzs = {PreferenceActivityTest.class, ExpandableListActivityTest.class};
  	
  	@Override
  	public void onCreate(Bundle savedInstanceState) {
  		super.onCreate(savedInstanceState);
  		ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, names);
  		setListAdapter(adapter);
  	}
  	
  	@Override
  	public Intent intentForPosition(int position) {
  		return new Intent(MainActivity.this, clazzs[position]);
  	}
}
```



**How It Works**







## 2.3  Fragments



## 2.4  Loaders





# Chapter 3:  App Resources



# Chapter 4:  App Manifest



# Chapter 5:  User Interface



# Chapter 6:  Animation and Graphics



# Chapter 7:  Computation



# Chapter 8:  Media Apps



# Chapter 9:  Media and Camera



# Chapter 10:  Location and Sensors



# Chapter 11:  Connectivity



# Chapter 12:  Text and Input







 



# Android working with CardView and RecyclerView

> By <u>Ravi Tamada</u> - May 23, 2016 From: [this](https://www.androidhive.info/2016/05/android-working-with-card-view-and-recycler-view/). 

`CardView` is another major element introduced in `Material Design`. Using `CardView` you can represent the information in a card manner with a drop shadow(elevation) and corner radius which looks consistent across the platform. `CardView` extends the `FrameLayout` and it is supported way back to Android 2.x.

We can achieve good looking UI when `CardView` is combined with `RecyclerView`. In this article we are going to learn how to integrate `CardView` with `RecyclerView` by creating a beautiful music app that displays music albums with a cover image and title.



## How to Add CardView?

To use the `CardView` in your app, add the `CardView` dependency in **build.gradle** and Sync the project.

**build.gradle**

```groovy
dependencies {
	// CardView
  compile 'com.android.support:cardview-v7:23.3.+'
}
```

Add the **<android.support.v7.widget.CardView>** widget to your layout and place other UI widgets like **TextView**s, **ImageView**s inside it. You can notice that the below `CardView` widget contains a single **TextView**.

```xml
<LinearLayout 
	xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:card_view="http://schemas.android.com/apk/res-auto">
  
    <android.support.v7.widget.CardView
        xmlns:card_view="http://schemas.android.com/apk/res-auto" 
        android:id="@+id/card_view" 
        android:layout_gravity="center"
        android:layout_width="250dp"
        android:layout_height="250dp"
        cardview:cardCornerRadius="4dp" />
        
    	<TextView
        	android:text="Hello Card"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
     </android.support.v7.widget.CardView>
</LinearLayout>                               
```



Now let's see this in action by creating a new project.

## 1  Creating New Project

1.  Create a new project in Android Studio from **File ⇒ New Project**. When it prompts you to select the default activity, select **Empty Activity** and proceed.

    ​

2.  Download this [res.zip](http://api.androidhive.info/cardview/res.zip) and add them to your projects res folder. This res folder contains few **album covers** and **icons** required for this project.

    ​

3.  Add the below strings, colors and dimen resources to **strings.xml**, **colors.xml** and **dimens.xml** files.

**strings.xml**

```xml
<resources>
	<string name="app_name">Card View</string>
	<string name="action_settings">Settings</string>
	<string name="action_add_favourite">Add to Favourites</string>
	<string name="action_play_next">Play Next</string>
	<string name="backdrop_title">LOVE MUSIC</string>
	<string name="backdrop_subtitle">This season top 20 albums</string>
</resources>
```

**colors.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
	<color name="colorPrimary">#F50057</color>
	<color name="colorPrimaryDark">#F50057</color>
	<color name="colorAccent">#FF4081</color>
	<color name="viewBg">#f1f5f8</color>
	<color name="album_title">#4c4c4c</color>
</resources>
```

**dimens.xml**

```xml
<resources>
    <!-- Default screen margins, per the Android Design guidelines. -->
    <dimen name="activity_horizontal_margin">16dp</dimen>
    <dimen name="activity_vertical_margin">16dp</dimen>
    <dimen name="fab_margin">16dp</dimen>
    <dimen name="item_offset">10dp</dimen>
    <dimen name="detail_backdrop_height">250dp</dimen>
    <dimen name="backdrop_title">30dp</dimen>
    <dimen name="backdrop_subtitle">18dp</dimen>
    <dimen name="card_margin">5dp</dimen>
    <dimen name="card_album_radius">0dp</dimen>
    <dimen name="album_cover_height">160dp</dimen>
    <dimen name="album_title_padding">10dp</dimen>
    <dimen name="album_title">15dp</dimen>
    <dimen name="songs_count_padding_bottom">5dp</dimen>
    <dimen name="songs_count">12dp</dimen>
    <dimen name="ic_album_overflow_width">20dp</dimen>
    <dimen name="ic_album_overflow_height">30dp</dimen>
    <dimen name="ic_album_overflow_margin_top">10dp</dimen>
</resources>
```



4.  Open **build.gradle** and add `CardView`, `RecyclerView` and `Glide` dependencies. `RecyclerView` is used to display the albums in grid manner. `CardView` is used to display single album item. `Glide` is used to display the album cover images.

**build.gradle**

```groovy
dependencies {
	compile fileTree(dir: 'libs', include: ['*.jar'])
	testCompile 'junit:junit:4.12'
	compile 'com.android.support:appcompat-v7:23.3.0'
	compile 'com.android.support:design:23.3.0'
	
	// RecyclerView
	compile 'com.android.support:recyclerview-v7:23.3.+'
	
	// CardView
	compile 'com.android.support:cardview-v7:23.3.+'
	
	// Glide
	compile 'com.github.bumptech.glide:glide:3.7.0'
}
```



5.  To create instance of a single album, we need a model class denoting the album properties like name, number of songs and cover image. So create a class named **Album.java** and add the below code.

**Album.java**

```java
package info.androidhive.cardview;

public class Album {
	private String name;
	private int numOfSongs;
	private int thumbnail;
	
	public Album() {}
	
	public Album(String name, int numOfSongs, int thumbnail) {
		this.name = name;
		this.numOfSongs = numOfSongs;
		this.thumbnail = thumbnail;
	}
	
	public String getName() {
		return name;
	}
	
	public void setName(String name) {
		this.name = name;
	}
	
	public int getNumOfSongs() {
		return numOfSongs;
	}
	
	public void setNumOfSongs(int numOfSongs) {
		this.numOfSongs = numOfSongs;
	}
	
	public int getThumbnail() {
		return thumbnail;
	}
	
	public void setThumbnail(int thumbnail) {
		this.thumbnail = thumbnail;
	}
}
```



6.  We also need an xml layout to display the album card. Create an xml layout named **album_card.xml** under res/layout. Here you can notice that I have added **<android.support.v7.widget.CardView>** and added all the album properties like name, number of songs and cover image inside it. I also add a 3 dot icon which shows a popup menu on tapping it.

**album_card.xml**

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:card_view="http://schemas.android.com/apk/res-auto"
	android:layout_width="match_parent"
	android:layout_height="wrap_content">
	
	<android.support.v7.widget.CardView 
		android:id="@+id/card_view"
		android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_gravity="center"
        android:layout_margin="@dimen/card_margin"
        android:elevation="3dp"
        card_view:cardCornerRadius="@dimen/card_album_radius">
        
        <RelativeLayout
        	android:layout_width="match_parent"
        	android:layout_height="match_parent">
        	
        	<ImageView
        		android:id="@+id/thumbnail"
        		android:layout_width="match_parent"
        		android:layout_height="@dimen/album_cover_height"
        		android:background="?attr/selectableItemBackgroundBorderless"
        		android:clickable="true"
        		android:scaleType="fitXY" />
        	
        	<TextView
        		android:id="@+id/title"
        		android:layout_width="match_parent"
        		android:layout_height="wrap_content"
        		android:layout_below="@id/thumbnail"
        		android:paddingLeft="@dimen/album_title_padding"
        		android:paddingRight="@dimen/album_title_padding"
        		android:paddingTop="@dimen/album_title_padding"
        		android:textColor="@color/album_title"
        		android:textSize="@dimen/album_title" />
        		
        	<TextView
        		android:id="@+id/count"
        		android:layout_width="match_parent"
        		android:layout_height="match_parent"
        		android:layout_below="@id/title"
        		android:paddingBottom="@dimen/songs_count_padding_bottom"
        		android:paddingLeft="@dimen/album_title_padding"
        		android:paddingRight="@dimen/album_title_padding"
        		android:textSize="@dimen/songs_count" />
        	
        	<ImageView
        		android:id="@+id/overflow"
        		android:layout_width="@dimen/ic_album_overflow_width"
        		android:layout_height="@dimen/ic_album_overflow_height"
        		android:layout_alignParentRight="true"
        		android:layout_below="@id/thumbnail"
        		android:layout_marginTop="@dimen/ic_album_overflow_margin_top"
        		android:scaleType="centerCrop"
        		android:src="@drawable/ic_dots" />
        
        </RelativeLayout>
      
	</android.support.v7.widget.CardView>
      
</LinearLayout>
```



7.   Create a menu file named **menu_album.xml** under **res\menu** folder. This menu will be shown as popup menu on tapping on dots icons on each album card item.

**menu_album.xml**

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools">
	
	<item
		android:id="@+id/action_add_favourite"
		android:orderInCategory="100"
		android:title="@string/action_add_favourite" />
	
	<item
		android:id="@+id/action_play_next"
		android:orderInCategory="101"
		android:title="@string/action_play_next" />
	
</menu>
```



8.  To render the `RecyclerView`, we need an adapter class which inflates the **album_card.xml** by keeping appropriate information. Create a class named **AlbumsAdapter.java** and add the below content.

**AlbumsAdapter.java**

```java
package info.androidhive.cardview;

import android.content.Context;
import android.support.v7.widget.PopupMenu;
import android.support.v7.widget.RecyclerView;
import android.view.LayoutInflater;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import com.bumptech.glide.Glide;

import java.util.List;

public class AlbumsAdapter extends RecyclerView.Adapter<AlbumsAdapter.MyViewHolder> {
	private Context mContext;
	private List<Album> albumList;
	
	public class MyViewHolder extends RecyclerView.ViewHolder {
    	public TextView title, count;
      	public ImageView thumbnail, overflow;
      
      	public MyViewHolder(View view) {
        	super(view);
          	title = (TextView) view.findViewById(R.id.title);
          	count = (TextView) view.findViewById(R.id.count);
          	thumbnail = (ImageView) view.findViewById(R.id.thumbnail);
          	overflow = (ImageView) view.findViewById(R.id.overflow);
      	}
	}
	
	public AlbumsAdapter(Context mContext, List<Album> albumList) {
		this.mContext = mContext;
		this.albumList = albumList;
	}
	
	@Override
	public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
		View itemView = LayoutInflater.from(parent.getContext())
				.inflate(R.layout.album_card, parent, false);
				
		return new MyViewHolder(itemView);
	}
	
	@Override
	public void onBindViewHolder(final MyViewHolder holder, int position) {
		Album album =albumList.get(position);
		holder.title.setText(album.getName());
		holder.count.setText(album.getNumOfSongs() + "songs");
		
		// loading album cover using Glide library
		Glide.with(mContext).load(album.getThumbnail()).into(holder.thumbnail);
		
		holder.overflow.setOnClickListener(new View.OnClickListener() {
			@Override
			public void onClick(View view) {
				showPopupMenu(holder.overflow);
			}
		});
	}
	
	/**
	 * Showing popup menu when tapping on 3 dots
	 */
	private void showPopupMenu(View view) {
		// inflate menu
		PopupMenu popup = new PopupMenu(mContext, view);
		MenuInflater inflater = popup.getMenuInflater();
		inflater.inflate(R.menu.menu_album, popup.getMenu);
		popup.setOnMenuItemClickListener(new MyMenuItemClickListener());
		popup.show();
	}
	
	/**
	 * Click listener for popup menu items
	 */
	class MyMenuItemClickListener implements PopupMenu.OnMenuItemClickListener {
		public MyMenuItemClickListener() {}
		
		@Override
		public boolean onMenuItemClick(MenuItem menuItem) {
			switch(menuItem.getItemId()) {
				case R.id.action_add_favourite:
					Toast.makeText(mContext, "Add to favourite", Toast.LENGTH_SHORT).show();
					return true;
				case R.id.action_play_next:
					Toast.makeText(mContext, "Play next", Toast.LENGTH_SHORT).show();
					return true;
				default:
			}
			return false;
		}
	}
	
	@Override
	public int getItemCount() {
		return albumList.size();
	}
}
```



9.  Open the layout files main activity **activity_main.xml** and **content_main.xml** , add `AppBarLayout`, `CollapsingToolbarLayout`,  `Toolbar` and `RecyclerView`.

**activity_main.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout
	xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	android:id="@+id/main_content"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:background="@android:color/white"
	android:fitsSystemWindows="true" >
	
	<android.support.design.widget.AppBarLayout
		android:id="@+id/appbar"
		android:layout_width="match_parent"
		android:layout_height="@dimen/detail_backdrop_height"
		android:fitsSystemWindows="true"
		android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">
		
		<android.support.design.wiget.CollapsingToolbarLayout
			android:id="@+id/collapsing_toolbar"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			android:fitsSystemWindows="true"
			app:contentScrim="?attr/colorPrimary"
			app:expandedTitleMarginEnd="64dp"
			app:expandedTitleMarginStart="48dp"
			app:expandedTitleTextAppearance="@android:color/transparent"
			app:layout_scrollFlags="scroll|exitUntilCollapsed" >
			
			<RelativeLayout
				android:layout_width="wrap_content"
				android:layout_height="wrap_content">
				
				<ImageView 
					android:id="@+id/backdrop"
					android:layout_width="match_parent"
					android:layout_height="match_parent"
					android:fitsSystemWindows="true"
					android:scaleType="centerCrop"
					app:layout_collapseMode="parallax"/>
				
				<LinearLayout
					android:layout_width="wrap_content"
					android:layout_height="wrap_content"
					android:layout_centerInParent="true"
					android:gravity="center_horizontal"
					android:orientation="vertical">
					
					<TextView
						android:id="@+id/love_music"
						android:layout_width="wrap_content"
						android:layout_height="wrap_content"
						android:text="@string/backdrop_title"
						android:textColor="@android:color/white"
						android:textSize="@dimen/backdrop_title"/>
					
					<TextView
						android:layout_width="wrap_content"
						android:layout_height="wrap_content"
						android:text="@string/backdrop_subtitle"
						android:textColor="@android:color/white"
						android:textSize="@dimen/backdrop_subtitle"/>
						
				</LinearLayout>
			</RelativeLayout>
			
			<android.support.v7.widget.Toolbar
				android:id="@+id/toolbar"
				android:layout_width="match_parent"
				android:layout_height="?attr/actionBarSize"
				app:layout_collapseMode="pin"
				app:popupTheme="@style/ThemeOverlay.AppCompat.Light"/>
				
		</android.support.design.wiget.CollapsingToolbarLayout>		
      
	</android.support.design.widget.AppBarLayout>
    
    <include layout="@layout/content_main" />
    
</android.support.design.widget.CoordinatorLayout>
```



**content_main.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:background="@color/viewBg"
	app:layout_behavior="@string/appbar_scrolling_view_behavior"
	tools:context="info.androidhive.cardview.MainActivtiy"
	tools:showIn="@layout/activity_main">
	
	<android.support.v7.widget.RecyclerView 
		android:id="@+id/recycler_view"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:clipToPadding="false"
		android:scrollbar="vertical" />

</RelativeLayout>
```



10.  Finally open **MainActivity.java** and do the necessary changes.

-> `initCollapsingToolbar()` - Shows or hides the toolbar title when the toolbar is collapsed or expanded.

-> `prepareAlbums()` - Adds sample albums data required for the recycler view.

-> `GridLayoutManager` is used to display the RecyclerView in Grid manner instead of list.

-> `GridSpacingItemDecoration` is used to give equal margins around RecyclerView grid items.

-> `AlbumsAdapter` instance is created and assigned to RecyclerView which renders the CardView albums in grid fashion.

**MainActivity.java**

```java
package info.androidhive.cardview;

import android.os.Bundle;
import android.support.v7.widget.GridLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.support.v7.widget.Toolbar;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {
	private RecyclerView recyclerView;
	private AlbumsAdapter adapter;
	private List<Album> albumList;
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        
        initCollapsingToolbar();
        
        recyclerView = (RecyclerView) findViewById(R.id.recycler_view);
        
        albumList = new ArrayList<>();
        adapter = new AlbumsAdapter(this, albumList);
        
        RecyclerView.LayoutManager mLayoutManager = new GridLayoutManager(this, 2);
        recyclerView.setLayoutManager(mLayoutManager);
        recyclerView.addItemDecoration(new GridSpacingItemDecoration(2, dpToPx(10), true));
        recyclerView.setItemAnimator(new DefaultItemAnimator());
        recyclerView.setAdapter(adapter);
        
        prepareAlbums();
        
        try {
        	Glide.with(this).load(R.drawable.cover).into((ImageView) findViewById(R.id.backdrop));
        } catch (Exception e) {
        	e.printStackTrace();
        }
	}
	
	/**
	 * Initializing collapsing toolbar will show and hide the toolbar title on scroll
	 */
	private void initCollapsingToolbar() {
		final CollapsingToolbarLayout collapsingToolbar = (CollapsingToolbarLayout) findViewById(R.id.collapsing_toolbar);
		collapsingToolbar.setTitle(" ");
		AppBarLayout appBarLayout = (AppBarLayout) findViewById(R.id.appbar);
		appBarLayout.setExpanded(true);
		
		// hiding & showing the title when toolbar expanded & collapsed
		appBarLayout.addOnOffsetChangedListener(new AppBarLayout.OnOffsetChangedListener() {
			boolean isShow = false;
			int scrollRange = -1;
			
			@Override
			public void onOffsetChanged(AppBarLayout appBarLayout, int verticalOffset) {
				if (scrollRange == -1) {
					scrollRange = appBarLayout.getTotalScrollRange();
				}
				if (scrollRange + verticalOffset == 0) {
					collapsingToolbar.setTitle(getString(R.string.app_name));
					isShow = true;
				} else if (isShow) {
					collapsingToolbar.setTitle(" ");
					isShow = false;
				}
			}
		});
	}
	
	/**
	 * Adding few albums for testing
	 */
	private void prepareAlbums() {
		int[] covers = new int[]{
				R.drawable.album1,
				R.drawable.album2,
				R.drawable.album3,
				R.drawable.album4,
				R.drawable.album5,
				R.drawable.album6,
				R.drawable.album7,
				R.drawable.album8,
				R.drawable.album9,
				R.drawable.album10,
				R.drawable.album11};
				
		Album a = new Album("True Romance", 13, covers[0]);
		albumList.add(a);
		
		a = new Album("Xscpae", 8, covers[1]);
		albumList.add(a);
		
		a = new Album("Maroon 5", 11, covers[2]);
        albumList.add(a);
 
        a = new Album("Born to Die", 12, covers[3]);
        albumList.add(a);
 
        a = new Album("Honeymoon", 14, covers[4]);
        albumList.add(a);
 
        a = new Album("I Need a Doctor", 1, covers[5]);
        albumList.add(a);
 
        a = new Album("Loud", 11, covers[6]);
        albumList.add(a);
 
        a = new Album("Legend", 14, covers[7]);
        albumList.add(a);
 
        a = new Album("Hello", 11, covers[8]);
        albumList.add(a);
 
        a = new Album("Greatest Hits", 17, covers[9]);
        albumList.add(a);
        
        adapter.notifyDataSetChanged();
	}
	
	/**
	 * RecyclerView item decoration - give equal margin around grid item
	 */
	public class GridSpacingItemDecoration extends RecyclerView.ItemDecoration {
		private int spanCount;
		private int spacing;
		private boolean includeEdge;
		
		public GridSpacingItemDecoration(int spanCount, int spacing, boolean includeEdge) {
			this.spanCount = spanCount;
			this.spacing = spacing;
			this.includeEdge = includeEdge;
		}
		
		@Override
		public void getItemOffsets(Rect outRect, View view, RecyclerView parent, RecyclerView.State state) {
			int position = parent.getChildAdapterPosion(view);  // item position
			int column = position % spanCount;  // item column
			
			if (includeEdge) {
				outRect.left = spacing - column * spacing / spanCount; // spacing - column * ((1f / spanCount) * spacing)
				outRect.right = (column + 1) * spacing / spanCount; // (column + 1) * ((1f / spanCount) * spacing)
				
				if (position < spanCount) {  // top edge
					outRect.top = spacing;
				}
				outRect.bottom = spacing;  // item bottom
			} else {
				outRect.left = column * spacing / spanCount;  // column * ((1f / spanCount) * spacing)
				outRect.right = spacing - (column + 1) * spacing /spanCount; // spacing - (column + 1) * ((1f / spanCount) * spacing)
				if (position >= spanCount) {
					outRect.top = spacing; // item top
				}
			}
		}
	}
	
	/**
	 * Converting dp to pixel
	 */
	private int dpToPx(int dp) {
		Resources r = getResources();
		// Math.round() -> "四舍五入"运算
		return Math.round(TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_DIP, dp, r.getDisplayMetrics()));
	} 
}
```



If you run the app now, you can see the album CardViews displayed in a grid.

<img src="https://www.androidhive.info/wp-content/uploads/2016/05/android-integrating-cardview-and-recyclerview-music-app.png" style="height:520px"> 

---



## Debug

error:

```mark
Caused by: java.lang.IllegalStateException: This Activity already has an action bar supplied by the window decor. Do not request Window.FEATURE_SUPPORT_ACTION_BAR and set windowActionBar to false in your theme to use a Toolbar instead.
```



resolve:

当在activity中调用了**setSupportActionBar(toolbar);** 

同时，AndroidManifest.xml 对应的Activity标签的android:theme为

同时，AndroidManifest.xml 对应的Activity标签的android:theme为

```
android:theme="@style/AppTheme" >
```

且，style资源文件中的parent为

```
parent="Theme.AppCompat.Light.DarkActionBar
```

就会报这个异常。

**问题分析：**

Using `Theme.AppCompat.Light` tells Android that you want the framework to provide an ActionBar for you. However, you are creating your own ActionBar (a `Toolbar`), so you are giving the framework mixed signals as to where you want the ActionBar to come from.

**解决方法：**

**在style.xml中加入：**

**![img](http://images2015.cnblogs.com/blog/1027377/201702/1027377-20170216110105566-1695088420.png)**

在Manifest.xml中，修改theme

![img](http://images2015.cnblogs.com/blog/1027377/201702/1027377-20170216110209722-1185297743.png)



---





# Android working with SVG / vector drawables

While developing Android Applications, supporting multiple resolutions are sometime nightmare to developers. Including multiple images for different resolutions also increases the project size. The solution is to use Vector Graphics such as SVG images. While Android does not support SVGs (**Scalable Vector Graphics**) directly, with the launch of Lollipop a new class was introduced called [VectorDrawable](https://developer.android.com/reference/android/graphics/drawable/VectorDrawable.html), which allows designers and developers to draw assets in a similar fashion using only code.

Simply explained, vector graphics are a way of describing graphical elements using geometric shapes. They are particularly well suited to graphical elements created in packages such as **Adobe Illustrator** or **Inkscape** where simple geometric shapes may be combined in to much more complex elements.



## 1. What is VectorDrawable?

As the name implies, vector drawables are based on vector graphics, as opposed to raster graphics, vector graphics are a way of describing graphical elements using geometric shapes. It is similar to a SVG file. In Android Vector Drawable are created as XML files. Now there is no need to create different size image for **mdpi**, **hdpi**, **xhdpi**, **xxhdpi**, **xxxhdpi** etc. We need only one vector file for multiple screen size devices. Also for older versions of Android that don’t support vector drawables, Vector Asset Studio can turn your vector drawables into different bitmap sizes for each screen density at runtime.

Here is the detailed [information](https://developer.android.com/studio/write/vector-asset-studio.html#about) Vector Asset Studio.

*Note:* For this project I’m using gradle version 2.2, my suggession is to use **2.0+**. However if you’re using gradle version below 2.0 then you’ll need to add some more code to the app level **build.gradle** file which I’ve mentioned below.

## 2. Creating Android Project

**1**. Create a new project in Android Studio from **File ⇒ New Project** and fill the project details.

**2**. Open **build.gradle** in app module, add the below line inside **defaultConfig** block.

```
vectorDrawables.useSupportLibrary = true
```

So the complete **build.gradle** looks like

```groovy
apply plugin: 'com.android.application'
 
android {
   compileSdkVersion 25
   buildToolsVersion "25.0.2"
   defaultConfig {
       applicationId "info.androidhive.vectordrawable"
       minSdkVersion 17
       targetSdkVersion 25
       versionCode 1
       versionName "1.0"
       testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
       vectorDrawables.useSupportLibrary = true
   }
   buildTypes {
       release {
           minifyEnabled false
           proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
       }
   }
}
 
dependencies {
   compile fileTree(dir: 'libs', include: ['*.jar'])
   androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
       exclude group: 'com.android.support', module: 'support-annotations'
   })
   compile 'com.android.support:appcompat-v7:25.1.0'
   testCompile 'junit:junit:4.12'
}
```



If you are using gradle version below 2.0 then use following

```groovy
apply plugin: 'com.android.application'
 
android {
    compileSdkVersion 24
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "info.androidhive.vectordrawable"
        minSdkVersion 17
        targetSdkVersion 24
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
        vectorDrawables.useSupportLibrary = true
        generatedDensities=[]
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    aaptOptions {
        additionalParameters "--no-version-vectors"
    }
}
 
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:24.2.1'
    testCompile 'junit:junit:4.12'
}
```



## 2.1 Creating VectorDrawable from Material Icons.

So let us start by creating VectorDrawables from Material Icons ([Material Icons](https://material.io/icons/) are the official icon set from Google that are designed under the [material design guidelines](https://material.io/guidelines/), these icons are open source and are beautifully crafted, delightful, and easy to use in your web, Android, and iOS projects).

**3**. In the project **Right click** on the **drawable** directory

**4**. Go to **New ⇒ Vector Asset**

![android-studio-new-vector-asset](https://www.androidhive.info/wp-content/uploads/2017/02/android-studio-new-vector-asset.png)

**5**. Click on the launcher icon to browse Material Icons

![android-studio-vector-asset-dialog](https://www.androidhive.info/wp-content/uploads/2017/02/android-studio-vector-asset-dialog.png)

**6**. Select an icon and click on ok

![choosing-vector-icon](https://www.androidhive.info/wp-content/uploads/2017/02/choosing-vector-icon.png)

**7**. Review the name of the file then click on next. 

![vector-asset-preview](https://www.androidhive.info/wp-content/uploads/2017/02/vector-asset-preview.png)

**8**. Now Vector Asset Studio will show the location about where the file is being saved, review it and click on finish.

**9**. The drawable folder will now consist of a newly created file (In my case ic_flight_takeoff)

below is the file code –

**ic_flight_takeoff.xml**

```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
        android:width="35dp"
        android:height="35dp"
        android:viewportWidth="24.0"
        android:viewportHeight="24.0">
    <path
        android:fillColor="#FFe29069"
        android:pathData="M2.5,19h19v2h-19zM22.07,9.64c-0.21,-0.8 -1.04,-1.28 -1.84,-1.06L14.92,10l-6.9,-6.43 -1.93,0.51 4.14,7.17 -4.97,1.33 -1.97,-1.54 -1.45,0.39 1.82,3.16 0.77,1.33 1.6,-0.43 5.31,-1.42 4.35,-1.16L21,11.49c0.81,-0.23 1.28,-1.05 1.07,-1.85z"/>
</vector>
```



You can modify the width and height of the vector as per your requirement (by default it stays as 24dp), a vector may consist of one or more paths. A path may have many attributes among which fillColor and pathData are the most important. fillColor attribute defines the color of the path, it must be a color attribute (hash code in *#aarrggbb*, or may also point to a color resource). pathData defines the path shape. In this case I’ve modified the vector **width**, **height** and path **fillColor**.

## 2.2 Creating VectorDrawable from SVG or PSD

Now we have created vectorDrawable from Material Icon, what if we want a separate icon? We can create it from SVG or PSD, below are the procedure, but it also has some restrictions you can check out here – <https://developer.android.com/studio/write/vector-asset-studio.html#PSD> (though the restriction listed here for PSD, it applies to SVG also).

**10**. In the project **Right click** on the **drawable** directory

**11**. Go to **New ⇒ Vector Asset**

**12**. Click on the radio button saying “Local File (SVG, PSD)”

![android-studio-choosing-vector-asset](https://www.androidhive.info/wp-content/uploads/2017/02/android-studio-choosing-vector-asset.png)

**13**. Click on the browse icon and navigate to your **SVG** or **PSD** file to select it

![android-studio-choosing-svg](https://www.androidhive.info/wp-content/uploads/2017/02/android-studio-choosing-svg.png)

**14**. After selecting click ok

**15**. Verify the image in preview and click **Next ⇒ Finish**.

![android-studio-choosing-svg](https://www.androidhive.info/wp-content/uploads/2017/02/android-studio-vector-asset-preview.png)

below is the file code generated from svg

**ic_light_bulb.xml**

```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="100dp"
    android:height="100dp"
    android:viewportHeight="512.0"
    android:viewportWidth="512.0">
    <path
        android:fillColor="#273B7A"
        android:pathData="M256,256m-256,0a256,256 0,1 1,512 0a256,256 0,1 1,-512 0" />
    <path
        android:fillColor="#121149"
        android:pathData="M506.4,309.5L300.1,103.3l-62.2,113.4l2.3,44.8l82.5,82.5l-3.4,3.4l-35.8,-35.8l-45.6,2.9h-64.7l-66.7,105.5l83.6,83.6C211.2,509 233.2,512 256,512C379,512 481.8,425.2 506.4,309.5z" />
    <path
        android:fillColor="#FFEDB5"
        android:pathData="M401.6,290.3c-3.3,-4.6 -9.3,-6.4 -14.6,-4.4c-0.1,0 -0.2,0.1 -0.2,0.1l-89.6,29.8c0,0.7 0,1.4 -0,2.2c-0.7,11.4 -9.6,20.6 -21,21.8l-54,5.6c-3.4,0.4 -6.5,-2.1 -6.8,-5.5c-0.4,-3.4 2.1,-6.6 5.5,-6.8l54,-5.6c5.3,-0.6 9.5,-4.9 9.8,-10.2c0.2,-2.9 -0.8,-5.8 -2.7,-8c-1.9,-2.2 -4.6,-3.5 -7.6,-3.7l-71.7,-4.7c-8.1,-0.5 -16,1.3 -23.1,5.1L85,358l25.6,51.6l23.8,-20.7c10.1,-8.8 23.5,-12.6 36.7,-10.4l79.4,13.2c14.6,1.9 29.1,-1.7 41.1,-10.2l108.1,-74.5C404.5,302.8 405.4,295.5 401.6,290.3z" />
    <path
        android:fillColor="#FEE187"
        android:pathData="M274.9,327.4c5.3,-0.6 9.5,-4.9 9.8,-10.2c0.2,-2.9 -0.8,-5.8 -2.7,-8c-1.9,-2.2 -4.6,-3.5 -7.6,-3.7l-15.9,-1v24.7L274.9,327.4z" />
    <path
        android:fillColor="#FEE187"
        android:pathData="M401.6,290.3c-3.3,-4.6 -9.3,-6.4 -14.6,-4.4c-0.1,0 -0.2,0.1 -0.2,0.1l-89.6,29.8c0,0.7 0,1.4 -0,2.2c-0.7,11.4 -9.6,20.6 -21,21.8l-17.7,1.8v50.6c11.8,-0.1 23.3,-3.8 33.1,-10.7l108.1,-74.5C404.5,302.8 405.4,295.5 401.6,290.3z" />
    <path
        android:fillColor="#FFC61B"
        android:pathData="M317.4,146c0,-34.7 -28.9,-62.8 -63.9,-61.4c-31.4,1.2 -57.1,26.5 -58.9,57.9c-1.2,21.6 8.7,40.9 24.6,52.7c10.1,7.6 16.3,19.2 16.3,31.9v21.3c0,11.3 9.2,20.5 20.5,20.5l0,0c11.3,0 20.5,-9.2 20.5,-20.5V227.4c0,-12.8 6.2,-24.6 16.5,-32.3C307.8,183.9 317.4,166 317.4,146z" />
    <path
        android:fillColor="#EAA22F"
        android:pathData="M255.4,84.6v184.2c0.2,0 0.4,0 0.6,0c11.3,0 20.5,-9.2 20.5,-20.5V227.4c0,-12.8 6.2,-24.6 16.5,-32.3c14.9,-11.2 24.5,-29 24.5,-49.1C317.4,111.9 289.6,84.3 255.4,84.6z" />
    <path
        android:fillColor="#A6A8AA"
        android:pathData="M235.5,227.9v20.5c0,11.3 9.2,20.5 20.5,20.5l0,0c11.3,0 20.5,-9.2 20.5,-20.5v-20.5L235.5,227.9z" />
    <path
        android:fillColor="#808183"
        android:pathData="M255.4,227.9v40.9c0.2,0 0.4,0 0.6,0c11.3,0 20.5,-9.2 20.5,-20.5v-20.5L255.4,227.9z" />
    <path
        android:fillColor="#FF5419"
        android:pathData="M244.2,183.8c-1.1,0 -2.3,-0.3 -3.3,-1.1c-2.5,-1.8 -3,-5.3 -1.2,-7.8l17.1,-23.4H244.2c-2.1,0 -4,-1.2 -5,-3.1c-1,-1.9 -0.8,-4.1 0.5,-5.8l23.6,-32.3c1.8,-2.5 5.3,-3 7.8,-1.2c2.5,1.8 3,5.3 1.2,7.8L255.2,140.4h12.6c2.1,0 4,1.2 5,3.1c1,1.9 0.8,4.1 -0.5,5.8l-23.6,32.3C247.6,183 245.9,183.8 244.2,183.8z" />
    <path
        android:fillColor="#C92F00"
        android:pathData="M272.3,117c1.8,-2.5 1.3,-6 -1.2,-7.8c-2.5,-1.8 -6,-1.3 -7.8,1.2l-7.9,10.8v18.9L272.3,117z" />
    <path
        android:fillColor="#C92F00"
        android:pathData="M267.8,140.4h-12.4v11.2h1.4l-1.4,1.9v18.9l16.9,-23.1c1.2,-1.7 1.4,-3.9 0.5,-5.8C271.8,141.6 269.9,140.4 267.8,140.4z" />
    <path
        android:fillColor="#D35933"
        android:pathData="M66.1,355.1l32.5,-22.2l40.5,64.7l-32.5,22.2z" />
    <path
        android:fillColor="#B54324"
        android:pathData="M139.1,397.6l-20.5,-32.8l-32.4,22.5l20.4,32.6z" />
</vector>
```



## 3. Using VectorDrawable

We have successfully added VectorDrawables to the project, now it’s time to use them. 

**16**. Open the layout file of main activity (**activity_main.xml**) and add the below xml. This layout contains shows how to use VectorDrawable with ImageView and other Views (as background) which is explained later in this tutorial.

**activity_main.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="info.androidhive.vectordrawable.MainActivity">
 
    <ImageView android:id="@+id/ic_logo"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="30dp"
        android:layout_marginTop="30dp"
        app:srcCompat="@drawable/ic_light_bulb" />
 
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="10dp"
        android:gravity="center_horizontal"
        android:text="Tap on icon to change tint color" />
 
    <android.support.v7.widget.AppCompatImageView
        android:id="@+id/ic_android"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="30dp" />
 
    <android.support.v7.widget.AppCompatTextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="20dp"
        android:drawableLeft="@drawable/ic_flight_takeoff"
        android:gravity="center_horizontal"
        android:text="TextView with Vector Drawable" />
 
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:text="Radio button with vector drawable icons" />
 
    <RadioGroup
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:showDividers="middle"
        android:orientation="horizontal"
        android:gravity="center">
 
        <android.support.v7.widget.AppCompatRadioButton
            android:id="@+id/radioBtn"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="10dp"
            android:background="@drawable/radio_selector"
            android:button="@android:color/transparent" />
 
        <android.support.v7.widget.AppCompatRadioButton
            android:id="@+id/radioBtn2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="10dp"
            android:background="@drawable/radio_selector"
            android:button="@android:color/transparent" />
 
        <android.support.v7.widget.AppCompatRadioButton
            android:id="@+id/radioBtn3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="10dp"
            android:background="@drawable/radio_selector"
            android:button="@android:color/transparent" />
 
        <android.support.v7.widget.AppCompatRadioButton
            android:id="@+id/radioBtn4"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="10dp"
            android:background="@drawable/radio_selector"
            android:button="@android:color/transparent" />
 
        <android.support.v7.widget.AppCompatRadioButton
            android:id="@+id/radioBtn5"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="10dp"
            android:background="@drawable/radio_selector"
            android:button="@android:color/transparent" />
 
    </RadioGroup>
 
 
</LinearLayout>
```



The above layout generates a screen something like this.

![android-working-with-vector-drawables](https://www.androidhive.info/wp-content/uploads/2017/02/android-working-with-vector-drawables.png)

## 3.1 Using VectorDrawable with ImageView from xml

So let us start with a simple ImageView, and even simpler by assigning the VectorDrawable to the ImageView through xml layout.

```xml
<ImageView
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   app:srcCompat="@drawable/ic_light_bulb"/>
```



As you can see, we used **app:srcCompat** instead of **android:src**, so that the support library can do the rest to display the image seamlessly on all versions of android. (The support library converts VectorDrawables to raster graphics automatically on android versions below 5.0 – API 21, details are [here](https://developer.android.com/guide/topics/graphics/vector-drawable-resources.html#vector-drawables-backward-solution)). So it was that easy.

## 3.2 Using VectorDrawable with ImageView from Java

Now Let us do the same thing with Java code, i.e. assigning `VectorDrawable` to *ImageView* through Java Code. 

**17**. Add another Vector Drawable (name it **ic_android.xml**) with the steps mention in section [2.1](https://www.androidhive.info/2017/02/android-working-svg-vector-drawables/#create_vector_drawable_from_material_icon) or [2.2](https://www.androidhive.info/2017/02/android-working-svg-vector-drawables/#create_vector_drawable_from_svg_psd), you can also create a file with that name and paste the below code.

**ic_android.xml**

```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="50dp"
    android:height="50dp"
    android:viewportHeight="24.0"
    android:viewportWidth="24.0">
    <path
        android:fillColor="@color/colorPrimaryDark"
        android:pathData="M6,18c0,0.55 0.45,1 1,1h1v3.5c0,0.83 0.67,1.5 1.5,1.5s1.5,-0.67 1.5,-1.5L11,19h2v3.5c0,0.83 0.67,1.5 1.5,1.5s1.5,-0.67 1.5,-1.5L16,19h1c0.55,0 1,-0.45 1,-1L18,8L6,8v10zM3.5,8C2.67,8 2,8.67 2,9.5v7c0,0.83 0.67,1.5 1.5,1.5S5,17.33 5,16.5v-7C5,8.67 4.33,8 3.5,8zM20.5,8c-0.83,0 -1.5,0.67 -1.5,1.5v7c0,0.83 0.67,1.5 1.5,1.5s1.5,-0.67 1.5,-1.5v-7c0,-0.83 -0.67,-1.5 -1.5,-1.5zM15.53,2.16l1.3,-1.3c0.2,-0.2 0.2,-0.51 0,-0.71 -0.2,-0.2 -0.51,-0.2 -0.71,0l-1.48,1.48C13.85,1.23 12.95,1 12,1c-0.96,0 -1.86,0.23 -2.66,0.63L7.85,0.15c-0.2,-0.2 -0.51,-0.2 -0.71,0 -0.2,0.2 -0.2,0.51 0,0.71l1.31,1.31C6.97,3.26 6,5.01 6,7h12c0,-1.99 -0.97,-3.75 -2.47,-4.84zM10,5L9,5L9,4h1v1zM15,5h-1L14,4h1v1z" />
</vector>
```



**18**. Open **MainActivity.java** and paste the below code.

```java
package info.androidhive.vectordrawable;
 
import android.graphics.Color;
import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.app.AppCompatDelegate;
import android.support.v7.widget.AppCompatImageView;
import android.view.View;
 
import java.util.Random;
 
public class MainActivity extends AppCompatActivity {
 
    static {
        AppCompatDelegate.setCompatVectorFromResourcesEnabled(true);
    }
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        final AppCompatImageView icAndroid = (AppCompatImageView) findViewById(R.id.ic_android);
        icAndroid.setImageResource(R.drawable.ic_android);
 
        icAndroid.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Random rnd = new Random();
                int color = Color.argb(255, rnd.nextInt(256), rnd.nextInt(256), rnd.nextInt(256));
                icAndroid.setColorFilter(color);
            }
        });
    }
}
```



Now, let me explain the code line by line.

**19**. For using *VectorDrawable* from java or to use it as background (in xml also) you need to intimate AppCompatDelegate to enable compat vector from resource. Below is the code for that.

```java
static {
        AppCompatDelegate.setCompatVectorFromResourcesEnabled(true);
    }
```



**20**. Whenever you are going to use *VectorDrawable* from java or to use it as background (in xml also) remember to use *AppCompatView* instead of normal view, here I have used *AppCompatImageView*, please also refer to the [layout](https://www.androidhive.info/2017/02/android-working-svg-vector-drawables/#using_vector_drawable) we created before.

**21**. Now assign the *VectorDrawable* as `src` or *background* as you do it normally, *AppCompat* will take care of the rest.

**22**. We have added some flavors to it, We implemented `OnClickListener` on the `ImageView` to set random color filter on it, upon click.

## 3.3 Using VectorDrawable as Drawable with TextView

You may want to use *VectorDrawable* as background or as compound drawable with TextView, so below is an example.

```xml
<android.support.v7.widget.AppCompatTextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginBottom="20dp"
        android:drawableLeft="@drawable/ic_flight_takeoff"
        android:gravity="center_horizontal"
        android:text="TextView with Vector Drawable" />
```



As you can see from above code we have used a *VectorDrawable* in the `drawableLeft` attribute of *android.support.v7.widget.AppCompatTextView*, we can also do it from the java code using `AppCompatTextView#setCompoundDrawables`. 

## 3.4 Using VectorDrawable to Customise RadioButton

So far the use was straightforward, what if you want to customise a *RadioButton* or *CheckBox* while using VectorDrawable? Now lets see that. If you go through the [layout we created](https://www.androidhive.info/2017/02/android-working-svg-vector-drawables/#using_vector_drawable), once again then you can find that a *RadioGroup* which contains a series of *AppCompatRadioButton*, all the *AppCompatRadioButton*s there uses `@drawable/radio_selector` as background, below is the code for that.

**radio_selector.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android" >
    <item
        android:drawable="@drawable/ic_star"
        android:state_checked="true"
        android:state_pressed="true" />
    <item
        android:drawable="@drawable/ic_star"
        android:state_pressed="true" />
    <item
        android:drawable="@drawable/ic_star"
        android:state_checked="true" />
    <item
        android:drawable="@drawable/ic_star_border" />
</selector>
```



As you can see this is a selector drawable as usual, the only difference is that it refers to *VectorDrawable*s (vector image resources) instead of raster image resources. The remaining is taken care by *android.support.v7.widget.AppCompatRadioButton* itself as mentioned earlier (remember to use **AppCompatDelegate.setCompatVectorFromResourcesEnabled(true)** for that also, even if you don’t consider backward compatibility).

The final output looks something like this.

<img src="https://www.androidhive.info/wp-content/uploads/2017/02/android-working-with-vector-drawables.png">

I hope this article gave you a very good overview about **Using Vector Drawables in Android**. Feel free to ask any queries / doubts in comments section below.



---



# Android XML Processing with the XmlPullParser - Tutorial

Lars Vogel (c) 2009, 2016 vogella GmbHversion 1.4,28.06.2016

>   XML processing with Android.This article describes how to process XML with Android.

## [1. XML processing in Android](http://www.vogella.com/tutorials/AndroidXML/article.html#xml-processing-in-android)

The Java programming language provides several standard libraries for processing XML files.

Per default, Android provides for XML parsing and writing the `XmlPullParser` class.This parser is not available in standard Java but is similar to the Stax parser.The parser is hosted at [ http://www.xmlpull.org/](http://www.xmlpull.org/).

On Android you use either the `XmlPullParser` or an additioal library like [Simple](http://simple.sourceforge.net/) which makes XML parsing easier.

| **   | The SAX and the DOM  XML parsers are available on Android.SAX and DOM have their limitations, therefore it is not recommended to use them on Android.Therefore this tutorial does not give an example for the usage of this library.The Java standard provides also the Stax parser.This parser is not part of the Android platform. |
| ---- | ---------------------------------------- |
|      |                                          |

## [2. Example for using XmlPullParser](http://www.vogella.com/tutorials/AndroidXML/article.html#example-for-using-xmlpullparser)

The Javadoc of `XmlPullParser` gives a nice example how you can use this library.

```JAVA
 import java.io.IOException;
 import java.io.StringReader;

 import org.xmlpull.v1.XmlPullParser;
 import org.xmlpull.v1.XmlPullParserException.html;
 import org.xmlpull.v1.XmlPullParserFactory;

 public class SimpleXmlPullApp
 {

     public static void main (String args[])
         throws XmlPullParserException, IOException
     {
         XmlPullParserFactory factory = XmlPullParserFactory.newInstance();
         factory.setNamespaceAware(true);
         XmlPullParser xpp = factory.newPullParser();

         xpp.setInput( new StringReader ( "<foo>Hello World!</foo>" ) );
         int eventType = xpp.getEventType();
         while (eventType != XmlPullParser.END_DOCUMENT) {
          if(eventType == XmlPullParser.START_DOCUMENT) {
              System.out.println("Start document");
          } else if(eventType == XmlPullParser.END_DOCUMENT) {
              System.out.println("End document");
          } else if(eventType == XmlPullParser.START_TAG) {
              System.out.println("Start tag "+xpp.getName());
          } else if(eventType == XmlPullParser.END_TAG) {
              System.out.println("End tag "+xpp.getName());
          } else if(eventType == XmlPullParser.TEXT) {
              System.out.println("Text "+xpp.getText());
          }
          eventType = xpp.next();
         }
     }
 }
```

## [3. Prerequisites for the following exercise](http://www.vogella.com/tutorials/AndroidXML/article.html#prerequisites-for-the-following-exercise)

This exercise is based on the [Android library project example](http://www.vogella.com/tutorials/AndroidLibraryProjects/article.html).

## [4. Exercise: Parsing an RSS feed with the XML pull parser](http://www.vogella.com/tutorials/AndroidXML/article.html#exercise-parsing-an-rss-feed-with-the-xml-pull-parser)

In this exercise you download RSS feed data from the network using your `com.example.android.rssfeedlibary` project.

### [4.1. Add permission to access the Internet](http://www.vogella.com/tutorials/AndroidXML/article.html#add-permission-to-access-the-internet)

Add the permission to use the Internet to the Android manifest file of your RSS Reader project.

```
<uses-permission android:name="android.permission.INTERNET"/>
```

| **   | Ensure that you added the permission to the correct manifest file.If you add this permission to the library project, Internet access will not work. |
| ---- | ---------------------------------------- |
|      |                                          |

The resulting manifest should look similar to the following listing.

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.android.rssfeed"
    android:versionCode="1"
    android:versionName="1.1" >

    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:name="RssApplication"
        android:allowBackup="false"
        android:icon="@drawable/launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="RssfeedActivity"
            android:label="@string/title_activity_main" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity
            android:name=".DetailActivity"
            android:label="Details" >
        </activity>
    </application>

</manifest>
```

### [4.2. Perform network access](http://www.vogella.com/tutorials/AndroidXML/article.html#perform-network-access)

Change the parse method in `RssFeedProvider` so that it reads the RSS feed.Also writes the output to the Android log.

```
package com.example.android.rssfeedlibrary;

import android.util.Log;
import android.util.Xml;

import org.xmlpull.v1.XmlPullParser;

import java.io.IOException;
import java.io.InputStream;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class RssFeedProvider {

    static final String PUB_DATE = "pubDate";
    static final String DESCRIPTION = "description";
    static final String CHANNEL = "channel";
    static final String LINK = "link";
    static final String TITLE = "title";
    static final String ITEM = "item";



    public static List<RssItem> parse(String rssFeed) {
        List<RssItem> list = new ArrayList<RssItem>();
        XmlPullParser parser = Xml.newPullParser();
        InputStream stream = null;
        try {
            // auto-detect the encoding from the stream
            stream = new URL(rssFeed).openConnection().getInputStream();
            parser.setInput(stream, null);
            int eventType = parser.getEventType();
            boolean done = false;
            RssItem item = null;
            while (eventType != XmlPullParser.END_DOCUMENT && !done) {
                String name = null;
                switch (eventType) {
                    case XmlPullParser.START_DOCUMENT:
                        break;
                    case XmlPullParser.START_TAG:
                        name = parser.getName();
                        if (name.equalsIgnoreCase(ITEM)) {
                            Log.i("new item", "Create new item");
                            item = new RssItem();
                        } else if (item != null) {
                            if (name.equalsIgnoreCase(LINK)) {
                                Log.i("Attribute", "setLink");
                                item.setLink(parser.nextText());
                            } else if (name.equalsIgnoreCase(DESCRIPTION)) {
                                Log.i("Attribute", "description");
                                item.setDescription(parser.nextText().trim());
                            } else if (name.equalsIgnoreCase(PUB_DATE)) {
                                Log.i("Attribute", "date");
                                item.setPubDate(parser.nextText());
                            } else if (name.equalsIgnoreCase(TITLE)) {
                                Log.i("Attribute", "title");
                                item.setTitle(parser.nextText().trim());
                            }
                        }
                        break;
                    case XmlPullParser.END_TAG:
                        name = parser.getName();
                        Log.i("End tag", name);
                        if (name.equalsIgnoreCase(ITEM) && item != null) {
                            Log.i("Added", item.toString());
                            list.add(item);
                        } else if (name.equalsIgnoreCase(CHANNEL)) {
                            done = true;
                        }
                        break;
                }
                eventType = parser.next();
            }
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            if (stream != null) {
                try {
                    stream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        return list;
    }
}
```

### [4.3. Validating](http://www.vogella.com/tutorials/AndroidXML/article.html#validating)

Start your application and load the RSS feed data.

Once the RSS feed is processed, the `RssItems` should be visible in the list fragment.



# ~ END ~





















































