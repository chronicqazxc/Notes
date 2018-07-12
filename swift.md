# Swift

* [Synchronized](http://yuhua-chen.logdown.com/posts/253806-synchronized-on-swift)
* [Completion Handlers](https://thatthinginswift.com/completion-handlers/)
* [Declare closure](http://fuckingclosuresyntax.com)
* [@noescape](http://stackoverflow.com/questions/28427436/noescape-attribute-in-swift-1-2)
* [Memory management](http://katalisha.com/2016/01/22/ARC-Swift-closures-and-weak-self.html)
* Curried function in Swift (Alternated solution)
      func rideTypeFilter(type: RideType, fromRides rides: [Ride]) -> [Ride] {
        return rides.filter { $0.types.contains(type) }
      }

      func createRideTypeFilter(type: RideType) -> [Ride] -> [Ride] {
        return { (rides: [Ride]) -> [Ride] in
          return rideTypeFilter(type, fromRides: rides)
        }
      }

      let kidRideFilter = createRideTypeFilter(.Kids)

      print(kidRideFilter(parkRides))
      
* [Functional Programming in Swift 1](https://www.raywenderlich.com/114456/introduction-functional-programming-swift)
* [Functional Progrmming in Swift 2](https://www.raywenderlich.com/82599/swift-functional-programming-tutorial)
* [Swift guide to map filter reduce](http://useyourloaf.com/blog/swift-guide-to-map-filter-reduce/)    
* [Map or Reduce with index](http://stackoverflow.com/questions/28012205/map-or-reduce-with-index-in-swift)
* [Using bridging headers with framework targets is unsupported](http://stackoverflow.com/questions/24875745/xcode-6-beta-4-using-bridging-headers-with-framework-targets-is-unsupported)
* [non-modular header inside framework module](http://stackoverflow.com/questions/24103169/swift-compiler-error-non-modular-header-inside-framework-module)
* Capture whole UICollecitonView
        let seconds = 10.0
        let delay = seconds * Double(NSEC_PER_SEC)  // nanoseconds per seconds
        let dispatchTime = dispatch_time(DISPATCH_TIME_NOW, Int64(delay))
        // TODO: Simulate internel delay
        dispatch_after(dispatchTime, dispatch_get_main_queue(), { [weak self] in
            // Draw1
            let size = self?.dataSource.collectionView.contentSize
            UIGraphicsBeginImageContextWithOptions(size!, (self?.dataSource.collectionView.opaque)!, 0.0)
          self?.dataSource.collectionView.layer.renderInContext(UIGraphicsGetCurrentContext()!)
            
            // Draw2
            let heigh = (self?.dataSource.collectionView.contentSize.height)! - (self?.view.frame.height)! + 10
            
            let rect = CGRectMake(0, (self?.view.frame.height)!, CGRectGetWidth((self?.dataSource.collectionView.bounds)!), (self?.dataSource.collectionView.contentSize.height)! - heigh)
            self?.dataSource.collectionView.scrollRectToVisible(rect, animated: false)
            self?.dataSource.collectionView.layer.renderInContext(UIGraphicsGetCurrentContext()!)
            
            // Draw3
            let bottom = CGRectMake(0, heigh, CGRectGetWidth((self?.dataSource.collectionView.bounds)!), heigh)
            self?.dataSource.collectionView.scrollRectToVisible(bottom, animated: false)
            self?.dataSource.collectionView.layer.renderInContext(UIGraphicsGetCurrentContext()!)
            
            let image = UIGraphicsGetImageFromCurrentImageContext()
            UIGraphicsEndImageContext()

            UIImageWriteToSavedPhotosAlbum(image!, nil, nil, nil);
        })
* [Swift pattern matching in detail](https://appventure.me/2015/08/20/swift-pattern-matching-in-detail/)
* [Global-vs-static-function-swift/](https://borgs.cybrilla.com/tils/global-vs-static-function-swift/)
* [Swift Imports](https://robots.thoughtbot.com/swift-imports)
