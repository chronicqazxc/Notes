# iOS UI Test

以下內容參考此篇文章，並列出重點部分
[[https://www.bignerdranch.com/blog/ui-testing-in-xcode-7-part-1-ui-testing-gotchas/]]

UI Test的概念
Elements
UI tests 存在於app外,並利用proxy elements與app互動. 這些proxies代表實際在app中的UI元素. 例XCUIElement type為Button代表UIButton, 但XCUIElement所代表的物件只有某些屬性, 如title而沒有title color. 而且和他們互動只有限定的API 像是tap 或 double-tap.

Queries
利用queries來導航結構樹並取得elements
UI element type適用enumeration(XCUIElementType)來表示,像是StaticText而不是classes如UILabel.
Common types可以利用存取運算子來取得全部的tables而不必人工建立一個query如descendantsMatchingType
有一點要注意的是element types沒有分平台, 因此你會同時看到iOS的.Cell及OS X的.TableRow及.TableColumn

Simulated Events
取得element後利用tap或doubleTap等來模擬操作

以移動專案為例:

```- (void)testExample {
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
   }```

