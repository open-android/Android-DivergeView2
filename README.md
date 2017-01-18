# Android-DivergeView

仿美拍直播的点赞动画。

项目地址：<https://github.com/open-android/Android-DivergeView2>

简书：[http://www.jianshu.com/p/2a830d089310](http://www.jianshu.com/p/2a830d089310 "美拍直播")

## 效果图

![](http://upload-images.jianshu.io/upload_images/4037105-b538df35dccccd81.gif?imageMogr2/auto-orient/strip)

* 爱生活,爱学习,更爱做代码的搬运工,分类查找更方便请下载黑马助手app


![黑马助手.png](http://upload-images.jianshu.io/upload_images/4037105-f777f1214328dcc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 使用步骤

### 1. 在project的build.gradle添加如下代码(如下图)

	allprojects {
	    repositories {
	        maven { url "https://jitpack.io" }
	    }
	}

![](http://upload-images.jianshu.io/upload_images/4037105-2faa5daca3bfe8a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
	

	
### 2. 在Module的build.gradle添加依赖

    compile 'com.github.open-android:Android-DivergeView2:0.1.0'



### 3.布局文件中使用

	<Button
        android:id="@+id/btnStart"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Start"/>

    <lib.homhomlib.view2.DivergeView
        android:id="@+id/divergeView"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:layout_width="130dp"
        android:layout_height="300dp"/>
    <ImageView
        android:id="@+id/iv_start"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginRight="10dp"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:background="@drawable/ic_praise_sm6"/>

### 4.复制如下代码到java类中
   

    private DivergeView mDivergeView;
    private Button mBtnStart;
    private ImageView mImageView;
    private ArrayList<Bitmap> mList;
    private int mIndex = 0;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mBtnStart = (Button)findViewById(R.id.btnStart);
        mImageView = (ImageView)findViewById(R.id.iv_start);
        mList = new ArrayList<>();
        mList.add(((BitmapDrawable) ResourcesCompat.getDrawable(getResources(), R.drawable.ic_praise_sm1, null)).getBitmap());
        mList.add(((BitmapDrawable) ResourcesCompat.getDrawable(getResources(),R.drawable.ic_praise_sm2,null)).getBitmap());
        mList.add(((BitmapDrawable) ResourcesCompat.getDrawable(getResources(),R.drawable.ic_praise_sm3,null)).getBitmap());
        mList.add(((BitmapDrawable) ResourcesCompat.getDrawable(getResources(),R.drawable.ic_praise_sm4,null)).getBitmap());
        mList.add(((BitmapDrawable) ResourcesCompat.getDrawable(getResources(),R.drawable.ic_praise_sm5,null)).getBitmap());
        mList.add(((BitmapDrawable) ResourcesCompat.getDrawable(getResources(), R.drawable.ic_praise_sm6, null)).getBitmap());
        mBtnStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(mIndex == 5){
                    mIndex = 0 ;
                }
                mDivergeView.startDiverges(mIndex);
                mIndex++;
            }
        });
        mDivergeView = (DivergeView) findViewById(R.id.divergeView);
        mDivergeView.post(new Runnable() {
            @Override
            public void run() {
                mDivergeView.setEndPoint(new PointF(mDivergeView.getMeasuredWidth()/2,0));
                mDivergeView.setDivergeViewProvider(new Provider());
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if(mList != null){
            mList.clear();
            mList = null;
        }

    }

    class Provider implements DivergeView.DivergeViewProvider{

        @Override
        public Bitmap getBitmap(Object obj) {
            return mList == null ? null : mList.get((int)obj);
        }
    }

* 详细的使用方法在DEMO里面都演示啦,如果你觉得这个库还不错,请赏我一颗star吧~~~

* 欢迎关注微信公众号

![](http://oi5nqn6ce.bkt.clouddn.com/itheima/booster/code/qrcode.png)
