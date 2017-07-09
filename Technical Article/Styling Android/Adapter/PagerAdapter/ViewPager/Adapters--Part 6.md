# Adapters – Part 6

**[May 10, 2013](https://blog.stylingandroid.com/adapters-part-6/)**[Mark Allison](https://blog.stylingandroid.com/author/admin/)**[No comment](https://blog.stylingandroid.com/adapters-part-6/#respond) 

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
}
```

