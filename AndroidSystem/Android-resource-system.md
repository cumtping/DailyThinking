[What is the 'app' Android XML namespace?](https://stackoverflow.com/questions/26692233/what-is-the-app-android-xml-namespace)
```
<menu xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
```


The app namespace is not specific to a library, but it is used for all attributes defined in your app, whether by your code or
by libraries you import, effectively making a single global namespace for custom attributes - i.e., attributes not defined by the android system.

In this case, the appcompat-v7 library uses custom attributes mirroring the android: namespace ones to support prior versions
of android (for example: android:showAsAction was only added in API11, but app:showAsAction 
(being provided as part of your application) works on all API levels your app does) - obviously using the android:showAsAction 
wouldn't work on API levels where that attribute is not defined.



