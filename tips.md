# Tips

####Single tap & double tap
```objc
UITapGestureRecognizer *singleTap = [[[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(doSingleTap)] autorelease];
singleTap.numberOfTapsRequired = 1; 
[self.view addGestureRecognizer:singleTap];

UITapGestureRecognizer *doubleTap = [[[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(doDoubleTap)] autorelease];
doubleTap.numberOfTapsRequired = 2; 
[self.view addGestureRecognizer:doubleTap];

[singleTap requireGestureRecognizerToFail:doubleTap];
```

####Perform connection on main thread
```objc
[self performSelectorOnMainThread:@selector(start) withObject:nil waitUntilDone:YES];
- (void)start
{
    NSURL *url = [NSURL URLWithString:@"www.2cto.com"];
    NSURLRequest *request =[NSURLRequest requestWithURL:url cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:30.0];
    self.connection = [[NSURLConnection alloc] initWithRequest:request delegate:self startImmediately:NO];//暂时不运行
    [connection scheduleInRunLoop:[NSRunLoop currentRunLoop] forMode:NSRunLoopCommonModes];//用NSRunLoopCommonModes
    [connection start];    
    if (self.connection) {
        NSLog(@"success");
    }else {
        NSLog(@"failed");
    }
}
```

####Scroll would not block timer
```objc
NSRunLoop *runloop = [NSRunLoop currentRunLoop];
NSTimer *timer = [NSTimer timerWithTimeInterval:0.1 target:self selector:@selector(myTimerAction:) userInfo:nil repeats:YES];
[runloop addTimer:timer forMode:NSRunLoopCommonModes];
[runloop addTimer:timer forMode:UITrackingRunLoopMode];
```