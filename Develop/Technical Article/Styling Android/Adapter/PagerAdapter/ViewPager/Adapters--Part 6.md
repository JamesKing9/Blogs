# Adapters – Part 6

[May 10, 2013](https://blog.stylingandroid.com/adapters-part-6/)

Previously in this [series](https://blog.stylingandroid.com/archives/1679) we’ve looked at different kinds of *Adapter*s, and in two separate separate series on Styling Android ([ViewPager](https://blog.stylingandroid.com/archives/537) and [ViewPager Redux](https://blog.stylingandroid.com/archives/1357)) we’ve looked at *ViewPager*s. In this article we’re going to look at the common factor of both of these: *PagerAdapters*.

 

A *PagerAdapter* is responsible for creating the content for each page within a *ViewPager*. It takes two main forms: When creating or inflating a standard *View* hierarchy the standard *PagerAdapter* is used, but when each page is a *Fragment* we can use *FragmentPagerAdapter* instead. Let’s start with the former:

```java
private static String[] titles = new String[]{"Page 1", "Page 2", "Page 3", "Page 4", "Page 5";};

private class MyPagerAdapter extends PagerAdapter {
  @Override
  public int getCount() {
    return titles.length;
  }
  
  @Override
  public boolean isViewFromObject(View view, Object object) {
    return view.equals(object);
  }
  
  @Override
  public Object instantiateItem(ViewGroup container, int position) {
    TextView text = new TextView(getActivity());
    text.setText(titles[position]);
    container.addView(text);
    return text;
  }
  
  @Override
  public void destroyItem(ViewGroup container, int position, Object object) {
     if(object instanceof View) {
       container.removeView((View)object);
     }
  }
  
  @Override
  public CharSequence getPageTitle(int position) {
    return titltes[position];
  }
}
```

This is pretty much as simple as we can get it. The view that is created is a simple `TextView ` and we set the text to the value of the appropriate string from the titles array. In the `instantiateItem()` method we could, just as easily, use a LayoutInflator to inflate a layout from XML and then find the controls to bind to. We could also create or inflate different layouts depending on the position. But the basic principle in that getCount() returns the number of pages to display, instantiateItem() gets called to create the individual layouts, destroyItem() gets called to remove the layouts, and getPageTitle() returns the title to use in a PagerTabStrip or PagerTitleStrip.



To create `Fragment` instead of a View hierarchy, we first need to create a Fragment class:

```java
public static class MyFragment extends Fragment {
  private static final String TAG = "MyFragment";
  public MyFragment() {
    super();
  }
  
  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View view = inflater.inflate(R.layout.page, container, false);
    View text = view.findViewById(android.R.id.text1);
    if (text != null && text instanceof TextView) {
      ((TextView)text).setText(titles[getArguments().getInt("position")]);
    }
    return view;
  }
  
  @Override
  public void onAttach(Activity activity) {
    super.onAttach(activity);
    Log.d(TAG, "Attached " + getArguments().getInt("position"));
  }
  
  @Override
  public void onDetach() {
    Log.d(TAG, "Detached " + getArguments().getInt("position"));
    super.onDetach();
  }
}
```

Our *Fragment* class, `MyFragment`, creates a layout identical to the one used in the previous example, only in this case it inflates it from XML instead of creating the View objects programatically. Either approach is fine, just chose whichever suits the task that you’re trying to perform best – I’ve simply included both forms here to show that it can be done. The overrides of the `onAttach()` and `onDetach()` methods simply add a little logging to show when the instances of this class become attached and detached from an *Activity* (the reasons for adding this will become obvious later on). 

The *Adapter* itself is actually simpler than the previous *PagerAdapter* example because we don’t need to worry about the `destroyItem()` method this time:



















