## 蓝牙权限申请

安卓手机需要开启权限才能启用蓝牙

```java
    PermissionManager.requestBluetoothPermission(BCLLockWebModule.this, getString(R.string.bluetooth_rationale));
```

### 权限回调

>用户同意了权限申请

```java
  @PermissionGranted(requestCode = PermissionManager.REQUEST_BLUETOOTH)
    public void bluetoothPermissionGranted() { 
        startScanDevice();
    }
```

>权限申请失败

```java
  @PermissionDenied(requestCode = PermissionManager.REQUEST_BLUETOOTH)
    public void bluetoothPermissionDenied() {
       
    }
```


## 蓝牙扫描

>初始化蓝牙扫描类

```java

mBLEScanner = new BLEScanner(getActivity(), mBleScanObserver);
```

>添加要扫描的设备地址开始扫描

```java
mBLEScanner.clean();
        //115802A00240   ==>   11:58:02:A0:02:40
mBLEScanner.addTarget(new BLETarget(null, mCurrentMac, ITargetTransformer.DEFAULT));
mBLEScanner.startScan();
```

>停止扫描

```java
mBLEScanner.stopScan(false);
```

>蓝牙扫描回调

```java
IBLEScanObserver mBleScanObserver = new IBLEScanObserver() {
        @Override
        public void onScanStarted() {
        }

        @Override
        public void onScanStopped() {// stopScan(true) 的时候才会走这里
   
        }

        @Override
        public void onBLEUnsupported() {

        }

        @Override
        public void onBLEDisabled() {//蓝牙关闭 去打开
            Intent enableIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
            startActivityForResult(enableIntent, REQUEST_ENABLE_BT);
        }

        @Override
        public void onScanTimeout() {

        }

        @Override
        public void onDeviceFound(BluetoothDevice btDevice) {//找到目标锁具
            
        }
    };
```


## 蓝牙设备连接和管理

>初始化设备操作类

```java
mCurrentBleDeviceInstance = new SmartLockDevice(getActivity(), btDevice);
```

>设置自动重连

```java
mCurrentBleDeviceInstance.setAutoReconnect(true,5);//设置自动重连
```

>开始连接

```java
mCurrentBleDeviceInstance.startConnect(new IDeviceConnectListener() {
                    @Override
                    public void onError(final int errorCode) {
                        

                    }

                    @Override
                    public void onConnectStatus(final int status) {
                        
                    }

                    @Override
                    public void onCommandResult(final String tag, final Object response) {
                        

                    }
                });

```

>断开连接

```java
  mCurrentBleDeviceInstance.close(false);
```

>发送指令

指令可能有好多种，发送格式都一样，如下：

```java

 SmartLockCommand.sendUnlock(pwd, mCurrentBleDeviceInstance, "sendUnlock");
```