# Symbolicate

![](assets/symbolicate/backtrace1.jpg)  
![](assets/symbolicate/1918EDB3-F321-4E15-94DF-71D2E5DC7702.jpg)  
![](assets/symbolicate/55989D1E-84E3-4D10-8A82-C29984154988.jpg)  
![](assets/symbolicate/E40396B8-9B90-4A0B-8275-2C3148FBD6A7.jpg)  
![](assets/symbolicate/2015-11-02.jpg)

```
symbolicatecrash path
    Xcode6, Xcode7: /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/PrivateFrameworks/DTDeviceKit.framework/Versions/A/Resources/symbolicatecrash
    Xcode8: /Applications/Xcode.app/Contents/SharedFrameworks/DVTFoundation.framework/Versions/A/Resources/symbolicatecrash
copy symbolicatecrash, dSYM, crash to same directory
$ export DEVELOPER_DIR="/Applications/XCode.app/Contents/Developer" 
$ ./symbolicatecrash -v CrystalTouch.crash  CrystalTouch.app.dSYM
```

![](assets/symbolicate/backtrace2.jpg)

