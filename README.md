## Android UART 串口通信
先上图

![](images\android_send.png)

![android_talk](images\android_talk.png)

![pc-comm](images\pc-comm.png)

由于[android-serialport-api](https://github.com/cepr/android-serialport-api)项目中的so使用较old的ndk编译，所以在对于Android 6.0 以上版本兼容的时候会报错`dlopen failed: "has text relocations"`。且使用的mk进行编译，特升级为用cmake编译。

**`升级`**android-serialport-api

- ndk 17.0.4xxx jni编译
- cmake 编译链
- EClipse项目-> Android Studio项目

项目结构：

~~~bash
.
├── AndroidSerialLibrary.iml
├── androidserial
│   ├── CMakeLists.txt
│   ├── androidserial.iml
│   ├── build
│   ├── build.gradle
│   ├── libs
│   ├── proguard-rules.pro
│   └── src
├── app
│   ├── app.iml
│   ├── build
│   ├── build.gradle
│   ├── libs
│   ├── proguard-rules.pro
│   └── src
├── build
│   └── android-profile
├── build.gradle
├── gradle
│   └── wrapper
├── gradle.properties
├── gradlew
├── gradlew.bat
├── local.properties
└── settings.gradle
~~~

app对应原项目中的各个Activity， androidserial 是module 对应编译之前的so，还有API的封装。可以直接引用androidserial，调用方法参考app目录下的activity。

**`注意`**关于权限！

当接入开发板后如果发现 `Error You do not have read/write permission to the serial port `
**需要root 权限**，在开发者模式中开启root 权限 adb和应用  

使用一下命令开启Android对串口的读写权限

~~~bash
❯ adb shell   
 rk3399_firefly_mid:/ $ su  
 rk3399_firefly_mid:/ # chmod 777 /dev/ttyS4  
 rk3399_firefly_mid:/ # setenforce 0     
 rk3399_firefly_mid:/ # 
~~~

`setenforce 0`: 关闭防火墙，有人说关键是这不，但是我的环境不用关闭，只要给权限就可以  


**`注意`**关于ttyS1 - 6
ttyS1 - 6 对应的是 UART 串口1-6 一般都是一一对应的。这个具体要看一下开发板的说明。