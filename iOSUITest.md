# iOS UI Test

## SwiftMonkey
https://github.com/wayne-lab/quick-news/blob/master/Podfile
Podfile configuration
```ruby
# Uncomment the next line to define a global platform for your project
 platform :ios, '10.0'

use_frameworks!
inhibit_all_warnings!
MonkeyTest = 'MonkeyTest'

target 'QuickNews' do
  pod "SwiftMonkeyPaws", '~> 2.1.0', :configurations => ['MonkeyTest']
end

target 'QuickNewsMonkeyTests' do
#  inherit! :search_paths
  pod 'SwiftMonkey', '~> 2.1.0'
end

# create a "MonkeyTest" config in our pods based on the standard "Debug" target
project 'QuickNews', MonkeyTest => :debug

post_install do |installer|
  installer.pods_project.targets.each do |target|
    
    target.build_configurations.each do |config|
      config.build_settings['ENABLE_BITCODE'] = 'YES' #For now all targets must have bitcode disabled :-(
      config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
      config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
      config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
      config.build_settings['SWIFT_VERSION'] = '4.2'

      if target.name == 'Pods-QuickNews'
        target.build_configurations.each do |config|
          if config.name == MonkeyTest
            config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] = [
              '$(inherited)',
              'Monkey=1'
            ]
            config.build_settings['OTHER_SWIFT_FLAGS'] = [
              '$(inherited)',
              '-D MonkeyTest'
            ]
          end
        end
      end
    end
  end
  
  app_project = Xcodeproj::Project.open(Dir.glob("*.xcodeproj")[0])
  app_project.native_targets.each do |target|
    if target.name == 'QuickNews'
      target.build_configurations.each do |config|
        if config.name == MonkeyTest
          config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] = [
            '$(inherited)',
            'Monkey=1'
          ]
          config.build_settings['OTHER_SWIFT_FLAGS'] = [
            '$(inherited)',
            '-D MonkeyTest'
          ]
        end
      end
    end
  end
  app_project.save
end
```

------------
以下內容參考此篇[文章](https://www.bignerdranch.com/blog/ui-testing-in-xcode-7-part-1-ui-testing-gotchas/)，並列出重點部分

Concept of UI tests
UI test exists outside of App, interact with app by proxy elements.
Those proxies represents UI elements in App.
e.g. XCUIElement type -> UIButton
Attributes of objects whitch represented by XCUIElement not identical to the exact UI object.
e.g. UIElement button have title attribute but doesn't have title color attribute.
Interect API is restricted.
e.g. Interect API tap or double-tap.

Queries
利用queries來導航結構樹並取得elements
UI element type適用enumeration(XCUIElementType)來表示,像是StaticText而不是classes如UILabel.
Common types可以利用存取運算子來取得全部的tables而不必人工建立一個query如descendantsMatchingType
有一點要注意的是element types沒有分平台, 因此你會同時看到iOS的.Cell及OS X的.TableRow及.TableColumn

Simulated Events
取得element後利用tap或doubleTap等來模擬操作

以移動專案為例:

```
- (void)testExample {
    XCUIApplication *cuiApplication = [[XCUIApplication alloc] init];
//    XCUIElementQuery *tabBarsQuery = cuiApplication.tabBars;
    XCUIElementQuery *tablesQuery = cuiApplication.tables;
    XCUIElementQuery *otherElementsQuery = cuiApplication.otherElements;
    XCUIElementQuery *navigationBarsQuery = cuiApplication.navigationBars;
    XCUIElementQuery *searchFields = cuiApplication.searchFields;
//    XCUIElementQuery *tabBarButtonsQuery = tabBarsQuery.buttons;
//    XCUIElement *portfolioButton = tabBarButtonsQuery["自选"];
//    [portfolioButton tap];
    XCUIElement *otherElement = otherElementsQuery.staticTexts["自选股"];
    [otherElement tap];
    for (int i=0; i < 2; i++) {
        XCUIElement *cell = tablesQuery.staticTexts["浦发银行"];
        [cell tap];
        [navigationBarsQuery["SynthesizeQuote"].buttons["返回"] tap];
    }
    [navigationBarsQuery["自选股中心"].buttons["Search"] tap];
    XCUIElement *searchField = searchFields["请输入代码或名称"];
    [searchField tap];
    [searchField typeText:"600000"];
    [[NSRunLoop currentRunLoop] runMode:NSDefaultRunLoopMode beforeDate:[NSDate dateWithTimeIntervalSinceNow:3.]];
    __weak XCTestExpectation *expectation = [self expectationWithDescription:"no cells"];
    XCUIElementQuery *cellsQuery = tablesQuery.cells;
    if ([cellsQuery count]) {
        XCUIElement *cell = [cellsQuery elementBoundByIndex:[cellsQuery count]-1];
        [cell tap];
        [expectation fulfill];
    }
    [self waitForExpectationsWithTimeout:.0 handler:^(NSError * _Nullable error) {
    }];
    XCUIElementQuery *segmentedControlsQuery = cuiApplication.segmentedControls;
    XCUIElement *segmentedControl = [segmentedControlsQuery elementBoundByIndex:0];
    for (int i=0; i<10; i++) {
        [segmentedControl.staticTexts["五日"] tap];
        [segmentedControl.staticTexts["分时"] tap];
      }
   }
```



