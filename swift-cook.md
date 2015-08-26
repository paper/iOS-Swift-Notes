## Swift语言与Foundation框架 By Paul Hegarty
###### open.163.com

### Array

```
// Some Array<T> Methods

+= [T] // not += T
first -> T? // note optional
last -> T? // note optional

var r = [a,b,c] // assume a,b,c are of some type (the same type)

append(T)
insert(T, atIndex:Int)	// r.insert(d, atIndex:1), r = [a,d,b,c]
splice(Array<T>, atIndex:Int) // r.splice([d, e], atIndex:1), r = [a,d,e,b,c]

removeAtIndex(Int)	// r.removeAtIndex(1), r = [a,c]
removeRange(Range)	// r.removeRange(0..<2), r = [c]
replaceRange(Range, with:[T])	// r.replaceRange(0...1, with:[x,y,z]), r = [x,y,z,b]

sort(isOrderedBefore: (T, T) -> Bool) // r.sort { $0 < $1 }

filter(includeElements: (T) -> Bool) -> [T] // 返回闭包里面为true的元素，一个新数组

map(transform: (T) -> U) -> [U]
let stringified: [String] = [1,2,3].map { "\($0)" }

reduce(initial: U, combine:(U, T) -> U) -> U
let sum: Int = [1,2,3].reduce(0) { $0 + $1 } // adds up the numbers in the Array
```

### String

```
// String.Index

var s = "hello"
let index = advance(s.startIndex, 2) // index is a String.Index to the 3rd glyph, "l"
s.splice("abc", index) // s will now be "heabcllo" (abc inserted at 2)

let startIndex = advance(s.startIndex, 1)
let endIndex = advance(s.startIndex, 6)
// 这里视频有个笔误
let substring = s[startIndex..<endIndex] // substring will be "eabcl"

var num = "56.25"
if let decimalRange = num.rangeOfString(".") {  //decimalRange is Range<String.index>
	let wholeNumberPart = num[num.startIndex..<decimalRange.startIndex] // "56"
}

// 这个视频还有个笔误，removeRange 是没有 [] 中括号的
num.removeRange(num.startIndex..<decimalRange.startIndex)	// .25，这个会改变 num 的值

num.replaceRange(num.startIndex..<decimalRange.startIndex, with: "ab") // ab.25，这个也会改变 num 的值

// Other String Methods
description -> String	// Printable
endIndex -> String.Index
hasPrefix(String) -> Bool
hasSuffix(String) -> Bool

// no toDouble
toInt() -> Int?

// "hello world".capitalizedString = "Hello World"
capitalizedString -> String
lowercaseString -> String
uppercaseString -> String

// ",".join(["1", "2" ,"3"]) = "1,2,3"
join(Array<String>) -> String

// "1,2,3".componentsSeparatedByString(",") = ["1", "2", "3"]
componentsSeparatedByString(String) -> [String]
```

### Type Conversion

```
let d:Double = 37.5
let f:Float = 37.5
let x = Int(d)			// 37
let xd = Double(x)		// 37
let cgf = CGFloat(d)	// 37.5

let a = Array("abc")	// a = ["a","b","c"], i.e. array of Character
let s = String(["a","b","c"])	// s = "abc" (the array is of Character, not String)

let s = String(52) // no floats 
let s = "\(37.5)" // 转换成字符串，就使用这种
```

### Assertions

```
// the function arguments is an "autoclosure" however, so you don't need the {}
assert(()->Bool, "message")

// will crash if validation() returns nil
assert(validation() != nil, "the validation function returned nil")

```
### Other Functions

```
// Collections include Array, Dictionary, String
// Sliceables include Array, String
// Below is pseudo-code because it's too much to teach the types involved here at this point
// 下面是伪代码

let count  = count(aCollection)	
let sub 	 = dropFirst(aSliceable)	// drop the first thing in the sliceable
let sub 	 = dropLast(aSliceable)		// drops the last thing in the sliceable
let first  = first(aCollection) 		// the fisrt element in the collection (or nil)
let last 	 = last(aCollection)	 	// the last element in the collection (or nil)
let prefix = prefix(aSliceable, maxLength:Int) // returns the first maxLength things
let suffix = suffix(aSliceable, maxLength:Int) // returns the last maxLength things
let reversed: Array = reverse(aCollection)     // return Array type!
let backwardsString = String(reverse(s))
let enum = enumerate(aSliceable)	// for (index, value) in enumerate(aSliceable) { ... }
```










