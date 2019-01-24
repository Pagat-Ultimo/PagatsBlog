---
layout: post
title:  "Android permissions in Xamarin Forms"
date:   2019-01-24 14:31:00 +0100
categories: jekyll update
---

# The Concept
Be aware that the way how permission requesting worked, changed after Android version `5.1.1`. On a device which runs Android `5.1.1` or lower or if the app's `targetSdkVersion` is `22` or lower, all requested permissions will be granted through the installation process. To request a permission for your app you have to add the following to your AndroidManifest.xml

{% highlight xml %}
<manifest mlns:android="http://schemas.android.com/apk/res/android"
          package="com.razzil.permissiondemo">

    <uses-permission android:name="android.permission.SEND_SMS"/>

    <application ...>
        ...
    </application>
</manifest>
{% endhighlight %}

So this is quite simple. But this system isn't that transparent for the user. Many Organisation startet to just added a lot of unnecessary permission to der manifest and the user granted them all by installing the app. So Android changed and now, apps that are targeting a `targetSdkVersion` above `22` or running on a device with a higher version than `5.1.1` have to request `dangerous` permissions seperatly from their app code. For this versions permissions are catogorized into `normal` permissions which are granted on installation as they were before and `dangerous` permissions which have to be granted individually by the user.

# The Code
Let's take a look how we could an implementation for our Xamarin app. The example is based on an app using Xamarin Forms to be as usful for people who are working with Xamarin Forms and don't want to be.

