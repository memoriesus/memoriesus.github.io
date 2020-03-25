---
post: page
title: the difference between Any and AnyObject in Swift
subtitle: Understand the scene to use them better
tags: [Swift,iOS]
comment: true
---
#AnyObject
The protocol to which all classes implicitly conform


You use AnyObject when you need the flexibility of an untyped object or when you use bridged Objective-C methods and properties that return an untyped result. AnyObject can be used as the concrete type for an instance of any class, class type, or class-only protocol.

#Any 

In Swift 3, the id type in Objective-C now maps to the Any type in Swift, which describes a value of any type, whether a class, enum, struct, or any other Swift type. This change makes Objective-C APIs more flexible in Swift, because Swift-defined value types can be passed to Objective-C APIs and extracted as Swift types

