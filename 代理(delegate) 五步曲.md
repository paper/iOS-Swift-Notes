## iOS SDK 8.3

### 代理(delegate) 五步曲
Delegates in five easy steps
In review, these are the steps for setting up the delegate pattern between two objects, where object A is the delegate for object B, and object B will send out the messages:
  1. Define a delegate protocol for object B.
  2. Give object B an optional delegate variable. This variable should be weak.
  3. Make object B send messages to its delegate when something interesting happens, such as the user pressing the Cancel or Done buttons, or when it needs a piece of information.
  4. Make object A conform to the delegate protocol. It should put the name of the protocol in its class line and implement the methods from the protocol.
  5. Tell object B that object A is now its delegate.
dd
```
// 第5步，
// 第一种可能：某个controller里面的元素代理，就比如 class A:UIViewController, UITextFieldDelegate
@IBOutlet weak var textField: UITextField!
textField.delegate = self

// 第二种就是跨两个 viewController：Tell object B that object A is now its delegate.
// 在A里面写：
override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
  // segueIdentifierName是指向B的segue identifier name
  if segue.identifier == "segueIdentifierName" {
    
    // 如果 A -> B
    let controller = segue.destinationViewController as! BController 
    controller.delegate = self
    
    // ---------- 分割线 -----------
    
    // 如果A -> navigationController -> B
    let navigationController = segue.destinationViewController as! UINavigationController
    let controller = navigationController.topViewController as! BController
    controller.delegate = self
     
  }
}
```
