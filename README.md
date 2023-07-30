# InterviewFQA

## Overview
- [viewController - life cycle](#viewControllerLifeCycle)
- [App - life cycle](App_-_life_cycle)
- [Optional](optional)
- [@escaping](escaping)
- [Struct vs Class](structVSClass)
- [Value type vs reference type](valueVSReference)
- [State variable](stateVariable)
- [Object-Oriented Programming(OOP)](oop)
- [Protocol oriented programming](pop)
- Architecture: MVVM, MVVM-C, MVC
- [SOLID principles](SOLID Principle)
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

<h2 name="structVSClass">@escaping</h2>

### What's the difference between an @escaping and a non-@escaping closure?

The difference between an @escaping and a non-@escaping closure is depends on how the closure is used and its lifetime.

##### non-@escaping closure
non-@escaping closure is the default behaviour in Swift. It is a closure that is guaranteed to be executed before the enclosing function returns. It means that the closure is synchronous and doesn't outlive the function itself.

##### @escaping closure
@escaping closure is a closure that can outlive the function, it means it can be stored or assign to a varibles. @escaping closure typically used when you want to capture the closure.

##### Key Diff
The key difference lies in how the closure is treated by the complier. For non-@escaping closures, the compiler can make certain optimazations since it know the closure will not outlive the function. In constrast, @escaping closure requires addtional considerations by the compiler to ensure the capured values retained and the closure is available when needed. 


<h2 name="escaping">Struct vs Class</h2>

### What is the difference between struct and a class in Swift?

##### Struct
Struct is value type, and it doesn't support inheritance. And they are allocated on the stack, they are deallocated automatically when that go out of scope.

##### Class
Class is reference type, and it support inheritance, and they're stored on the heap and require memory management using ARC. The memory is dellocated when there are zero reference to the instance.

##### Which one is better?
Choosing between a Struct and a Class depends on the specific use case and requirements. Struct are suitable for small, simple, and immutable data structure, while classes are preferred for more complex objects that require reference semantics, inheritance, and more advanced features.

<h2 name="valueVSReference">Value type vs reference type</h2>

### What's the difference between a value type and a reference type?

##### Value Type
A value type is a type that is copied when assigned to a new variable or passed as a function argument. Modifying a copy of a value type does not affect to the original instance. Examples of value type in Swift include struct, intergers, string and enum.

##### Reference Type
A reference type is a type that is passed b reference. When assigned to a new variable or passed as an argument, a referenceto the exsiting instance is created, and both variable point to the same underlying object in memory. Modifying a reference type affect all variables that reference the same object. Examples of reference type in Swift include Class, closure.

<h2 name="stateVariable">State variable</h2>
When you declare a property or method as `state`, it means there is only one copy of that property or method shared across all instances of the class or struct, and you can access it directly through the type itself.

##### Static Property
- A static property is associated with the type itself, not with the instance of the type.
- All instances of the type share the same value for the static property.
- Static properties or methods can be accessed direrctly through the type without creating an instance of the type.
  
  ```
  class AClass {
    static var count = 0
  }
  // Accessing the static property without creating an instance.
  let value = AClass.count
  ```


<h2 name="oop">Object-Oriented Programming(OOP)</h2>

In OOP, software is designed and organized using objects, which are instances of classses representing real-world entities or concerpts.

#### Key Principles:

##### 1. Encapsulation
Encapsulation is the binding of data and methods into one entity to define itself and the scope of its operations. The bundling of data and methods into individual entities hides complexity by providing abstracted interface to program and interact with. The most common example of such a unit would be a class/object setting. 

##### 2. Abstraction
Abstraction focus on representing the essential features of an object while hiding the unnecessary details. Swift Example: Protocol

##### 3. Inheritance
Inheritance enables a class to inherit properties and behavious from another class. This promotes code reuse and hierarchical relationships between classes.

##### 4. Polymorphism
Polymorphism allows objects of different classes to be treated as objects of a common superclass. It enables a single interface to represent multiple underlying data types, providing flexibility and extensibility in the code.

#### Benefits
- Modularity
- Reusability
- Maintainability
- Flexibility
- Scalability


<h2 name="pop">Protocol-Oriented programming(POP)</h2>
Protocol-Oriented Programming is a programming paradigm that emphasizes the use of protocols to define interfaces and behaviour, promoting code reuse and flexibility.

### Key Concepts:

##### 1. protocol
A protocol in Swift like as a blueprint defining a set of methods, properties, and other requirements. These requirements act as a contract that any class, struct, or enum adopting the protocol must fulfill.

##### 2. Protocol Adoption
A class, struct, or enum can adopt a protocol by declaring that it conforms to it.

##### 3. Protocol Extensions
Protocols can be extended to provide default impletmentations for some of their requirments.

##### 4. compositions
Code reuse is achieved through composition rather than inheritance. Instead of using subclassing, you create small, modular protocols and then compose types by conforming to multiple protocols.

### Benefits:
- Code Reusability
- Multiple Inheritance
- Protocol Extensioins
- Testability
