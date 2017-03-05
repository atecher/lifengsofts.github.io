---
title: RecyclerView的使用解析
date: 2017-03-05 10:48:03
categories: Android
tags: 
    - RecyclerView
---
# 为什么要使用它

RecyclerView比ListView更灵活，比如我现在是显示一个List，过一会儿需要换成Grid格式，在这种情况下如果使用的是ListView，那我们需要换成GridView等，下面就来看看他的基本使用

# 添加控件到布局文件

```xml
<android.support.v7.widget.RecyclerView
    android:id="@+id/my_recycler_view"
    android:scrollbars="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```

# 设置布局管理器

所谓布局管理器就是你要告诉RecyclerView怎样去显示一个Item，因为他不像ListView那样一开始就定义死了怎么布局，比如ListView定义死了垂直布局，而GridView用于显示格式样式的布局。他提供了几个默认的实现

- LinearLayoutManager：垂直或水平滚动列表方式显示项目。
- GridLayoutManager：网格中显示项目。
- StaggeredGridLayoutManager：在分散对齐网格中显示项目。

我们这里用垂直布局管理器

```java
//设置布局管理器
LinearLayoutManager linearLayoutManager = new LinearLayoutManager(this);
rv.setLayoutManager(linearLayoutManager);
```

# 设置adapter

这一步和ListView这类的控件使用的方式差不多，也要设置一个适配器，告诉他数据源，他是继承RecyclerView.Adapter，我们需要实现三个方法

onCreateViewHolder：创建一个ViewHolder

onBindViewHolder：为ViewHolder绑定数据

getItemCount：整个列表的长度

```java
public class SimpleAdapter extends BaseRecyclerViewAdapter<String, SimpleAdapter.ViewHolder> {

    public SimpleAdapter(Context context) {
        super(context);
    }

    //下面两个方法想当与BaseAdapter的getView，只是他将创建view和设置view数据分开了
    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        return new ViewHolder(LayoutInflater.from(context).inflate(android.R.layout.simple_list_item_1, parent, false));
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
        holder.bindView(getItem(position), position);
    }


    public class ViewHolder extends RecyclerView.ViewHolder {

        private final TextView tv;

        public ViewHolder(View itemView) {
            super(itemView);
            tv = (TextView) itemView.findViewById(android.R.id.text1);
        }

        public void bindView(final String item, final int position) {
            tv.setText(item);
            tv.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    onItemClickListener.onItemClick(position);
                }
            });
        }
    }


}
```

这里我写了一个通用的Adapter

```java
package cn.woblog.recyclerviewsimple;

import android.content.Context;
import android.support.v7.widget.RecyclerView;

import java.util.ArrayList;
import java.util.List;

public abstract class BaseRecyclerViewAdapter<D, VH extends RecyclerView.ViewHolder> extends RecyclerView.Adapter<VH> {
    /**
     * 条目点击事件
     */
    protected OnItemClickListener onItemClickListener;

    protected final Context context;

    public void setOnItemClickListener(OnItemClickListener onItemClickListener) {
        this.onItemClickListener = onItemClickListener;
    }

    public BaseRecyclerViewAdapter(Context context) {
        this.context = context;
    }

    private List<D> data = new ArrayList<>();

    public List<D> getData() {
        return data;
    }

    public D getItem(int position) {
        return data.get(position);
    }

    //整个列表的长度，类似BaseAdapter的getCount
    @Override
    public int getItemCount() {
        return data.size();
    }

    public void setData(List<D> data) {
        this.data.clear();
        this.data.addAll(data);
        notifyDataSetChanged();
    }

    public void addData(List<D> data) {
        this.data.addAll(data);
        notifyDataSetChanged();
    }

    public interface OnItemClickListener {
        void onItemClick(int position);
    }
}
```

他定义了data列表对应最终的数据集合，定义了一个条目点击事件接口。接下来我们将整个适配器设置到RecyclerView

```java
//设置adapter
simpleAdapter = new SimpleAdapter(this);
rv.setAdapter(simpleAdapter);

simpleAdapter.setOnItemClickListener(this);

simpleAdapter.setData(getTestData());
```

到这一步我们这个相当于ListView的列表已经显示出来了

//无分割线图

但是还发现少点什么，对，就是分割线，RecyclerView的分割线实现起来要比ListView要难一点，我们需要通过addItemDecoration添加一个实现，居然没人默认的实现，真是醉了，这里我们先实现一个垂直列表的水平分割线，实现分割线需要继承ItemDecoration类，一般要复写如下方法：

- onDraw：改方法调用在drawChildren之前
- onDrawOver：该方法调用位于drawChildren之后
- getItemOffsets：通过outRect.set方法为每一个Item设置一个偏移量，用来绘制分割线

onDraw和onDrawOver一般只需要重写其中一个

```java
package cn.woblog.recyclerviewsimple;

import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Canvas;
import android.graphics.Rect;
import android.graphics.drawable.Drawable;
import android.support.v7.widget.RecyclerView;
import android.view.View;
import android.widget.LinearLayout;

public class ListItemDecoration extends RecyclerView.ItemDecoration {

    private static final int[] ATTRS = new int[]{
            android.R.attr.listDivider
    };

    private Drawable mDivider;

    private int mOrientation;

    public ListItemDecoration(Context context, int orientation) {
        final TypedArray a = context.obtainStyledAttributes(ATTRS);
        mDivider = a.getDrawable(0);
        a.recycle();
        setOrientation(orientation);
    }

    public void setOrientation(int orientation) {
        mOrientation = orientation;
    }

    @Override
    public void onDraw(Canvas c, RecyclerView parent) {
        if (mOrientation == LinearLayout.VERTICAL) {
            drawVertical(c, parent);
        } else {
            drawHorizontal(c, parent);
        }

    }

    public void drawVertical(Canvas c, RecyclerView parent) {
        final int left = parent.getPaddingLeft();
        final int right = parent.getWidth() - parent.getPaddingRight();

        //获取每个child个数
        final int childCount = parent.getChildCount();
        for (int i = 0; i < childCount; i++) {
            //获取到每一个child
            final View child = parent.getChildAt(i);

            //获取到每个child的params
            final RecyclerView.LayoutParams params = (RecyclerView.LayoutParams) child
                    .getLayoutParams();

            //计算分割线的顶部位置=当前Item的高度+当前item到顶部分割线的距离
            final int top = child.getBottom() + params.topMargin;

            //计算分割线的底部位置=top+分割线的真实高度+当前Item到底部分割线的距离
            final int bottom = top + mDivider.getIntrinsicHeight() + params.bottomMargin;

            //设置分割线线的边距
            mDivider.setBounds(left, top, right, bottom);
            mDivider.draw(c);
        }
    }

    public void drawHorizontal(Canvas c, RecyclerView parent) {
        final int top = parent.getPaddingTop();
        final int bottom = parent.getHeight() - parent.getPaddingBottom();

        final int childCount = parent.getChildCount();
        for (int i = 0; i < childCount; i++) {
            final View child = parent.getChildAt(i);
            final RecyclerView.LayoutParams params = (RecyclerView.LayoutParams) child
                    .getLayoutParams();
            final int left = child.getRight() + params.leftMargin;
            final int right = left + mDivider.getIntrinsicHeight() + params.rightMargin;
            mDivider.setBounds(left, top, right, bottom);
            mDivider.draw(c);
        }
    }

    @Override
    public void getItemOffsets(Rect outRect, int itemPosition, RecyclerView parent) {
        if (mOrientation == LinearLayout.VERTICAL) {
            outRect.set(0, 0, 0, mDivider.getIntrinsicHeight()); //dp单位
        } else {
            outRect.set(0, 0, mDivider.getIntrinsicWidth(), 0);
        }
    }
}

```

设置分割线

```java
//设置分割线
rv.addItemDecoration(new ListItemDecoration(this, LinearLayoutManager.VERTICAL));
```

到这里一个效果基本ListView差不多了

# 定制分割线样式

到这一步虽然分割线已经显示出来了，但是还是系统默认的，我们肯定有需要换颜色的需要对吧。我们从上面可以得知是使用了系统的listDivider属性，那要更改分割线肯定也是更改他了

item_divider.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" 
    android:shape="rectangle">
    <size android:width="10dp" android:height="10dp"/>
	<solid android:color="#ff0000"/>
</shape>
```

我这里定义的高度为1dp，形状为矩形，大家可以根据自己的需求随便改。重要的步骤来了，就是要设置listDivider属性了，可以直接在application对应的theme里面设置，也可以对单个activity的theme设置

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <item name="android:listDivider">@drawable/item_divider</item>
</style>
```

## LinearLayoutManager

这个布局管理器可以垂直和水平

使用ItemViewDecoration

ItemViewDecoration.java

```java
package cn.woblog.android;

import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Canvas;
import android.graphics.Rect;
import android.graphics.drawable.Drawable;
import android.support.v4.view.ViewCompat;
import android.support.v7.widget.RecyclerView;
import android.support.v7.widget.RecyclerView.ItemDecoration;
import android.support.v7.widget.RecyclerView.LayoutParams;
import android.support.v7.widget.RecyclerView.State;
import android.view.View;
import android.widget.LinearLayout;

/**
 * Created by renpingqing on 2017/3/4.
 */

public class ItemViewDecoration extends ItemDecoration {

  private int orientation;
  private final int[] atts = new int[]{android.R.attr.listDivider};
  private final Drawable dividerDrawable;
  private final Context context;

  public ItemViewDecoration(Context context, int orientation) {
    this.context = context;
    this.orientation = orientation;
    TypedArray typedArray = context.obtainStyledAttributes(atts);
    dividerDrawable = typedArray.getDrawable(0);
    typedArray.recycle();
  }

  public ItemViewDecoration(Context context) {
    this(context, LinearLayout.VERTICAL);
  }

  @Override
  public void onDraw(Canvas c, RecyclerView parent, State state) {
    super.onDraw(c, parent, state);
    if (isVertical()) {
      drawVertical(c, parent, state);
    } else {
      drawHorizontal(c, parent, state);
    }
  }

  private void drawHorizontal(Canvas c, RecyclerView parent, State state) {
    int top = parent.getPaddingTop();
    int bottom = parent.getHeight() - parent.getPaddingBottom();

    int childCount = parent.getChildCount();
    for (int i = 0; i < childCount; i++) {
      View view = parent.getChildAt(i);
      RecyclerView.LayoutParams params = (LayoutParams) view.getLayoutParams();
      int left =
          view.getRight() + params.rightMargin + Math.round(ViewCompat.getTranslationX(view));
      int right = left + dividerDrawable.getIntrinsicWidth();
      dividerDrawable.setBounds(left, top, right, bottom);
      dividerDrawable.draw(c);
    }
  }

  private void drawVertical(Canvas c, RecyclerView parent, State state) {
    int left = parent.getPaddingLeft();
    int right = parent.getWidth() - parent.getPaddingRight();
    int childCount = parent.getChildCount();
    for (int i = 0; i < childCount; i++) {
      View view = parent.getChildAt(i);
      RecyclerView.LayoutParams params = (LayoutParams) view.getLayoutParams();
      int top =
          view.getBottom() + params.bottomMargin + Math.round(ViewCompat.getTranslationY(view));
      int bottom = top + dividerDrawable.getIntrinsicHeight();
      dividerDrawable.setBounds(left, top, right, bottom);
      dividerDrawable.draw(c);
    }
  }

  private boolean isVertical() {
    return orientation == LinearLayout.VERTICAL;
  }

  public void setOrientation(int orientation) {
    this.orientation = orientation;
  }

  @Override
  public void getItemOffsets(Rect outRect, View view, RecyclerView parent, State state) {
    if (isVertical()) {
      outRect.set(0, 0, 0, dividerDrawable.getIntrinsicHeight());
    } else {
      outRect.set(0, 0, dividerDrawable.getIntrinsicWidth(), 0);
    }
  }
}
```

### 水平方向

```java
rv.setLayoutManager(new LinearLayoutManager(this, LinearLayout.HORIZONTAL,false));
itemViewDecoration = new ItemViewDecoration(this,LinearLayout.HORIZONTAL);
rv.addItemDecoration(itemViewDecoration);
```

### 垂直方向

```jade
rv.setLayoutManager(new LinearLayoutManager(this));
itemViewDecoration = new ItemViewDecoration(this);
rv.addItemDecoration(itemViewDecoration);
```

## GridLayoutManager

使用ItemGridViewDecoration，他里面写了两种情况，一种是四边都有，一种是只有中间才有

```java
package cn.woblog.android;

import android.content.Context;
import android.content.res.TypedArray;
import android.graphics.Canvas;
import android.graphics.Rect;
import android.graphics.drawable.Drawable;
import android.support.v7.widget.GridLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.support.v7.widget.RecyclerView.ItemDecoration;
import android.support.v7.widget.RecyclerView.LayoutParams;
import android.support.v7.widget.RecyclerView.State;
import android.support.v7.widget.StaggeredGridLayoutManager;
import android.view.View;
import android.widget.LinearLayout;

/**
 * Created by renpingqing on 2017/3/4.
 */

public class ItemGridViewDecoration extends ItemDecoration {

  private int orientation;
  private final int[] atts = new int[]{android.R.attr.listDivider};
  private final Drawable dividerDrawable;
  private final Context context;
  private int spanCount;

  public ItemGridViewDecoration(Context context) {
    this.context = context;
    TypedArray typedArray = context.obtainStyledAttributes(atts);
    dividerDrawable = typedArray.getDrawable(0);
    typedArray.recycle();
  }

  @Override
  public void onDraw(Canvas c, RecyclerView parent, State state) {
    super.onDraw(c, parent, state);
    drawVertical(c, parent, state);
    drawHorizontal(c, parent, state);
  }

  private void drawHorizontal(Canvas c, RecyclerView parent, State state) {
    int childCount = parent.getChildCount();
    for (int i = 0; i < childCount; i++) {
      View view = parent.getChildAt(i);
      LayoutParams params = (LayoutParams) view.getLayoutParams();

      int c2 = i % spanCount;

      if (i <= spanCount) {
        //第一行，绘制第一行，顶部
        int left = view.getLeft() - params.rightMargin - dividerDrawable.getIntrinsicWidth();

        int top = params.bottomMargin;
//      这里加上dividerDrawable.getIntrinsicWidth()，边框宽度，就可以绘制到下一个格子的左边，如果这里不加，当然也可以加在绘制垂直的时候
        int right = view.getRight() + params.rightMargin + dividerDrawable.getIntrinsicWidth();
        int bottom = top + dividerDrawable.getIntrinsicHeight() + params.bottomMargin;
        dividerDrawable.setBounds(left, top, right, bottom);
        dividerDrawable.draw(c);
      }

      //左边减去divider的宽度，就可以绘制最左边的线了
      int left = view.getLeft() - params.rightMargin - dividerDrawable.getIntrinsicWidth();
      int top = view.getBottom() + params.bottomMargin;
//      这里加上dividerDrawable.getIntrinsicWidth()，边框宽度，就可以绘制到下一个格子的左边，如果这里不加，当然也可以加在绘制垂直的时候
      int right = view.getRight() + params.rightMargin + dividerDrawable.getIntrinsicWidth();
      int bottom = top + dividerDrawable.getIntrinsicHeight() + params.bottomMargin;
      dividerDrawable.setBounds(left, top, right, bottom);
      dividerDrawable.draw(c);
    }
  }

  private void drawVertical(Canvas c, RecyclerView parent, State state) {
    int childCount = parent.getChildCount();
    for (int i = 0; i < childCount; i++) {
      View view = parent.getChildAt(i);
      LayoutParams params = (LayoutParams) view.getLayoutParams();

      int c2 = i % spanCount;
//      if (c2 == 2) {
      //第一列，左边线
      int left = params.rightMargin;
      int top = view.getTop() - params.bottomMargin - dividerDrawable.getIntrinsicHeight(); //就能补齐
      int right = left + dividerDrawable.getIntrinsicWidth();
      int bottom = view.getBottom() + params.bottomMargin;
      dividerDrawable.setBounds(left, top, right, bottom);
      dividerDrawable.draw(c);
//      }

      left = view.getRight() + params.rightMargin;
      top = view.getTop() - params.bottomMargin;
      right = left + dividerDrawable.getIntrinsicWidth();
      bottom = view.getBottom() + params.bottomMargin;
      dividerDrawable.setBounds(left, top, right, bottom);
      dividerDrawable.draw(c);


    }
  }

  private boolean isVertical() {
    return orientation == LinearLayout.VERTICAL;
  }

  public void setOrientation(int orientation) {
    this.orientation = orientation;
  }

  @Override
  public void getItemOffsets(Rect outRect, View view, RecyclerView parent, State state) {
    //左边，右边都偏移divider宽度

    int itemCount = 0;
    int position = 0;

    if (parent.getLayoutManager() instanceof GridLayoutManager) {
      GridLayoutManager layoutManager = (GridLayoutManager) parent.getLayoutManager();

      itemCount = layoutManager.getItemCount();
      position = layoutManager.getPosition(view) + 1;
      spanCount = layoutManager.getSpanCount();
    } else if (parent.getLayoutManager() instanceof StaggeredGridLayoutManager) {
      //TODO 显示还有问题
      StaggeredGridLayoutManager layoutManager = (StaggeredGridLayoutManager) parent
          .getLayoutManager();

      itemCount = layoutManager.getItemCount();
      position = layoutManager.getPosition(view) + 1;
      spanCount = layoutManager.getSpanCount();
    }

    int childSize = parent.getChildCount();

    int rowCount = itemCount / spanCount - 1;
    int lastRowStart = rowCount * spanCount;

    int c = position % spanCount;

//    //    ---中间，四边都有
//    if (position <= spanCount) {
//      //如果是第一列
//      if (c == 1) {
//        outRect.set(dividerDrawable.getIntrinsicWidth(), dividerDrawable.getIntrinsicWidth(),
//            dividerDrawable.getIntrinsicWidth(), dividerDrawable.getIntrinsicHeight());
//      } else {
//        outRect.set(0, dividerDrawable.getIntrinsicHeight(), dividerDrawable.getIntrinsicWidth(),
//            dividerDrawable.getIntrinsicHeight());
//      }
//
//    } else {
//      //判断是否是第一列
//      if (c == 1) {
//        outRect.set(dividerDrawable.getIntrinsicWidth(), 0, dividerDrawable.getIntrinsicWidth(),
//            dividerDrawable.getIntrinsicHeight());
//      } else {
//        outRect
//            .set(0, 0, dividerDrawable.getIntrinsicWidth(), dividerDrawable.getIntrinsicHeight());
//      }
//
//    }
//
//    //    \---中间，四边都有

//    ---只有中间才有分割线
    if (position > lastRowStart) {
      //最后一行
      //最后一列
      if (c == 0) {
        outRect.set(0, 0, 0, 0);
      } else {
        outRect.set(0, 0, dividerDrawable.getIntrinsicWidth(), 0);
      }
    } else {
      if (c == 0) {
        outRect.set(0, 0, 0, dividerDrawable.getIntrinsicHeight());
      } else {
        outRect
            .set(0, 0, dividerDrawable.getIntrinsicWidth(), dividerDrawable.getIntrinsicHeight());
      }
    }

    //    \---只有中间才有分割线
  }


}
```

使用的时候添加一个布局管理器和一个分割线

```
rv.setLayoutManager(new GridLayoutManager(this,3));
rv.addItemDecoration(new ItemGridViewDecoration(this));
```



# 常见错误

## item宽度一直是wrap_content

布局里面我们一直是写的match_parent，但是运行后却不是，最后发现是inflate时没有穿parent

```kotlin
//return ViewHolder(ViewGroup.inflate(parent.ctx, R.layout.item_weather, null),itemClick);
//return ViewHolder(View.inflate(parent.ctx, R.layout.item_weather, null),itemClick);
return ViewHolder(LayoutInflater.from(parent.context).inflate(R.layout.item_weather, parent,false),itemClick);
```

## ScrollView嵌套

对于这个问题，网上的解决办法五花八门，但都是重写layoutManager的onMeasure方法，这样会有各种问题，要么兼容性不好，要么有性能问题，好消息是在23.2.0后，google提供了官方解决方法，我们只需要

```kotlin
layoutManager.isAutoMeasureEnabled = true
```

这样就不会有问题了

# 瀑布流

## 设置布局管理器

```java
rv = (RecyclerView) findViewById(R.id.rv);
rv.setLayoutManager(new StaggeredGridLayoutManager(3, LinearLayout.VERTICAL));
```

## 设置高度

```java
public void onBindViewHolder(ListAdapter.ViewHolder holder, int position) {
  MyData data = getData(position);
  LayoutParams layoutParams = holder.tv.getLayoutParams(); //
  layoutParams.height=data.getHeight();
  holder.tv.setBackgroundColor(data.getColor());
}
```

通常使用这种方式：

```
return new ViewHolder(layoutInflater.inflate(R.layout.item_1,parent,false));
```

但是如果你使用了这种：

```
return new ViewHolder(View.inflate(context,R.layout.item_1,null));
```

如果你的item_1里面外层有ViewGroup包裹那也是没问题的，因为holder.tv.getLayoutParams()就能返回值了，如果没有包裹，那这里是空。

但是如果手动传值给parent给他，也会报错，只不过不是这里空指针。

```
return new ViewHolder(View.inflate(context,R.layout.item_2,parent));
```

如果这样就会报错：

java.lang.IllegalStateException: The specified child already has a parent. You must call removeView() on the child's parent first.

原因是新创建的view是否添加到布局是由RecyelerView决定的，如果我们手动添加就会导致有两个父类。

解放方式是要么，在外层包裹一个ViewGroup,或者直接使用layoutInflater填充布局。一般不要用View.inflate，这就是偷懒的代价。

## 动态更改List和瀑布流效果

只需要更改布局管理器

```java
if (isList) {
  rv.setLayoutManager(new StaggeredGridLayoutManager(3, LinearLayout.VERTICAL));
} else {
  rv.setLayoutManager(new LinearLayoutManager(this));
}
```

