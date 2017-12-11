---
layout: post
title:  "TransitDB no longer on BlackBerry App World"
categories: Android, TransitDB
---

I've removed TransitDB from BlackBerry App World.
I didn't plan for this change, as it was an unforeseen consequence of my recent effort to 
modernize some internal components of the TransitDB app.
The issue is that the [BlackBerry's APK Packager](https://developer.blackberry.com/android/documentation/rpkg_with_apk_pkgr_tool.html),
which converts Android apps into BlackBerry's required format, doesn't work if the Android app uses some newer Android features.
A fix on BlackBerry's end is unlikely, and there's still 
[Amazon Appstore](https://www.amazon.ca/Carson-Lam-TransitDB-Vancouver/dp/B00RYZVCOW) as an alternative for BlackBerry users.

In particular, the problem appears to be the use of 
[Adaptive Launcher Icons](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive.html),
introduced in Android 8.0 Oreo. The APK Packager tool fails with the following log output:

```
(res/mipmap-anydpi-v26/ic_launcher.xml) icon could not be verified:impact=1
(null) icon too small:impact=2
(res/mipmap-anydpi-v26/ic_launcher.xml) no suitable icon found:impact=4
(AndroidManifest.xml) minSdkVersion: 15 is higher than 10: required minimal BlackBerry OS version = 10.2:impact=5
(AndroidManifest.xml) targetSdkVersion: 27 is higher than 18:impact=1
[ERROR] Error while reading icon: ic_launcher.xml
Summary: [5]=2; [4]=1; [3]=0; [2]=1; [1]=2;
Impact Legend: [5]=Severe; [4]=High /context; [3]=Medium /context; [2]=Medium-low /context; [1]=Minor;
```

For compatibility with older versions of Android, the use of Adaptive Icons includes PNG fallback versions.
However, it appears that the APK Packager isn't picking them up.
[BlackBerry's Android developer tools](https://developer.blackberry.com/android/tools/)
were last updated in 2014, so a fix is unlikely.

This means I'm no longer able to convert TransitDB into the BAR format required by BlackBerry App World -
at least without holding back adoption of new features in Android, which I'm reluctant to do.
Therefore, I've removed TransitDB from BlackBerry App World.
TransitDB will still be available to BlackBerry users through the 
[Amazon Appstore](https://www.amazon.ca/Carson-Lam-TransitDB-Vancouver/dp/B00RYZVCOW).
BlackBerry OS now includes Amazon Appstore anyway, so I don't expect this to have any real consequence to users.

Dropping the BAR packaging step also makes the build process much simpler by eliminating some concerns:

* BlackBerry BAR signing token annual expiry and renewal
* BlackBerry signing server uptime (it's gone down for days at a time this year)
* The 4-part A.B.C.D TransitDB app version names required by BlackBerry's signing server
* The signing server's requirement that once a version name has been used for one signature, it can't be used again
* Re-signing APKs with a specific JDK8 `jarsigner` invocation to support very old versions of Android, and BlackBerry BARs
