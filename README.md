# twilio-1.2.14-packaging-test

## Problem

Twilio library v1.2.14 clashes with the commons-codec package. 

To reproduce, try to compile the project. It has both Twilio 1.2.14 and commons-codec 1.10 as a dependency (see `app/build.gradle`):

```groovy
compile 'com.twilio:client-android:1.2.14'
compile 'commons-codec:commons-codec:1.10'
```

The compilation will fail with the following error:

```
Error:Error converting bytecode to dex:
Cause: com.android.dex.DexException: Multiple dex files define Lorg/apache/commons/codec/Decoder;
```

And the error is due to `org.apache.http.legacy.jar` included in the Twilio client `.aar` which contains classes from `commons-codec`.
