---
layout: post
category : android
tags : [android, makefile]
---

# Best Guide:
* http://www.ibm.com/developerworks/cn/opensource/os-cn-android-build/
* [Understanding of Android Build system](http://www.programering.com/a/MDN5EDNwATM.html)
* [深入浅出Android makefile](http://blog.csdn.net/memechashang/article/details/23428841)
* http://blog.csdn.net/zhangchiytu/article/details/6424910
* http://android.mk/
* http://www.kandroid.org/ndk/docs/ANDROID-MK.html

# Add your applications into products

1. Need add it to PRODUCT_PACKAGES, otherwise it won't be built to final product.
2. Need define the application's Android.mk under TOP, so it can be scaned by build system.

If you don't want your application to be built into final product, then just remove it from PRODUCT_PACKAGES.

# Add Prebuilts

here is a good reference http://blog.csdn.net/jscese/article/details/40615801.

1. Use PRODUCT_COPY_FILES, "+= src:dst". Copy file only, can't execute any
   script. So the source file can't get any dependencies.
2. Use BUILD_PREBUILT
3. Use BUILD_MULTI_PREBUILT, only support known types.
4. use add-prebuilt-files. do as bellow: "$(call add-prebuilt-files, class, filename)"

   here, the class can be any of: ETC, APPS, EXECUTABLES, SHARED_LIBRARIES, STATIC_LIBRARIES

## BUILD_MULTI_PREBUILT

When use BUILD_MULTI_PREBUILT, multiple LOCAL_MODULE will be created, and each
module name is the basename of each LOCAL_SRC_FILES.

See build/core/multi_prebuilt.mk

Say

```makefile
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
LOCAL_SRC_FILES := out/libA.so out/libB.so
LOCAL_MODULE_PATH := $(TARGET_OUT_VENDOR_SHARED_LIBRARIES)
include $(BUILD_MULTI_PREBUILT)
```

* http://www.phonesdevelopers.com/1724715/


# Others

* [Android源码下载与编译全过程](http://blog.csdn.net/fengliang191/article/details/40679793)
* [深入分析Android (build/core/*.mk脚本)](http://blog.csdn.net/wh_19910525/article/details/7519919)
