# Vector drawables backward compatibility solution

Vector drawable was introduced to Android from 5.0 (API level 21), Today I learned that for Android Version lower than 5.0, to support backward compatibility of vector drawable, there are two solutions

|  Tech   | Note  | Deawback
|  ----  | ----  | ----  |
| PNG generation  | generate png on build time | 1. some vector drawable element not supported <br> 2. larger apk size <br>|
| Support Library  | render the vector drawable using support lib in runtime | can be only used in ImageView via app:srcCompat or setImageResource ( if used in places like launcher icons, can not be displaced as there is no vector drawable or png generated)|

## Using PNG generation

if the minSdkVersion < 21, then the png generation will be automatically used (introduced in Android Studio 1.4)

## Enable Support Library support

``` groovy
 // Gradle Plugin 2.0+  
 android {  
   defaultConfig {  
     vectorDrawables.useSupportLibrary = true  // this will disable build time png generation 
    }  
 }  
```

then in ImageView, the `android:src` should be replaced by `app:srcCompat`, and the drawable should not be used in places outside ImageView