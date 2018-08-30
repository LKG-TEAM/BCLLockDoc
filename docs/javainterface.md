## natvie 和js交互
 
 可以通过自定义类`CustomerJavaInterfaces` 来实现, 该自定义类主要是通过提供接口给js调用来实现 js和native的通信
 
## js调用通用方法
 
 > 弹出Toast 
 
```java
@JavaInterface4JS("showToast")
public void showToast() {
   ToastUtil.normal("弹出toast");
}
```
 
 > 获取谷歌fcm token信息（推送使用）

```java
/**
 * @param commonCallback
 * @return
 * @method getFcmToken
 * @description 获取谷歌fcm token信息
 */
@JavaInterface4JS("getFcmToken")
public void getFcmToken(@ParamCallback BridgeJavaInterfaces.CommonCallback commonCallback) {

}
```


 > 获取通知栏信息


```java
/**
 * @param commonCallback
 * @method getNotificationInfo
 * @description 获取通知栏信息
 */
@JavaInterface4JS("getNotificationInfo")
public void getNotificationInfo(@ParamCallback BridgeJavaInterfaces.CommonJSONCallback commonCallback) {
          
}
```

 > 获取语言类型

```java
/**
 * <p>getLanguageType</p>
 *
 * @param commonCallback
 * @description 获取语言类型
 */
 @JavaInterface4JS("getLanguageType")
public void getLanguageType(@ParamCallback BridgeJavaInterfaces.CommonCallback commonCallback) {
            
}
```


 > 设置语言类型

```java
 /**
 * <p>setLanguageType</p>
 *
 * @param lgType
 * @description 设置语言类型
 */
@JavaInterface4JS("setLanguageType")
public void setLanguageType(@Param("lgType") String lgType) {
}
```


 > 获取未读信息条数

```java
/**
 * <p>getUnreadMessageData</p>
 *
 * @param commonCallback
 * @description 获取未读信息条数
 */
 @JavaInterface4JS("getUnreadMessageData")
public void getUnreadMessageData(@ParamCallback BridgeJavaInterfaces.CommonCallback commonCallback) {
           
}
```



 > 清除未读条数
 
```java
/**
 * <p>clearUnreadMessageData</p>
 *
 * @description 清除未读条数
 */
@JavaInterface4JS("clearUnreadMessageData")
public void clearUnreadMessageData() {
            
 }
```


 > 复制文字到剪贴板

```java
/**
 * @param text 要复制的文字
 * @description 将传入的文字复制到剪切板
 */
@JavaInterface4JS("copyToClipboard")
public void copyToClipboard(@Param("text") String text) {
          
}
```


## js调用蓝牙相关方法


 > 开始扫描蓝牙

```java
/**
 * 开始扫描蓝牙
 *
 * @param
 */
@JavaInterface4JS("beginScanBle") //DF:57:6A:06:46:37
 public void beginScanBle(@Param("mac") String mac, @Param("callbackId") final String callbackId) {
          
}
```



 > 连接蓝牙
 
```java
/**
 * 连接蓝牙
 *
 * @param address    蓝牙mac地址
 * @param callbackId
 */
@JavaInterface4JS("connectBle")
public void connectBle(@Param("address") String address, @Param("callbackId") final String callbackId) {
           
}
```


 > 断开蓝牙连接

```java
/**
 * 连接蓝牙
 * <p>
 * @param address    蓝牙mac地址
 * @param callbackId
 */
@JavaInterface4JS("disConnectBle")
public void disConnectBle(/*@Param("address") String address,*/ @Param("callbackId") final String callbackId) {

}
```


 > 蓝牙设备登录

```java

/**
 * 支持的协议
 *
 * @param adminPwd 管理员密码
 * @param
 */
@JavaInterface4JS("loginBle")
public void loginBle(@Param("adminPwd") String adminPwd, @Param("callbackId") final String callbackId) {
           
}
```


 > 发送协议指令

```java
/**
 * 支持的协议
 *
 * @param type 0 1 2  分别为
 *             0x0100：获取开锁方式类命令配置
 *             0x0101: 获取开关类配置
 *             0x0102: 可同步数据类配置
 * @param
 */
@JavaInterface4JS("sendSupportedProtocol")
public void sendSupportedProtocol(@Param("type") int type, @Param("callbackId") final String callbackId) {
           
}
```


 > 删除用户

```java
/**
 * 删除用户
 *
 * @param userId 用户id
 * @param
 */
@JavaInterface4JS("sendDelUser")
public void sendDelUser(@Param("userId") String userId, @Param("callbackId") final String callbackId) {
          
 }
```


 > 删除开锁方式

```java
/**
 * 删除开锁方式
 *
 * @param type 0密码，1指纹，2NFC，3钥匙
 * @param
 */
 @JavaInterface4JS("sendDelUnlockMode")
public void sendDelUnlockMode(@Param("type") int type, @Param("userId") String userId, @Param("callbackId") final String callbackId) {
        
}
```


 > 发送功能相关指令

```java
/**
 *  
 *
 * @param type 0 1 2 3 4 分别为
 *             读取开关提示语音状态
 *             读取配网功能状态
 *             读取距离传感器状态
 *             读取开关门判断状态
 *             读取电机控制状态
 * @param
 */
 @JavaInterface4JS("sendFunctionConfig")
public void sendFunctionConfig(@Param("type") int type, @Param("callbackId") final String callbackId) {
           
        }
```


 > 发送解锁指令

```java
/**
 * 解锁
 *
 * @param pwd 密码
 * @param
 */
 @JavaInterface4JS("sendUnlock")
public void sendUnlock(@Param("pwd") String pwd, @Param("callbackId") final String callbackId) {
        
        }
```


 > 添加密码，指纹，nfc，key

```java
/**
 * 添加密码，指纹，nfc，key
 * 传1为true，0为false
 *
 * @param
 * @param hasPwd         是否有密码，1为是，0为否
 * @param hasFingerprint 是否有Fingerprint，1为是，0为否
 * @param hasNFC         是否有NFC ，1为是，0为否
 * @param hasKey         是否有Key，1为是，0为否
 * @param flag           是否有用户id，1为现有用户，0为新增用户
 * @param userId         用户id，没有就传空
 * @param pwd            密码 只有hasPws为1才需要传，否则传空
 */
@JavaInterface4JS("sendAddPwdOrFingerprint")
public void sendAddPwdOrFingerprint(@Param("hasPwd") int hasPwd, @Param("hasFingerprint") int hasFingerprint, @Param("hasNFC") int hasNFC,
                                            @Param("hasKey") int hasKey, @Param("flag") int flag, @Param("userId") int userId,
                                            @Param("pwd") String pwd, @Param("callbackId") final String callbackId) {
     
        }
```


 > 获取zigbee地址

```java
/**
 * 获取zigbee地址
 */
@JavaInterface4JS("getZigbeeAddress")
public void getZigbeeAddress(@Param("callbackId") final String callbackId) {
     
        }
```



## 参数

- callbackId:      `String` | js回调接口id，当js调用了 类`CustomerJavaInterfaces`方法 且需要native给js  回调信息的时候 用于区分是哪个功能接口的回调
- commonCallback   `BridgeJavaInterfaces.CommonCallback` | js回调callback，直接调用commonCallback.callback() 方法给js回调信息

!>其他参数都是不固定参数 可以是各种js传给native的参数

## native回调


 > 同步回调信息给js
 
 ```java
  /**
     * 同步调用jsCallback
     *
     * @param callbackId
     * @param callbackContent
     */
    public void syncInvokeJsCallback(String callbackId, String callbackContent, boolean isStatus) {
        if (!TextUtils.isEmpty(callbackId) && !TextUtils.isEmpty(callbackContent)) {//有这个callbackId则通知js
            String jsonWrapper;
            if (callbackContent.contains("{")) {//自己就是json格式 就不加jsonWrapper了
                jsonWrapper = callbackContent;
            } else if (!isStatus) {//传输数据
                jsonWrapper = "{\"data\":\"" + callbackContent + "\"}";//似乎格式都是这样
            } else {//通知状态
                jsonWrapper = "{\"status\":\"" + callbackContent + "\"}";//似乎格式都是这样
            }

            Log.e("JsCallback", callbackId + "-->invokeJsCallback raw json:" + jsonWrapper);
            String base64Dat = Base64.encodeToString(jsonWrapper.getBytes(), Base64.DEFAULT);
            base64Dat = base64Dat.replace("\n", "");
//            Log.e("JsCallback", callbackId + "-->invokeJsCallback Base64:" + base64Dat);
            fetchSuccessCallback(base64Dat, callbackId, true);
        }
    }
 
 
 ```



 > 根据callbackId注册js异步回调

```java
/**
 * 注册js异步回调callbackId
 *
 * @param jsFunctionName
 * @param callbackId
 */
public void registerJsCallback(String jsFunctionName, final String callbackId) {
    if (TextUtils.isEmpty(jsFunctionName) || TextUtils.isEmpty(callbackId))
        return;

    mCallbackIdMap.put(jsFunctionName, callbackId);
}
```


 > 异步调用回调接口
 
 ```java
/**
 * 异步调用js回调通知js
 *
 * @param jsFunctionName
 * @param callbackContent
 */
public void asyncInvokeJsCallback(String jsFunctionName, String callbackContent, boolean isStatus) {
    if (TextUtils.isEmpty(jsFunctionName) || !mCallbackIdMap.containsKey(jsFunctionName)) {
        return;
    }
    String callbackId = mCallbackIdMap.get(jsFunctionName);
    syncInvokeJsCallback(callbackId, callbackContent, isStatus);
    mCallbackIdMap.remove(jsFunctionName);//用完一次就删除
}

 
 ```