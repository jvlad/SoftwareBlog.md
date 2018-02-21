---
title: "Access Swift properties from Objective-C. Mixing Objective-C with Swift"
date: 2018-02-21T08:55:30
draft: false
---

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
