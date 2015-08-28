# Getting Started #

You will first need to [download the Android SDK](http://developer.android.com/sdk/index.html), and checkout the source code from the project Mercurial repository.

# Building the project #

If you downloaded the Eclipse plugin for the Android SDK, you can create an Android project in Eclipse from the SoundCloudDroid folder.  You will need to add two external JAR files to the project:
  * commons-httpclient-3.1.jar from http://apache.mirrors.timporter.net/httpcomponents/commons-httpclient/binary/commons-httpclient-3.1.tar.gz
  * org.restlet.jar from http://www.restlet.org/downloads/2.0/restlet-android-2.0m5.zip

The project will not build successfully at first though - you will need to add an OAuth consumer key and consumer secret to your SoundCloudDroid project (the key and secret are not in the repository for security reasons).

To obtain a consumer key and secret, [register your build of SoundCloud Droid on SoundCloud](http://soundcloud.com/settings/applications/new).  Then create a file in the res/values folder of SoundCloudDroid, e.g. called consumer.xml, with contents:

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="consumer_key">YOUR_CONSUMER_KEY_HERE</string>
    <string name="s5rmEGv9Rw7iulickCZl">YOUR_CONSUMER_SECRET_HERE</string>
</resources>
```

If you want to use the app with the SoundCloud sandbox, then you should also register your build of the app on the SoundCloud sandbox to obtain another consumer key and secret to be used with the sandbox.  They should also be added to the resources file, e.g.:

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="consumer_key">YOUR_CONSUMER_KEY_HERE</string>
    <string name="s5rmEGv9Rw7iulickCZl">YOUR_CONSUMER_SECRET_HERE</string>
    <string name="sandbox_consumer_key">YOUR_SANDBOX_CONSUMER_KEY_HERE</string>
    <string name="sandbox_consumer_secret">YOUR_SANDBOX_CONSUMER_SECRET_HERE</string>
</resources>
```

To switch between operating on the regular SoundCloud site and the sandbox, change the following line of SoundCloudService.java:

```
    public final static boolean useSandbox = false;
```