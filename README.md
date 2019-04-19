This project can be built inside xcode 10.2 (or 10.2.1) but cannot be built via the command line using xcodebuild, through fastlane.

In order to reproduce the problem:
1. enter the `Example` folder and run `bundle install && pod install`
2. Open `example.xcworkspace` in Xcode
3. Build the `Example` scheme. It should build perfectly
4. Now at the terminal, go to the `Example` folder
5. run `bundle exec fastlane build_ios`. If the build runs perfectly, try executing the same comand again.

You'll notice that the build logs:
```
19:27:15]: ▸ Processing Clappr-tvOS-Info.plist
[19:27:15]: ▸ TARGETED_DEVICE_FAMILY value (3) does not contain any device family values compatible with the iOS platform. Please add one or more of the following values to the TARGETED_DEVICE_FAMILY build setting to indicate the device families supported by this target: '1' (indicating 'iphone'), '2' (indicating 'ipad').
```

xcodebuild will try to process `Clappr-tvOS-Info.plist`, which it is not supposed to do, as it is this is an iOS build, and the plist refers to a tvOS bundle. The warning log also indicates that. The build will fail as other resources are not present in iphoneos.

