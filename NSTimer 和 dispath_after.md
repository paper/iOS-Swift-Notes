## iOS SDK 8.3

### dispatch_after
http://stackoverflow.com/questions/28356263/stop-dispatch-after

```
typealias cancellable_closure = (() -> ())?
    
func setTimeout(#seconds:Double, callback:()->Void) -> cancellable_closure {
    var cancelled = false
 
    let cancel_closure: cancellable_closure = {
        cancelled = true
    }
 
    var delay = seconds * Double(NSEC_PER_SEC)
    var time = dispatch_time(DISPATCH_TIME_NOW, Int64(delay))
 
    dispatch_after(time, dispatch_get_main_queue()) {
        if !cancelled {
            callback()
        }
    }
        
    return cancel_closure
}
    
func clearTimeout(cancel_closure:cancellable_closure) {
    cancel_closure?()
}

// 运用实例：
// UITableViewCell 双击事件

var tapCount = 0
var tapOneClickKey:cancellable_closure

override func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath) {

    if let cell = tableView.cellForRowAtIndexPath(indexPath){
        tapCount++
    
        switch tapCount {
        case 1:
            tapOneClickKey = setTimeout(seconds: 0.4, callback: {
                println("tap one")
                self.tapCount = 0
            })
        case 2:
            clearTimeout(tapOneClickKey)
            println("double tap")            
            tapCount = 0
        default:
            break
        }
    }
        
 }
```

### NSTimer
https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Classes/NSTimer_Class/index.html

```
// 定义好后，3秒后，会运行dotest函数
// 如果你想 快点执行dotest(立即执行)： tm.fire()
// 如果你想 取消执行dotest(立即取消)： tm.invalidate()
var tm = NSTimer.scheduledTimerWithTimeInterval(3.0, target: self, selector: "dotest", userInfo: nil, repeats: false)

func dotest() {
    println("NSTimer -> dotest")
}

// 上面的 “UITableViewCell 双击事件” 也可以改为 NSTimer 来实现

```
