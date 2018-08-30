## 初始化模块

```java 
/**
     * @param data {Bundle} 由Module容器传入的参数或前一个页面传入的参数
     * @example Object object = data.get("key");
     */
    @Override
    public void initData(Bundle data) {
		
		}
```


## 获取H5加载地址

可以直接通过 设置H5地址来决定加载内容

示例代码如下：
```java 
public String getWebUrl() {
        //初始化路由参数
        Bundle arguments = getArguments();
        if (arguments != null) {
            mAppType = arguments.getString(BCLLockConstants.APP_TYPE);
            mBaseUrl = arguments.getString(BCLLockConstants.BASEURL);
        }
        String url = null;
        if (com.linkstec.blockchains.bcllock.BuildConfig.BUILD_REMOTE) {
            url = com.linkstec.blockchains.bcllock.BuildConfig.BUILD_WEB_URL;
        } else {
            url = "file:///android_asset/www-bcllock/index.html";
        }
        if (!TextUtils.isEmpty(mAppType)) {
            if (url.contains("?")) {
                url = url + "&appType=" + mAppType;
            } else {
                url = url + "?appType=" + mAppType;
            }
        }
        if (!TextUtils.isEmpty(mBaseUrl)) {
            if (url.contains("?")) {
                url = url + "&baseurl=" + mBaseUrl;
            } else {
                url = url + "?baseurl=" + mBaseUrl;
            }
        }
        return url;
    }
```

## 自定义和Js交互的类


如果想自定义和js的加护, 只需要在方法`getWebJavaInterfaces`中返回自定义类 即可

```java
   /**
     * 自定义方法
     *
     * @return
     */
    public Object getWebJavaInterfaces() {
        return new CustomerJavaInterfaces();
    }

```

 
