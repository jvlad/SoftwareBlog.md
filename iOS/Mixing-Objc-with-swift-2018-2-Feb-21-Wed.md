---
title: "Accessing Swift properties from Objective-C. Mixing Objective-C with Swift"
date: 2018-02-20T08:55:30
draft: true
---

# Accessing Swift properties from Objective-C. Mixing Objective-C with Swift in Framework Target

Example that worked for developing Framework Target using both Objective-c and Swift languages.

Possible ways to declare Swift properties that are accessible from obj-c code:  

``` swift
// in SampleClass.swift

public class SampleClass: NSObject {
// Other possible options for class declaration
// open class SampleClass: NSObject {
// @obj public class SampleClass: NSObject {
// @obj open class SampleClass: NSObject {

  @objc public let sampleConstant: String
  @objc open let sampleConstant2: String
  
  @objc public var readWriteVariable: String
  @objc public private(set) var readOnlyVariable: String

  @objc open var readWriteVariable: String
  @objc open private(set) var readOnlyVariable: String
}
```

While in objc file I have 
``` Objc
// in Consumer.m. 

#import "Consumer.h" // `Consumer.h` is a part of the same framework that contains `SampleClass.swift` as well
#import <FrameworkProductNameIAmInRightNow/FrameworkProductNameIAmInRightNow-Swift.h>

@implementation   //... left for homework, I am lazy.

SampleClass *sampleObj = [[SampleClass alloc] init];
NSLog(sampleObj.sampleConstant);

@end
```

The official doc by Apple<sup>1</sup> seemed to me as confusing and hard-to-navigate paper. Beside it, it's not correct, at least, in some details<sup>2</sup>.

I asked publicly if somebody has seen a better version of a documentation on the topic.

Better in terms of: 
* Structure and navigation between subtopics
* Smaller number of wrong and misleading statements
* Working source code examples supply

I still look for the answer. In general, I would like to have this<sup>1</sup> document split to separate files on my local disk to be able to search though it, reorder some parts and make notes. Why just not to publish it to GitHub to keep it up to date in collaboration with other developers?

[1]: 'Swift and Objective-C in the Same Project'  
      https://developer.apple.com/library/content/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html#//apple_ref/doc/uid/TP40014216-CH10-ID122

[2]: E. g. the doc says:  
  > To be accessible and usable in Objective-C, a Swift class must be a descendant of an Objective-C class or it must be marked @objc.

  That's not true. According to what compiler complains about, I can not use `@objc` mark for classes that are not derivatives of Objective-C classes (which often means derivatives of `NSObject`). Therefor, it's not logically correct to use "**or**" in that statement from the documentation. 