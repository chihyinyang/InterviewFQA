# InterviewFQA

## Overview
- [viewController - life cycle](#viewControllerLifeCycle)
- [App - life cycle](App_-_life_cycle)
- [Optional](optional)
- [@escaping](escaping)
- Struct vs class
- Value type vs reference type
- State variable
- Objective oriented programming
- Protocol oriented programming
- Architecture: MVVM, MVVM-C, MVC
- SOLID principles
- Unit test, UITest
- Access control: open vs public
- Dependency injection
- Approach for data persistence
- Singletion
- troubleShooting
- Retain cycle, weak, unowned, ARC
- Bounds and frame
- Combine


<h2 name="viewControllerLifeCycle">ViewController - Life cycle</h2>

### Life Cycle happens order
1. init
2. loadview
3. viewDidLoad
4. viewWillAppear
5. viewWillLayoutSubviews 
6. viewDidLayoutSubviews
7. viewWillLayoutSubviews ← repeat here
8. viewDidLayoutSubviews ← repeat here
9. viewDidAppear
10. viewWillDisappear
11. viewDidDisappear
12. deinit  

#### init
- It would be called when you create an instance of the viewController.
- We can create custom initializer, the intializer is added to accept a custom property and perform the necessary setup before calling the superclass's designed intializer. Example: injection
  
#### LoadView
- This method is called automatically by the system when the view property of the viewController is accessed, and the view is currently nil.
- ViewController creates its custom view hierarchy or a single root view that will act as the container for other subviews.
- Once the view hierarchy is created, the viewController sets it as te value of its `view` property using the `view` property setter.
- We can create our custom root view by using `let rootView = UIView(frame: UIScreen.main.bounds)`
  
#### ViewDidLoad
- This method will be called once in vc life cycle after the view has been loaded into memory but before it is presented.
- Do the things that need to be done once.
  - Data fetching
  - Subview customization

#### ViewWillAppear
- This method is called when the view becomes visible to the user.
- You do the animation setup here.
- I would do the navigationBar updates here.
  
#### viewWillLayoutSubviews
- This method will be called before the view's subviews are laid out.
- This method is called frequently, so we should avoid performing expensive or time-comsuming operations within this method.
  
#### viewDidLayoutSubviews
- This method will be called after the view's subviews have been laid out.
- Need avoid performing heavy computations or layout changes that trigger another layout pass within this method.
  
#### ViewWillAppear
- This method is called whenever the view is going to be presented.
- If you want to add animations or transitions when the view appears, viewWillAppear(_:) is a suitable place to set up those animations before the view is displayed.
  
#### ViewDidAppear
- This method is called after the view has finished animating and is fully visible to the user.
  
#### viewWillDisappear
- This is method is called when the view is about to removed or disappear from the screen.
-  This is a appropriate place to perform any cleanup or state-saving tasks.
  
#### viewDidDisapppear
- This method is called after the view has disappeared from the screen.
- We can perform any final cleanup or release of resources associated with view or the viewController.
- Stop Animation or Timers.
  
#### deinit
- This method will be called before an object is deallocated from memory.
- We can release any resources associated with the object that need manual cleanup.
- Removing observers

<h2 name="appLifeCycle">App - life cycle</h2>

#### The `AppDelegate` class in iOS is responsible for manaing the app's life cycle and responding to various state changes.
- `application(_:didFinishLaunchingWithOptions:)`
  - This method will be called when app is launched.
    
- `applicationWillResignActive(_:):`
  - This method will be called when the app is about to transitioin from an active to an inactive.
  - example：incoming phone call or a system alert appear.
    
- `applicationDidEnterBackground(_:)`
  - This method will be called when the app enter background, either user pressed the home button or because another app is launched.
    
- `applicationWillEnterForeground(_:)`
  - This method will be called when the app is back to the foreground.
    
- `applicationDidBecomeActive(_:):`
  - This method is called when tha app becomes active.
    
- `applicationWillTerminate(_:):`
  - This method will be called when the app is about to terminate.
    
- `applicationDidReceiveMemoryWarning(_:):`
  - This method is called when the system issues a memory warning to the app due to low memory conditions.
  - You can release the unnecessary memory and resources to prevent the app from being terminated.


<h2 name="optional">Optional</h2>
An optional is a way to handle a variable that mighe be empty. It adds a question mark to the variable's type, indicating the possibility to be nil.

To work with optional value, there were two safe way we can obtain the value: Optional chaining and Conditional binding. 

It is important to note that force unwrapping is unsafe way to get the value. It would cause a crash when you try to get the value from the variable, but the variable is empty.

<h2 name="escaping">@escaping</h2>

### What's the difference between an @escaping and a non-@escaping closure?

The difference between an @escaping and a non-@escaping closure is depends on how the closure is used and its lifetime.

##### non-@escaping closure
non-@escaping closure is the default behaviour in Swift. It is a closure that is guaranteed to be executed before the enclosing function returns. It means that the closure is synchronous and doesn't outlive the function itself.

##### @escaping closure
@escaping closure is a closure that can outlive the function, it means it can be stored or assign to a varibles. @escaping closure typically used when you want to capture the closure.

##### Key Diff
The key difference lies in how the closure is treated by the complier. For non-@escaping closures, the compiler can make certain optimazations since it know the closure will not outlive the function. In constrast, @escaping closure requires addtional considerations by the compiler to ensure the capured values retained and the closure is available when needed. 








