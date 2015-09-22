# Android AdvancedPagerSlidingTabStrip

Android AdvancedPagerSlidingTabStrip是一种Android平台的导航控件，完美兼容Android自带库和兼容库的`ViewPager`组件。

#新更新！

last version: v1.0.0

new version: v1.0.2b

NEXT :

我将会更新demo，并增加几个功能，包括：将小圆点换成带有数字显示的形态；单独的tab背景效果，不再用绘制方式（已经完成）；可以循环拉动，到最后的时候会拉回到第一个。
以及文档的更新，一些细节优化和bug修复，以及将库打包，可以直接gradle。

# v1.0.1内容:

①将tab的indicateLine变为和textview长度一致的形态，现在多了一种显示效果。

②现在iconTab也可以显示小圆点了!iconTab情况下有新消息也可以展示了。

# v1.0.2b内容（2015年9月22日）：

①增加可以自定义view的tab：customtab，文档后续会介绍，还缺少一些优化，会持续关注

![p1](http://ww4.sinaimg.cn/mw1024/6e4e0c91gw1euym6rifr7j20810g2dgl.jpg)![p2](http://ww2.sinaimg.cn/bmiddle/6e4e0c91gw1euym6s3jw3j20810g2dgm.jpg)![p3](http://ww1.sinaimg.cn/bmiddle/6e4e0c91gw1euymy0xtn7j20810g2dgl.jpg)![p4](http://ww1.sinaimg.cn/bmiddle/6e4e0c91gw1ew6q3hxg7qj20k00zkdh8.jpg)![p5](http://ww4.sinaimg.cn/bmiddle/6e4e0c91gw1ew6q95gmllj20k00zk400.jpg)![p6](http://ww3.sinaimg.cn/bmiddle/6e4e0c91gw1ewb9a9y0kyj20k00zkmym.jpg)

#用法

将Library导入工程，在需要添加的界面xml中添加组件和ViewPager

    <com.lhh.apst.library.AdvancedPagerSlidingTabStrip
        android:id="@+id/tabs"
        android:layout_width="match_parent"
        android:layout_height="55dp"
        style="@style/pagertab_icon_style"
        android:layout_alignParentBottom="true"
        android:fillViewport="false"/>

    <style name="pagertab_style">
        <item name="android:background">@drawable/tab_bg_normal</item>
        <item name="ptabBackground">@drawable/tab_bg_transparent</item>
        <item name="android:textSize">13sp</item>
        <item name="android:textAppearance">@style/CustomTabPageIndicator.Text</item>
        <item name="android:textColor">@drawable/tab_color_select</item>
        <item name="indicatorColor">@color/home_bar_text_push</item>
        <item name="underlineColor">#1A000000</item>
        <item name="dividerColor">#00000000</item>
        <item name="shouldExpand">false</item>
        <item name="tabPaddingLeftRight">8dp</item>
        <item name="apsts_draw_mode">text</item>
        <item name="tabTextSelectColor">@color/home_bar_text_push</item>
    </style>

在代码中find该组件，并且设置adapter和ViewPager。

    ViewPager pager = (ViewPager) findViewById(R.id.pager);
    pager.setAdapter(new TestAdapter(getSupportFragmentManager()));


    AdvancedPagerSlidingTabStrip tabs = (AdvancedPagerSlidingTabStrip) findViewById(R.id.tabs);
    tabs.setViewPager(pager);


AdvancedPagerSlidingTabStrip支持绑定OnPageChangeListener，并且不影响使用效果。

    tabs.setOnPageChangeListener(mPageChangeListener);

# 特点

一、现在你可以使用带有文字和图片的Tab了，并且带有多种切换的效果。

  1.带有文字的图片
  只需要将你的Adapter实现AdvancedPagerSlidingTabStrip.IconTabProvider即可。其中提供getPageIconText(int index)方法用于返回index位置的图片文字。

  2.切换效果
  AdvancedPagerSlidingTabStrip.IconTabProvider中提供了getPageIconSelectResId(int index)和getPageIconResId(int index)两个方法，前者用于实现选中时候的图片效果，后者用于实现默认情况下的图片效果。


二、带有提示小点的tab。现在你可以通过AdvancedPagerSlidingTabStrip实现像iOS一样的红点提示功能了。

   1.带有提示点的tab
     只需要调用AdvancedPagerSlidingTabStrip的showDot(int index)或者hideDot(int index)即可实现红点的显示和隐藏两个方法，index代表需要显示和隐藏的tab序列位置（0 ~ N）。
     该方法对任意一种tab（IconTab和TextTab都有效）。

三、跟随TextView的动态显示效果模式。现在你可以通过AdvancedPagerSlidingTabStrip实现下划线跟随TextView的动态效果了。任意tab都有效果！

四、自定义View形式的Tab。你可以通过实现为每个View自定义的形式来创建属于你自己的Tab。

    通过将Adapter实现CustomTabProvider接口，实现其中的getDisSelectTabView(int position, View convertView)和getSelectTabView(int position, View convertView) 回调即可，前者为非选中状态下的TabView视图，后者为选中状态下的TabView视图，具体查看demo。

五、BUG修复和参数增加

    默认情况下一些字体和颜色设置无效的问题也在AdvancedPagerSlidingTabStrip中得到了修复。

# 参数

 * `indicatorColor` Color of the sliding indicator
 * `underlineColor` Color of the full-width line on the bottom of the view
 * `dividerColor` Color of the dividers between tabs
 * `indicatorHeight`Height of the sliding indicator
 * `underlineHeight` Height of the full-width line on the bottom of the view
 * `dividerPadding` Top and bottom padding of the dividers
 * `tabPaddingLeftRight` Left and right padding of each tab
 * `tabPaddingTopBottom` Top and bottom padding of each tab
 * `scrollOffset` Scroll offset of the selected tab
 * `tabBackground` Background drawable of each tab, should be a StateListDrawable
 * `shouldExpand` If set to true, each tab is given the same weight, default false
 * `textAllCaps` Tab的文字是否为全部大写，如果是true就全部大写，默认为true
 * `tabTextSelectColor` 你所选择的那个tab的颜色
 * `apsts_draw_mode` 绘制模式，text或者normal，用于是否将下划线绘制为跟随TextView

# 更新日志

### 当前版本: 1.0.1

# Developed By

 * Linhonghong - <linhh90@163.com> (本小弟，^_^)

#PS

  该组件基于Andreas Stuetz的PagerSlidingTabStrip[Github](https://github.com/astuetz/PagerSlidingTabStrip/)

