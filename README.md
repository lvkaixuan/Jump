Android利用悬浮窗轻松实现微信跳一跳辅助
-----------------------

![Alt text](https://github.com/lvkaixuan/Jump/blob/master/video.gif)
## 实现思路 ##

 - 透明悬浮窗
 - 手指滑动通过onTouch获取滑动的间距
 - 按比例计算出需要长按的时间
 - 使用shell命令模拟长按(需要ROOT权限)
## 主要代码 ##

```
@Override
public boolean onTouch(View v, MotionEvent event) {
    switch (event.getAction()) {
        case MotionEvent.ACTION_DOWN: //按下
            Log.d(TAG, "开始位置: " + event.getRawX() + " " + event.getRawY());
            mStartX = event.getRawX();
            mStartY = event.getRawY();
            break;
        case MotionEvent.ACTION_UP: //松开
            Log.d(TAG, "结束位置: " + event.getRawX() + " " + event.getRawY());
            float endX = event.getRawX();
            float endY = event.getRawY();
            //三角形边长1
            float length1 = Math.abs(endX - mStartX);
            //三角形边长2
            float length2 = Math.abs(endY - mStartY);
            //通过勾股定理计算间距
            int distance = 
                    (int) Math.sqrt(Math.pow(length1, 2) + Math.pow(length2, 2));
            Log.d(TAG, "距离: " + distance);
            int temp = (int) (distance * 1.44); //这里需要多尝试几次 找到最佳时间
            exec("input swipe 600 1800 600 1800 " + (temp) + "\n");
            break;
    }
    return true;
}
```
## 项目Demo ##

 - 项目源码: https://github.com/lvkaixuan/Jump
 - 项目Demo: http://fir.im/wechatjump
 
 - 也可以扫码下载:
![这里写图片描述](https://user-gold-cdn.xitu.io/2018/1/5/160c50c949629152?imageView2/0/w/1280/h/960/ignore-error/1)

## 感谢 ##

 - 如果该项目对你有帮助的话,请动动你可爱的小手点一下star
 
 - 这里感谢GitHub上的悬浮窗框架: https://github.com/yhaolpz/FloatWindow
