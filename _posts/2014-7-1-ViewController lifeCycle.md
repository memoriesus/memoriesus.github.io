---
post: page
title: View Controller lifeCycle
tags: [iOS]
comment: true 
---

#  What's the lifeCycle 

LifeCycle is an event that has several steps from the point of creation to deletion. It is a sequence of methods as they progress. If you want to design an application, you need to study the concepts and life cycle of the View Controller.

View Controllers play a major role in iOS applications and they create the skeleton of every application made by developers. While programming in iOS, it is inevitable to avoid subclass UIViewController.

A View Controller manages a set of views and helps in making the application’s user interface. It coordinates with model objects and other controller objects. It is known for playing the role for both view objects and controller objects. Each view controller displays its own views for the app content. The views are loaded automatically when the user accesses
’

the view property of view controller in the app Let s focus on the events
the view property of view controller in the app Let s focus on the events
controller If you are working with storyboards or nib files then you do
 required to load a view.
# Lifecycle events order
 
init(coder:)
 (void)loadView  (void)viewDidLoad  (void)viewWillAppear  (void)viewDidAppear  (void)didReceiveMemoryWarning  (void)viewWillDisappear
 (void)viewDidDisappear
How can we use them? - init
init(coder:)

While creating the views of your app in a Storyboard, init(coder:) is the method that gets called to instantiate your view controller and bring it to life. During the initial phase of a view controller, you usually allocate the resources that the view controller will need during its lifetime. In this method, you might instantiate dependencies, including subviews that you’ll add to your view programmatically. And note that init(coder:) is called only once during the life of the object, as all init methods are.

- LoadView
(void)loadView 
It is only called when the view controller is created and only when done programatically. You can override this method in order to create your views manually. This is the method that creates the view for the view
.

controller. If you are working with storyboards or nib files, then you do not have to anything with this method and you can ignore it. Its implementation in UIViewController loads the interface from the interface file and connects all the outlets and actions for you.
- viewDidLoad
-(void)viewDidLoad 
{
[super viewDidLoad]; }

It’s only called when the view is created. Keep in mind that in this lifecycle

step the view bounds are not final. Good place to init and setup objects used in the viewController. When this method gets called, the view of the view controller has been created and you are sure that all the outlets are in place. It is also a good place where to start some background activity where you need to have the user interface in place at the end. A common case are network calls that you need to do only once when the screen is loaded. This method is called only once in the lifetime of a view controller, so you use it for things that need to happen only once.

- viewWillAppear
(void)viewWillAppear:(BOOL)animated 
You override this method for tasks that require you to repeat every time a view controller comes on screen. Keep in mind that this method can be called several times for the same instance of a view controller. This event is called every time the view appears and so, there is no need to add code here, which should be executed just one time. Usually you use this method to update the user interface with data that might have changed while the view controller was not on the screen. You can also prepare the interface for animations you want to trigger when the view controller appears.
 
appears
 - viewDidAppear
(void)viewDidAppear:(BOOL)animated
This method gets called after the view controller appears on screen. You can use it to start animations in the user interface, to start playing a video or a sound, or to start collecting data from the network. In some cases can be a good place to load data from core data and present it in the view or to start requesting data from a server.
- didReceiveMemoryWarning
(void)didReceiveMemoryWarning
iOS devices have a limited amount of memory and power. When the memory starts to fill up, iOS does not use its limited hard disk space to move data out of the memory like a computer does. If your app starts using too much memory, iOS will notify it. Since view controllers perform resource management, these notifications are delivered to them through this method. In this way you can take actions to free some memory. Keep in mind that if you ignore memory warnings and the memory used by your app goes over a certain threshold, iOS will end your app means this will look like a crash to the user and should be avoided.
- viewWillDisappear
(void)viewWillDisappear
Before the transition to the next view controller happens and the origin view controller gets removed from screen, this method gets called. You rarely need to override this method since there are few common tasks that need to be performed at this point, but you might need it.
- viewDidDisappear

(void)viewDidDisappear
After a view controller gets removed from the screen, this method gets called. You usually override this method to stop tasks that are should not run while a view controller is not on screen. For example, you can stop listening to notifications, observing other objects properties, monitoring the device sensors or a network call that is not needed anymore.


