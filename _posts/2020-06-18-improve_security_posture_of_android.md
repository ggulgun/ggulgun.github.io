---
title: "Improve Android Application Security Posture as a Bug Bounty Hunter"
layout: post
---

# Introduction
2020-06-18 
<br />

When testing Android applications, it is recommended to use a rooted device to perform the assessment efficiently and thoroughly. However, some applications have an additional layer of protection, which prevents an application from running on a rooted device. 
<br />

## Methodology:

For better protection, Anti Hooking, Anti Root and SSL Pinning mechanisms must implemented together. Native (JNI) C/C++ and Java/Kotlin protections must be developed together.

- Anti Root Native Solution
- Anti Frida Implementation
- Anti Hook Implementation
- Native SSL Pinning Implementation

### Anti Root Native Solution

 (JNI based) C/C++ level protections are better than Java based detection. In the methods, you can easily see they detects multiple parameters. checkRootAccessMethod3 is used for natively test-keys detection.

{% highlight c %}
#include <string.h>
#include <jni.h>
#include <time.h>
#include <sys/stat.h>
#include <stdio.h>
#include "android_log.h"
#include <errno.h>
#include <unistd.h>
#include <sys/system_properties.h>

JNIEXPORT int JNICALL Java_com_test_RootUtils_checkRootAccessMethod1(
        JNIEnv* env, jobject thiz) {


    //Access function checks whether a particular file can be accessed
    int result = access("/system/app/Superuser.apk",F_OK);

    ANDROID_LOGV( "File Access Result %d\n", result);

    int len;
    char build_tags[PROP_VALUE_MAX]; // PROP_VALUE_MAX from <sys/system_properties.h>.
    len = __system_property_get(ANDROID_OS_BUILD_TAGS, build_tags); // On return, len will equal (int)strlen(model_id).
    if(strcmp(build_tags,"test-keys") == 0){
        ANDROID_LOGV( "Device has test keys\n", build_tags);
        result = 0;
    }
    ANDROID_LOGV( "File Access Result %s\n", build_tags);
    return result;

}

JNIEXPORT int JNICALL Java_com_test_RootUtils_checkRootAccessMethod2(
        JNIEnv* env, jobject thiz) {
    //which command is enabled only after Busy box is installed on a rooted device
    //Outpput of which command is the path to su file. On a non rooted device , we will get a null/ empty path
    //char* cmd = const_cast<char *>"which su";
    FILE* pipe = popen("which su", "r");
    if (!pipe) return -1;
    char buffer[128];
    std::string resultCmd = "";
    while(!feof(pipe)) {
        if(fgets(buffer, 128, pipe) != NULL)
            resultCmd += buffer;
    }
    pclose(pipe);

    const char *cstr = resultCmd.c_str();
    int result = -1;
    if(cstr == NULL || (strlen(cstr) == 0)){
        ANDROID_LOGV( "Result of Which command is Null");
    }else{
        result = 0;
        ANDROID_LOGV( "Result of Which command %s\n", cstr);
        }
    return result;

}

JNIEXPORT int JNICALL Java_com_test_RootUtils_checkRootAccessMethod3(
        JNIEnv* env, jobject thiz) {


    int len;
    char build_tags[PROP_VALUE_MAX]; // PROP_VALUE_MAX from <sys/system_properties.h>.
    int result = -1;
    len = __system_property_get(ANDROID_OS_BUILD_TAGS, build_tags); // On return, len will equal (int)strlen(model_id).
    if(len >0 && strstr(build_tags,"test-keys") != NULL){
        ANDROID_LOGV( "Device has test keys\n", build_tags);
        result = 0;
    }

    return result;

}
{% endhighlight %}

With the above implementation, Also you can connect JNI code to Java.

{% highlight c %}
public boolean checkRooted() {

       if( rootUtils.checkRootAccessMethod3()  == 0 || rootUtils.checkRootAccessMethod1()  == 0 || rootUtils.checkRootAccessMethod2()  == 0 )
           return true;
      return false;
     }
{% endhighlight %}

### Anti Frida Implementation

Frida is usually used for bypassing an application Root Detection and SSL Pinning mechanisms.
Frida is binding sample port in the device. For detection following code piece can be used. (https://github.com/b-mueller/frida-detection-demo)
In the shared repository, Frida is detected via multiple methodology. You can see methodology from below.

{% highlight c %}
a) Detect presence of frida-agent, frida-gadget native library in /proc/<pid>/maps file which can be bypassed by changing the name of native library.

b) Scan the memory of native libraries for presence of certain strings or frida specific symbols as mentioned in this blog, but this can be eventually bypassed by recompiling the frida library after patching the frida specific artifacts.

c) Iterate through all the TCP open ports and pass D-Bus AUTH message to see if frida-server responds. This is effective approach as long as frida-server is used.When application is tampered to use frida-gadget then this mechanism is not useful.

d) Check for the presence of frida specific files in /data/local/tmp, which are quite trivial to bypass by renaming the frida specific files.

e) Check if the executable section of native library is writeable ( rwxp flag for the native library in /proc/<pid>/maps file) which is unlikely to happen on a normal device.
{% endhighlight %}

### Anti Hook Detection

For Anti-Hook implementation, The following blog post can be seen. https://d3adend.org/blog/posts/android-anti-hooking-techniques-in-java/.

{% highlight c %}
Stab 1: Check what is installed on the device.
Stab 2: Check the stack trace for suspicious method calls.
Stab 3: Check for native methods that shouldn’t be native.
Stab 4: Use /proc/[pid]/maps to detect suspicious shared objects or JARs loaded into memory.
{% endhighlight %}

### Native SSL Pinning Implementation

For implementation of Native (JNI) SSL Pinning, you can follow up the repository https://github.com/leenjewel/openssl_for_ios_and_android


## What's next
I'll probably do a part II on how to bypass all of this. 

[1]: https://github.com/b-mueller/frida-detection-demo
[2]: https://d3adend.org/blog/posts/android-anti-hooking-techniques-in-java/
[3]: https://github.com/leenjewel/openssl_for_ios_and_android

