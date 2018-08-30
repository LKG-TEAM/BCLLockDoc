## 消息推送

> app消息推送 使用了 友盟的推送框架

## 友盟推送使用

> 友盟推送 在Application中注册

```java 
        /**
         * 初始化common库
         * 参数1:上下文，不能为空
         * 参数2:设备类型，UMConfigure.DEVICE_TYPE_PHONE为手机、UMConfigure.DEVICE_TYPE_BOX为盒子，默认为手机
         * 参数3:Push推送业务的secret
         */
        //     UMConfigure.init(this, UMConfigure.DEVICE_TYPE_PHONE, "1fe6a20054bcef865eeb0991ee84525b");
        UMConfigure.init(this, UMConfigure.DEVICE_TYPE_PHONE, null);
        PushAgent mPushAgent = PushAgent.getInstance(this);
        //若要不显示前台通知，调用接口如下：
        // mPushAgent.setNotificaitonOnForeground(false);
        //注册推送服务，每次调用register方法都会回调该接口
        mPushAgent.register(new IUmengRegisterCallback() {

            @Override
            public void onSuccess(String deviceToken) {
                Log.e("deviceToken", deviceToken);
                //注册成功会返回device token An6A7WVRaN5LyA0qd-WU6HHVTN03fOyGUFD6DryCo4IW
                SharePreUtil.putString("deviceToken", getApplicationContext(), "deviceToken", deviceToken);
            }

            @Override
            public void onFailure(String s, String s1) {

            }
        });

     
  
```

> 友盟推送设置

```java
   // 设置通知栏显示条数
        mPushAgent.setDisplayNotificationNumber(2);
        // 自定义消息处理
        // mPushAgent.setPushIntentServiceClass(MyPushIntentService.class);
        // mPushAgent.setPushIntentServiceClass(null);

    
        mPushAgent.setNotificationPlaySound(MsgConstant.NOTIFICATION_PLAY_SERVER); //声音
        mPushAgent.setNotificationPlayLights(MsgConstant.NOTIFICATION_PLAY_SERVER);//呼吸灯
        mPushAgent.setNotificationPlayVibrate(MsgConstant.NOTIFICATION_PLAY_SERVER);//振动
```

>友盟推送 消息栏点击相应

```java
    UmengNotificationClickHandler notificationClickHandler = new UmengNotificationClickHandler() {
            @Override
            public void dealWithCustomAction(Context context, UMessage msg) {
                ActivityStack.getInstance().navigateTo(null, "file:///android_asset/www-bcllock/index.html?isNoticeList=true", null, -1);
            }
        };
    mPushAgent.setNotificationClickHandler(notificationClickHandler);

```