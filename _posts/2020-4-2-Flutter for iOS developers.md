---
post: page
title: Flutter for iOS developer
subtitle: understand the difference between Flutter and native development
tags: [Flutter,iOS]
comment: true 
---
## WHAT ARE THE EQUIVALENT TO UIVIEW IN FLUTTER?
In iOS, you create your UI with view objects that are instances of UIView. In Flutter, everything is a widget, and that’s the closest comparison to a UIView. They aren’t exactly the same,

because they handle more, but they are used to construct UI. For our intents and purposes, they’re close enough.

So, if widgets are UIViews, what’re the differences?

First, widgets are immutable. They’re light-weight blueprints for the UI that are destroyed as soon as they need to be changed. Every time the configuration or state of a widget is changed, Flutter redraws the relevant widget tree. But, widgets are just descriptions for actual elements, and don’t get drawn to the screen directly.

Also, because of the immutability, a widget doesn’t "change" it’s children widgets. Rather than saying: "hey, UI element, remove child ABC and replace it with XYZ", you just redraw the UI element with the child XYZ.

Widgets and updating the view is explained in detail in chapters one and three.

## WHAT IS THE PARADIGM OR MENTAL MODEL DIFFERENCE?
The biggest difference between writing Flutter and iOS is that Flutter uses composition and reactive-style programming to make handling UI state simple. You, the developer, don’t have to be concerned with mutating the UI State, because it’s handled by the framework internally.

This is mostly due to the fact that the UI is described by widgets. Widgets aren’t UI elements themselves, but rather they’re "blueprints" for true elements. And you use widgets to describe the current view. And, as your app’s state changes and the screen needs to re-render, the framework is just rendering the current widget tree, and it knows how to transition the UI as it changes. You don’t have to tell the UI explicitly to remove elements from the screen and add new ones. You just say "hey Flutter, this is what my widget tree looks like. And, when that button is pressed, it’ll look like this." And Flutter knows how to make that transition happen. This is called reactive programming.

Secondly, in iOS you often extend UIView or other UI classes to create your views. Flutter uses composition instead. All of your widgets are tiny, modular views that are pieced together similar to a markup language like HTML. This makes your views highly reusable.


## HOW TO I MAKE COMPLEX LAYOUTS LIKE UITABLEVIEW?
In iOS, you can show a list of elements in either a UITableView or UICollectionView. In Flutter this can be done with ListView widgets, GridView widgets, and the Table widget.
The ListView widget is specifically a great example of Flutter vs iOS. Unlike in iOS, there’s no need to determine the number of rows up front, or the size of the cells upfront. Due partially to the immutability of widgets, you simply pass a list of widgets to a ListView and it "just works".

##  WHAT’S SIMILAR TO STORYBOARD?
In short, nothing. Everything is a widget, including the app structure and layouts themselves. You use widgets to add padding to other widgets, rather than setting constraints in the Storyboard.

## How to draw to Screen
In iOS, you can use "CoreGraphics" to draw on the screen. Flutter has something similar-ish called Canvas. It’s similar the HTML canvas. You draw to canvas, which is housed by a widget, using the CustomPainter class, which you use to run your algorithm which paints lines and shapes to the screen.

## How to manage the dependencies
The pubspec file uses Dart's Pub package manager to declare and fetch dependencies.

## HOW DO I INTERACT WITH THE DEVICE AND USE NATIVE APIS?
Perhaps the biggest difference between native mobile development and Flutter development is that Flutter doesn’t have direct access to the devices underlying SDK. Your Flutter app actually is hosted in a ViewController on iOS, but you can’t communicate with it directly.

Flutter solved this problem by creating "platform channels", which can communicate with the ViewController. According to the docs, “Platform channels are essentially an asynchronous messaging mechanism that bridge the Dart code with the host ViewController and the iOS framework it runs on. You can use platform channels to execute a method on the native side, or to retrieve some data from the device’s sensors, for example.

Most platform channel work would be included in your app as a plugin that encapsulates the native and Dart code and exposes the Dart api. You can write your own plugins to do this, which basically consists of writing the iOS native code, because the Dart code is generally quite simple.

This isn’t so necessary, though, because there are already a ton of plugins provided by the Pub package manager that communicate with native APIS.
for instance :
* image_picker to access the camera
* geolocator to access the GPS sensor

 
