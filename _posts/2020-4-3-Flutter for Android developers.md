---
post: page
title: Flutter for Android developer
tags: [Flutter,Android]
comment: true
---


## 1  WHAT IS THE EQUIVALENT OF A VIEW IN FLUTTER?
In Andriod, you create all your UI elements with Views. In Flutter, everything is a widget, and that’s the closest comparison to a View. They aren’t exactly the same, because they handle more, but they are used to construct UI. For our intents and purposes, they’re close enough.

So, if widgets are Views, what’re the differences?

First, widgets are immutable. They’re light-weight blueprints for the UI that are destroyed as soon as they need to be changed. Every time the configuration or state of a widget is changed, Flutter redraws the relevant widget tree. But, widgets are just descriptions for actual elements, and don’t get drawn to the screen directly.

Also, because of the immutability, a widget doesn’t "change" it’s children widgets. There is no equivalent to addChild() or removeChild() Rather than saying: "hey, UI element, remove child ABC and replace it with XYZ", you just redraw the the UI element with the child XYZ.

## What's the paradigm or mental model difference?
The biggest difference between writing Flutter and Android is that Flutter uses composition and reactive-style programming to make handling UI state simple. You, the developer, don’t have to be concerned with mutating the UI State, because it’s handled by the framework internally.

This is mostly due to the fact that the UI is described by widgets. Widgets aren’t UI elements themselves, but rather they’re "blueprints" for true elements. And you use widgets to describe the current view. And, as your app’s state changes and the screen needs to re-render, the framework is just rendering the current widget tree, and it knows how to transition the UI as it changes. You don’t have to tell the UI explicitly to remove elements from the screen and add new ones. You just say "hey Flutter, this is what my widget tree looks like. And, when that button is pressed, it’ll look like this." And Flutter knows how to make that transition happen. This is called reactive programming.

Secondly, in Android, you often extend or subclass View to create your views. Flutter uses composition instead. All of your widgets are tiny, modular views that are pieced together similar to a markup



## 3,WHERE IS THE XML LAYOUT FILE?
In short, you don’t write any markup anymore. Everything is Dart code. Everything is a widget, including the app structure and layouts themselves. You use widgets to build the "widget-tree", which handles styles, layout, and structure (among other things).


## 4,HOW DO I DRAW TO THE SCREEN?
Flutter has an API based on the same rendering engine as Android, and it’s also called Canvas. You draw to canvas, which is housed by a widget, using the CustomPainter class, which you use to run your algorithm which paints lines and shapes to the screen.

There’s a big section on this in chapter six of this book, but in general Flutter Canvas should feel very familiar to Android developers.

## 5,WHAT IS THE EQUIVALENT OF AN INTENT IN FLUTTER?
In short, nothing. Flutter doesn’t really have a concept of activities. Rather, you navigate between screens using a navigator and routes. It’s much closer to routing on the web.

