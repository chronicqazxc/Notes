# Swift

* [Synchronized](http://yuhua-chen.logdown.com/posts/253806-synchronized-on-swift)
* [Completion Handlers](https://thatthinginswift.com/completion-handlers/)
* [Declare closure](http://fuckingclosuresyntax.com)
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
* [Map or Reduce with index](http://stackoverflow.com/questions/28012205/map-or-reduce-with-index-in-swift)
* [Using bridging headers with framework targets is unsupported](http://stackoverflow.com/questions/24875745/xcode-6-beta-4-using-bridging-headers-with-framework-targets-is-unsupported)
* [non-modular header inside framework module](http://stackoverflow.com/questions/24103169/swift-compiler-error-non-modular-header-inside-framework-module)
