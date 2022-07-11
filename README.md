# expo-ads-admob

> Source code for the deprecated expo-ads-admob package. This module is removed from Expo SDK in SDK 46. There will be no replacement that works with the classic build service (`expo build`) because [the classic build service has been superseded by **EAS Build**](https://blog.expo.dev/turtle-goes-out-to-sea-d334db2a6b60). With **EAS Build** and [Development Builds](/development/introduction.md), you should use [react-native-google-mobile-ads](https://github.com/invertase/react-native-google-mobile-ads) instead.

Provides support for the Google AdMob SDK (https://www.google.com/admob/) for mobile advertising. This module is largely based of the react-native-admob (https://github.com/sbugert/react-native-admob) module, as the documentation and questions surrounding that module may prove helpful. A simple example implementing AdMob SDK can be found at https://github.com/deadcoder0904/expo-google-admob.

# Installation in bare React Native projects

For bare React Native projects, you must ensure that you have [installed and configured the `expo` package](https://docs.expo.dev/bare/installing-expo-modules/) before continuing.

### Add the package to your npm dependencies

```
expo install expo-ads-admob
```

### Configure for iOS

Run `npx pod-install` after installing the npm package.

In your app's `Info.plist` file, add a `GADApplicationIdentifier` key with a string value of your AdMob app ID, as shown in Google's [Mobile Ads SDK iOS docs](https://developers.google.com/admob/ios/quick-start#update_your_infoplist).

```xml
<key>GADApplicationIdentifier</key>
<string>ca-app-pub-3940256099942544~1458002511</string>
```

Add `NSUserTrackingUsageDescription` key to your `Info.plist`:

```xml
<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized ads to you.</string>
```

Add the required `SKAdNetworkIdentifier` items to your `Info.plist`: [Google SKAdNetwork](https://developers.google.com/admob/ios/ios14#skadnetwork).

### Configure for Android

Ensure that there is a `meta-data` element inside the `application` node inside `AndroidManifest.xml` file (located typically under `/android/app/src/main/AndroidManifest.xml`) with `android:name` of `"com.google.android.gms.ads.APPLICATION_ID"` and a value of your AdMob App ID. Google's Mobile Ads SDK documentation shows precisely how to do this [here](https://developers.google.com/admob/android/quick-start#update_your_androidmanifestxml). In the end your `AndroidManifest.xml` should look more or less like this:

```xml
<manifest>
  <application>
    ...
    <!-- Ensure that tag with this name and proper value is inside application -->
    <meta-data
      android:name="com.google.android.gms.ads.APPLICATION_ID"
      android:value="ca-app-pub-xxxxxxxxxxxxxxxx~yyyyyyyyyy"/> <!-- App ID -->
    <!-- You can find your App ID in the AdMob UI -->
    ...
  </application>
</manifest>
```

This package automatically adds the `INTERNET` permission. It's required to interact with Google's service.

```xml
<manifest>
  <!-- Added permissions -->
  <uses-permission android:name="android.permission.INTERNET" />
</manifest>
```