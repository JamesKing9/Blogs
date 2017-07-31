   



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

Add the **<android.support.v7.widget.CardView>** widget to your layout and place other UI widgets like TextViews, ImageViews inside it. You can notice that the below CardView widget contains a single **TextView**.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
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
	android:background="color/viewBg"
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



































































