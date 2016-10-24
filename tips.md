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