# View的生命周期

为了验证View的生命周期，笔者做了以下实验：
``` Java

public class MyTestView extends View {
    private static final String TAG = "MyTestView";
    public MyTestView(Context context) {
        super(context);
        Log.i(TAG, "MyTestView(Context context)");
    }

    public MyTestView(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        Log.i(TAG, "MyTestView(Context context, @Nullable AttributeSet attrs)");
    }

    public MyTestView(Context context, @Nullable AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        Log.i(TAG, "MyTestView(Context context, @Nullable AttributeSet attrs, int defStyleAttr)");
    }

    @Override
    protected void onFinishInflate() {
        super.onFinishInflate();

        Log.i(TAG, "onFinishInflate");
    }

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);

        Log.i(TAG, "onMeasure()");
    }

    @Override
    protected void onLayout(boolean changed, int left, int top, int right, int bottom) {
        super.onLayout(changed, left, top, right, bottom);
        Log.i(TAG, "onLayout");
    }

    @Override
    protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        super.onSizeChanged(w, h, oldw, oldh);
        Log.i(TAG, "onSizeChanged");
    }


    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        Log.i(TAG, "onDraw");
    }

    @Override
    protected void onFocusChanged(boolean gainFocus, int direction, @Nullable Rect previouslyFocusedRect) {
        super.onFocusChanged(gainFocus, direction, previouslyFocusedRect);

        Log.i(TAG, "onFocusChanged");
    }

    @Override
    public void onWindowFocusChanged(boolean hasWindowFocus) {
        super.onWindowFocusChanged(hasWindowFocus);

        Log.i(TAG, "onWindowFocusChanged");
    }

    @Override
    protected void onAttachedToWindow() {
        super.onAttachedToWindow();

        Log.i(TAG, "onAttachedToWindow");
    }

    @Override
    protected void onDetachedFromWindow() {
        super.onDetachedFromWindow();

        Log.i(TAG, "onDetachedFromWindow");
    }

    @Override
    protected void onWindowVisibilityChanged(int visibility) {
        super.onWindowVisibilityChanged(visibility);

        Log.i(TAG, "onWindowVisibilityChanged");
    }
}

public class MainActivity extends AppCompatActivity {
    private static final String TAG = "MyMainActivity";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Log.i(TAG, "onCreate()1");
        setContentView(R.layout.activity_main);
        Log.i(TAG, "onCreate()2");
    }

    @Override
    protected void onStart() {
        super.onStart();
        Log.i(TAG, "onStart()");
    }

    @Override
    protected void onRestart() {
        super.onRestart();
        Log.i(TAG, "onRestart()");
    }

    @Override
    protected void onResume() {
        super.onResume();
        Log.i(TAG, "onResume()");
    }

    @Override
    protected void onPause() {
        super.onPause();
        Log.i(TAG, "onPause()");
    }

    @Override
    protected void onStop() {
        super.onStop();
        Log.i(TAG, "onStop()");
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        Log.i(TAG, "onDestroy()");
    }
}

```

输出实验结果如下
```
从onCreate走进来
2019-04-17 07:02:02.480 15510-15510/com.example.viewlife I/MyMainActivity: onCreate()1
2019-04-17 07:02:02.544 15510-15510/com.example.viewlife I/MyTestView: MyTestView(Context context, @Nullable AttributeSet attrs)
2019-04-17 07:02:02.544 15510-15510/com.example.viewlife I/MyTestView: onFinishInflate
2019-04-17 07:02:02.544 15510-15510/com.example.viewlife I/MyMainActivity: onCreate()2
2019-04-17 07:02:02.546 15510-15510/com.example.viewlife I/MyMainActivity: onStart()
2019-04-17 07:02:02.548 15510-15510/com.example.viewlife I/MyMainActivity: onResume()
2019-04-17 07:02:02.586 15510-15510/com.example.viewlife I/MyTestView: onAttachedToWindow
2019-04-17 07:02:02.586 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:02:02.595 15510-15510/com.example.viewlife I/MyTestView: onMeasure()
2019-04-17 07:02:02.615 15510-15510/com.example.viewlife I/MyTestView: onMeasure()
2019-04-17 07:02:02.616 15510-15510/com.example.viewlife I/MyTestView: onMeasure()
2019-04-17 07:02:02.619 15510-15510/com.example.viewlife I/MyTestView: onSizeChanged
2019-04-17 07:02:02.619 15510-15510/com.example.viewlife I/MyTestView: onLayout
2019-04-17 07:02:02.633 15510-15510/com.example.viewlife I/MyTestView: onWindowFocusChanged
2019-04-17 07:02:02.640 15510-15510/com.example.viewlife I/MyTestView: onDraw

自然灭屏
2019-04-17 07:02:32.242 15510-15510/com.example.viewlife I/MyMainActivity: onPause()
2019-04-17 07:02:32.280 15510-15510/com.example.viewlife I/MyMainActivity: onStop()
2019-04-17 07:02:37.599 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:02:37.634 15510-15510/com.example.viewlife I/MyTestView: onWindowFocusChanged

亮屏
2019-04-17 07:03:22.070 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:03:22.096 15510-15510/com.example.viewlife I/MyMainActivity: onRestart()
2019-04-17 07:03:22.098 15510-15510/com.example.viewlife I/MyMainActivity: onStart()
2019-04-17 07:03:22.100 15510-15510/com.example.viewlife I/MyMainActivity: onResume()
2019-04-17 07:03:22.117 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:03:22.145 15510-15510/com.example.viewlife I/MyTestView: onDraw
2019-04-17 07:03:22.163 15510-15510/com.example.viewlife I/MyTestView: onWindowFocusChanged

按下home
2019-04-17 07:03:54.656 15510-15510/com.example.viewlife I/MyMainActivity: onPause()
2019-04-17 07:03:54.723 15510-15510/com.example.viewlife I/MyTestView: onWindowFocusChanged
2019-04-17 07:03:54.790 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:03:55.032 15510-15510/com.example.viewlife I/MyMainActivity: onStop()

又回来
2019-04-17 07:04:38.090 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:04:38.104 15510-15510/com.example.viewlife I/MyMainActivity: onRestart()
2019-04-17 07:04:38.120 15510-15510/com.example.viewlife I/MyMainActivity: onStart()
2019-04-17 07:04:38.120 15510-15510/com.example.viewlife I/MyMainActivity: onResume()
2019-04-17 07:04:38.123 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:04:38.140 15510-15510/com.example.viewlife I/MyTestView: onDraw
2019-04-17 07:04:38.155 15510-15510/com.example.viewlife I/MyTestView: onWindowFocusChanged

按下back键
2019-04-17 07:19:41.524 15510-15510/com.example.viewlife I/MyMainActivity: onPause()
2019-04-17 07:19:41.645 15510-15510/com.example.viewlife I/MyTestView: onWindowFocusChanged
2019-04-17 07:19:41.718 15510-15510/com.example.viewlife I/MyTestView: onWindowVisibilityChanged
2019-04-17 07:19:41.963 15510-15510/com.example.viewlife I/MyMainActivity: onStop()
2019-04-17 07:19:41.965 15510-15510/com.example.viewlife I/MyMainActivity: onDestroy()
2019-04-17 07:19:41.966 15510-15510/com.example.viewlife I/MyTestView: onDetachedFromWindow
```
