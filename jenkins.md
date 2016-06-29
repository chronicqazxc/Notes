# Jenkins

    iOS jenkins CI Code Sign error: No matching provisioning profile found

    1.Ensure the project is building successfully from Xcode to real target.

    -In KeyChain
    2. Copy all the development cretificates & credentials form your user folder to the system folder

    3.Copy all the Provisioning profiles existing in
    ~/Library/MobileDevice/Provisioning Profiles
    to
    Jenkins/Library/MobileDevice/Provisioning Profiles

    sudo chown -R admin:staff xxx
    
Step1. 

Xcode plugin
![Xcode plugin](assets/jenkins/Screen_Shot_2015-12-20_at_18.45.09.png)
FTP plugin
![Xcode plugin](assets/jenkins/Screen_Shot_2015-12-20_at_21.44.49.png)
Step2. 

Generate Item
![Generate Item](assets/jenkins/Screen_Shot_2015-12-20_at_18.42.25.png)

Step3.

Setting
![Setting](assets/jenkins/Screen_Shot_2015-12-20_at_18.46.22.png)
![Setting](assets/jenkins/Screen_Shot_2015-12-20_at_18.38.41.png)
![Setting](assets/jenkins/Screen_Shot_2015-12-20_at_18.47.23.png)


Inject environment variables to the build process:
  DEVELOPER_DIR=/Applications/Xcode7.3.app/Contents/Developer
  
Inject passwords to the build as environment variables:
  ....
    
Build with xcodebuilder:
1. export LC_ALL="en_US.UTF-8"
   cd dlr && /usr/local/bin/pod update
2. # UNLICK KEYCHAIN
   security unlock -p $keychainPassword ~/Library/Keychains/login.keychain
3. INFOPLIST_FILE=${WORKSPACE}/${TARGET}/${PROJECT}-Info.plist
   export VERSION=`defaults read ${INFOPLIST_FILE} CFBundleShortVersionString`
   DATE=$(date +%Y-%m-%d)
   PROJECT="project_name"

    archivePath="build/${DATE}_${BUILD_NUMBER}/${PROJECT}_${VERSION}_${BUILD_NUMBER}.xcarchive"
    exportPath="build/${DATE}_${BUILD_NUMBER}"
    exportFile="${exportPath}/${PROJECT}_${VERSION}_${BUILD_NUMBER}.ipa"

  echo 'Building IPA for HockeyApp'
 
      /usr/bin/xcodebuild -scheme ${scheme} \
      -workspace "${WORKSPACE}/${PROJECT}.xcworkspace" \
      -derivedDataPath "${WORKSPACE}/DerivedData" \
      -configuration Prerelease clean build \
      archive -archivePath $PWD/$archivePath \
      CODE_SIGN_IDENTITY="iPhone Developer: XXXX"
        
     /usr/bin/xcodebuild -exportArchive \
     -archivePath ${PWD}/${archivePath} \
     -exportOptionsPlist "/Users/Shared/Jenkins/****/exportOptions.plist" \
     -exportPath ${PWD}/${exportFile}

    DSYM="${PWD}/${archivePath}/dSYMs/${PROJECT}.app.dSYM"
    /usr/bin/zip -r "${PWD}/${exportPath}/${PROJECT}.dSYM.zip" "${DSYM}"

  TODO:Upload ipa and dSYM to HockeyApp

Building issues:
* [IDEDistributionErrorDomain Code=1 error and Fastlane](http://ajmccall.com/idedistributionerrordomain-code-1-error-and-fastlane/)
* [Clear CocoaPods cache, re-download and re-install all pods](https://gist.github.com/mbinna/4202236)
