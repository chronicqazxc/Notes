# Jenkins

```
iOS jenkins CI Code Sign error: No matching provisioning profile found

1.Ensure the project is building successfully from Xcode to real target.

-In KeyChain
2. Copy all the development cretificates & credentials form your user folder to the system folder

3.Copy all the Provisioning profiles existing in
~/Library/MobileDevice/Provisioning Profiles
to
Jenkins/Library/MobileDevice/Provisioning Profiles

sudo chown -R admin:staff xxx
```

Inject environment variables to the build process:

```batch
DEVELOPER_DIR=/Applications/Xcode7.3.app/Contents/Developer
```

Inject passwords to the build as environment variables:  
  ....

# Build with xcodebuilder:

Build & Archive

```bash
#BUILD & ARCHIVE
/usr/bin/xcodebuild -scheme XXX \
                    -workspace "${WORKSPACE}/XXX.xcworkspace" \
                    -configuration $CONFIGURATION \
                    -derivedDataPath "${WORKSPACE}/DerivedData" \
                    archive -archivePath ${WORKSPACE}/$ARCHIVEPATH \
                    CODE_SIGN_IDENTITY="${CODESIGN}" \
                    PROVISIONING_PROFILE_SPECIFIER=$PROVISIONING | /usr/local/bin/xcpretty -sc
```

Export

```batch
/usr/bin/xcodebuild -exportArchive \
                    -archivePath ${PWD}/${ARCHIVEPATH} \
                    -exportOptionsPlist ${exportOptionsPlist} \
                    -exportPath ${PWD}/${EXPORTPATH}
```

ExportOptions.plist

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>compileBitcode</key>
    <false/>
    <key>method</key>
    <string>enterprise</string>
    <key>provisioningProfiles</key>
    <dict>
        <key>com.xxx.xxx</key>
        <string>ProvisionName</string>
    </dict>
    <key>signingCertificate</key>
    <string>iPhone Distribution</string>
    <key>signingStyle</key>
    <string>manual</string>
    <key>stripSwiftSymbols</key>
    <true/>
    <key>teamID</key>
    <string>XXX</string>
    <key>thinning</key>
    <string>&lt;thin-for-all-variants&gt;</string>
</dict>
</plist>
```

Building issues:

* [IDEDistributionErrorDomain Code=1 error and Fastlane](http://ajmccall.com/idedistributionerrordomain-code-1-error-and-fastlane/)
* [Clear CocoaPods cache, re-download and re-install all pods](https://gist.github.com/mbinna/4202236)
* [git: error: unable to find utility "git", not a developer tool or in PATH Creating shallow clone of spec repo `master-1` from https://github.com/CocoaPods/Specs.git](https://github.com/CocoaPods/CocoaPods/issues/3631)

Build with parameters from GitHub:
* [https://stackoverflow.com/a/31572888](https://stackoverflow.com/a/31572888)

## PR Build

### Github![](/assets/github_1.png)![](/assets/github_2.png)

### Jenkins

![](/assets/jenkins_1.png)![](/assets/jenkins_2.png)![](/assets/jenkins_3.png)![](/assets/jenkins_4.png)![](/assets/jenkins_5.png)

### GitHub OAuth App
https://wiki.jenkins.io/display/JENKINS/GitHub+OAuth+Plugin  

|GitHub|Jenkins|
|--|--|
|![](/assets/jenkins/oauth_setting_github.png)|![](/assets/jenkins/oauth_setting_jenkins.png)|  
