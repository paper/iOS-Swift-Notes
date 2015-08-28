## Objective-C 兼容性、Property List和Views By Paul Hegarty
###### open.163.com

### NSUserDefaults

##### A storage mechanism for Property List data

- It's essentially a very tiny database that stores Propery List data.
- It persists between launchings of your application!
- Great for thing like "setting" and such
- Do not use it for anything big!

```
// It can store/retrieve entire Property Lists by name(keys)...
setObject(AnyObject, forKey:String)    // the AnyObject must be a Property List
objectForKey(String) -> AnyObject?
arrayForKey(String) -> Array<AnyObject>? // returns nil if value is not set or not an array

// It can also store/retrieve little pieces of data ...
setDouble(Double, forKey:String)
doubleForKey(String) -> Double    // not an optional, returns 0  if no such key
```
##### Using NSUserDefaults
```
// Get the defaults reader/writer ...
let defaults = NSUserDefaults.standardUserDefaults()

// Then write and read ...
defaults.setObject(AnyObject, forKey:String)    // AnyObject musy be a Property List
let plist:AnyObject = defaults.objectForKey(String)

// Your changes will be automatically saved
// But you can be sure they are saved at any time by synchronizing ...
if !defaults.synchronize(){ /* failed! not much you can do about it */ }
(it's not "free" to synchronize, but it's not that expensive either)
```

### Views
```
addSubview(aView: UIView)    // sent to aView's (soon to be) superview
removeFromSuperview()    // this is sent to the view you want to remove(not its superview)
```





