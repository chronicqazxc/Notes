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
    


