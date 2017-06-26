原文作者：https://github.com/gongwen/MarqueeViewLibrary

# MarqueeViewDemo
通过MarqueeFactory来提供各种样式的跑马灯View，
支持自定义跑马灯ItemView

### 效果图
![image](https://github.com/mengcuiguang/MarqueeViewLibrary-master/blob/master/test.gif ) 

#### 属性

| Attribute 属性          | Description 描述 |
|:---				     |:---|
| marqueeInterval         |    翻页时间间隔       |
| marqueeAnimDuration         | 动画执行时间            |
| marqueeAnimIn         |  marquee in动画          |
| marqueeAnimOut         | marquee out动画          |

#### 通过自定义MarqueeFactory来设置ItemView
继承自MarqueeFactory，通过泛型指定ItemView类型以及ItemData类型，之后实现generateMarqueeItemView方法，提供ItemView，并为ItemView设置数据即可。
##### 例如：
```
public class NoticeMF extends MarqueeFactory<TextView, String> {
    private LayoutInflater inflater;

    public NoticeMF(Context mContext) {
        super(mContext);
        inflater = LayoutInflater.from(mContext);
    }

    @Override
    public TextView generateMarqueeItemView(String data) {
        TextView mView = (TextView) inflater.inflate(R.layout.notice_item, null);
        mView.setText(data);
        return mView;
    }
}
```

#### 设置列表数据
###### 适用于仅设置一次数据源
<pre>
MarqueeFactory<TextView, String> marqueeFactory = new NoticeMF(this);
marqueeFactory.setData(datas);
</pre>
###### 适用于多次设置数据源
<pre>
MarqueeFactory<TextView, String> marqueeFactory = new NoticeMF(this);
marqueeFactory.resetData(datas);
</pre>
#### 设置事件监听
<pre>
marqueeFactory.setOnItemClickListener(new MarqueeFactory.OnItemClickListener<TextView, String>() {
            @Override
            public void onItemClickListener(MarqueeFactory.ViewHolder<TextView, String> holder) {
                Toast.makeText(MainActivity.this, holder.data, Toast.LENGTH_SHORT).show();
            }
});
</pre>

#### MarqueeView设置Factory
<code>marqueeView.setMarqueeFactory(marqueeFactory);</code>


#### 重影问题可参考以下解决方案(参考自[这里](https://github.com/sfsheng0322/MarqueeView))

<pre>
@Override
public void onStart() {
    super.onStart();
    marqueeView.startFlipping();
}

@Override
public void onStop() {
    super.onStop();
    marqueeView.stopFlipping();
}
</pre>
