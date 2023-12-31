# InterviewFQA

## Overview
- [ViewController Life Cycle](#viewcontroller-life-cycle)
- [App Life Cycle](#app-life-cycle)
- [Optional](#optional)
- [@escaping](#escaping)
- [Struct vs Class](#struct-vs-class)
- [Value Type vs Reference Type](#value-type-vs-reference-type)
- [State variable](#state-variable)
- [Object-Oriented Programming](#object-oriented-programming)
- [Protocol-Oriented programming](#protocol-oriented-programming)
- Architecture: MVVM, MVVM-C, MVC
- [SOLID principles](#solid-principles)
- [Unit Test](#unit-test), [UI Test](#ui-test)
- [Access control: open vs public](#access-control)
- [Dependency injection](#dependency-injection)
- [Approach for data persistence](#approach-for-data-persistence)
- [Singletion](#singleton)
- [TroubleShooting](#trouble-shooting)
- [Retain cycle](#retain-cycle), [Strong, Weak, Unowned](#strong-weak-unowned), [Automatic Reference Counting](#automatic-reference-counting)
- [Frame VS Bounds](#frame-vs-bounds)
- [Combine](#combine)


## ViewController Life Cycle

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

### init
- It would be called when you create an instance of the viewController.
- We can create custom initializer, the intializer is added to accept a custom property and perform the necessary setup before calling the superclass's designed intializer. Example: injection
  
### LoadView
- This method is called automatically by the system when the view property of the viewController is accessed, and the view is currently nil.
- ViewController creates its custom view hierarchy or a single root view that will act as the container for other subviews.
- Once the view hierarchy is created, the viewController sets it as te value of its `view` property using the `view` property setter.
- We can create our custom root view by using `let rootView = UIView(frame: UIScreen.main.bounds)`
  
### ViewDidLoad
- This method will be called once in vc life cycle after the view has been loaded into memory but before it is presented.
- Do the things that need to be done once.
  - Data fetching
  - Subview customization

### ViewWillAppear
- This method is called when the view becomes visible to the user.
- You do the animation setup here.
- I would do the navigationBar updates here.
  
### viewWillLayoutSubviews
- This method will be called before the view's subviews are laid out.
- This method is called frequently, so we should avoid performing expensive or time-comsuming operations within this method.
  
### viewDidLayoutSubviews
- This method will be called after the view's subviews have been laid out.
- Need avoid performing heavy computations or layout changes that trigger another layout pass within this method.
  
### ViewWillAppear
- This method is called whenever the view is going to be presented.
- If you want to add animations or transitions when the view appears, viewWillAppear(_:) is a suitable place to set up those animations before the view is displayed.
  
### ViewDidAppear
- This method is called after the view has finished animating and is fully visible to the user.
  
### viewWillDisappear
- This is method is called when the view is about to removed or disappear from the screen.
-  This is a appropriate place to perform any cleanup or state-saving tasks.
  
### viewDidDisapppear
- This method is called after the view has disappeared from the screen.
- We can perform any final cleanup or release of resources associated with view or the viewController.
- Stop Animation or Timers.
  
### deinit
- This method will be called before an object is deallocated from memory.
- We can release any resources associated with the object that need manual cleanup.
- Removing observers


<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>


## App Life Cycle

#### The `AppDelegate` class in iOS is responsible for managing the app's life cycle and responding to various state changes.
### `application(_:didFinishLaunchingWithOptions:)`
  - This method will be called when app is launched.
    
### `applicationWillResignActive(_:):`
  - This method will be called when the app is about to transitioin from an active to an inactive.
  - example：incoming phone call or a system alert appear.
    
### `applicationDidEnterBackground(_:)`
  - This method will be called when the app enter background, either user pressed the home button or because another app is launched.
    
### `applicationWillEnterForeground(_:)`
  - This method will be called when the app is back to the foreground.
    
### `applicationDidBecomeActive(_:):`
  - This method is called when tha app becomes active.
    
### `applicationWillTerminate(_:):`
  - This method will be called when the app is about to terminate.
    
### `applicationDidReceiveMemoryWarning(_:):`
  - This method is called when the system issues a memory warning to the app due to low memory conditions.
  - You can release the unnecessary memory and resources to prevent the app from being terminated.

### [What's the difference between AppDelegate and SceneDelegate?](https://github.com/chihyinyang/InterviewFQA/blob/main/SceneDelegate.md)

  
<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Optional

An optional is a way to handle a variable that mighe be empty. It adds a question mark to the variable's type, indicating the possibility to be nil.

To work with optional value, there were two safe way we can obtain the value: Optional chaining and Conditional binding. 

It is important to note that force unwrapping is unsafe way to get the value. It would cause a crash when you try to get the value from the variable, but the variable is empty.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## @escaping

### What's the difference between an @escaping and a non-@escaping closure?

The difference between an @escaping and a non-@escaping closure is depends on how the closure is used and its lifetime.

#### non-@escaping closure
non-@escaping closure is the default behaviour in Swift. It is a closure that is guaranteed to be executed before the enclosing function returns. It means that the closure is synchronous and doesn't outlive the function itself.

#### @escaping closure
@escaping closure is a closure that can outlive the function, it means it can be stored or assign to a varibles. @escaping closure typically used when you want to capture the closure.

#### Key Diff
The key difference lies in how the closure is treated by the complier. For non-@escaping closures, the compiler can make certain optimazations since it know the closure will not outlive the function. In constrast, @escaping closure requires addtional considerations by the compiler to ensure the capured values retained and the closure is available when needed. 



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Struct vs Class

### What is the difference between struct and a class in Swift?

#### Struct
Struct is value type, and it doesn't support inheritance. And they are allocated on the stack, they are deallocated automatically when that go out of scope.

#### Class
Class is reference type, and it support inheritance, and they're stored on the heap and require memory management using ARC. The memory is dellocated when there are zero reference to the instance.

#### Which one is better?
Choosing between a Struct and a Class depends on the specific use case and requirements. Struct are suitable for small, simple, and immutable data structure, while classes are preferred for more complex objects that require reference semantics, inheritance, and more advanced features.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Value Type vs Reference Type

### What's the difference between a value type and a reference type?

#### Value Type
A value type is a type that is copied when assigned to a new variable or passed as a function argument. Modifying a copy of a value type does not affect to the original instance. Examples of value type in Swift include struct, intergers, string and enum.

#### Reference Type
A reference type is a type that is passed by reference. When assigned to a new variable or passed as an argument, a reference to the exsiting instance is created, and both variable point to the same underlying object in memory. Modifying a reference type affect all variables that reference the same object. Examples of reference type in Swift include Class, closure.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## State Variable

When you declare a property or method as `state`, it means there is only one copy of that property or method shared across all instances of the class or struct, and you can access it directly through the type itself.

### Static Property
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

  
<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Object-Oriented Programming

In OOP, software is designed and organized using objects, which are instances of classses representing real-world entities or concerpts.

### Key Principles:

#### 1. Encapsulation
Encapsulation is the binding of data and methods into one entity to define itself and the scope of its operations. The bundling of data and methods into individual entities hides complexity by providing abstracted interface to program and interact with. The most common example of such a unit would be a class/object setting. 

#### 2. Abstraction
Abstraction focus on representing the essential features of an object while hiding the unnecessary details. Swift Example: Protocol

#### 3. Inheritance
Inheritance enables a class to inherit properties and behavious from another class. This promotes code reuse and hierarchical relationships between classes.

#### 4. Polymorphism
Polymorphism allows objects of different classes to be treated as objects of a common superclass. It enables a single interface to represent multiple underlying data types, providing flexibility and extensibility in the code.

### Benefits:
- Modularity
- Reusability
- Maintainability
- Flexibility
- Scalability


  
<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Protocol-Oriented programming

Protocol-Oriented Programming is a programming paradigm that emphasizes the use of protocols to define interfaces and behaviour, promoting code reuse and flexibility.

### Key Concepts:

#### 1. protocol
A protocol in Swift like as a blueprint defining a set of methods, properties, and other requirements. These requirements act as a contract that any class, struct, or enum adopting the protocol must fulfill.

#### 2. Protocol Adoption
A class, struct, or enum can adopt a protocol by declaring that it conforms to it.

#### 3. Protocol Extensions
Protocols can be extended to provide default impletmentations for some of their requirments.

#### 4. compositions
Code reuse is achieved through composition rather than inheritance. Instead of using subclassing, you create small, modular protocols and then compose types by conforming to multiple protocols.

### Benefits:
- Code Reusability
- Multiple Inheritance
- Protocol Extensioins
- Testability



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## SOLID Principles

### Single responsible
Responsible for one

### Open-closed
Open to expand, close to modification

### Liskov substitution 
Define that object of a superclass should be replaceable with object of its subclass without breaking the application

### Interface segregation 
No code should be force to depend on method it doesn’t use.

### Dependence inversion
High level should not import anything from low-level modules. Both should depend on abstractions



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>




## Unit Test

The purpose of unit testing is to ensure that each unit of code functions as intended and to catch and fix bugs early in the development process.

### Key Purposes:
1. Isolation:
   Unit tests isolate specific piece of code, allowing us to verify the functionality of each unit independently.
   -> This makes it easier to identify and fix issue.

2. Early Bug Detection



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## UI Test

Unlike unit tests that test individual components in isolation, UI tests interact with the application as a whole, simulating user interactions to verify that the ui behaves correctly.

### Key Purposes:
1. User Experience Validation
2. Platform Consistency
3. Automated Validation

### Things to notice in UI testing:
1. Ensure that the test environment is setup with necessary test data.
2. Ansnchronous Operations, some UI interactions and actions may take time to complete.


   
<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>




## Access Control

What's the difference between open and public?

### open: 
This is the highest level of access and allows entities to be subclassed and overridden outside the module where they are defined. It is typically used for framework or library developers who want to allow other developers to subclass and modify their classes or override their methods. open entities can be accessed and modified from any module.

### public: 
This level of access allows entities to be accessed from any module but does not allow subclassing or overriding outside the module where they are defined. public entities can be used and accessed by other modules, but they cannot be subclassed or overridden in those modules.

### To summarise
Open provides the broadest level of access, allowing subclassing and overriding from outside the module, while public provides access to entities from other modules but restricts subclassing and overriding to



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Dependency Injection

In DI, instead of components creating or obtaining their dependencies internally, the dependencies are provided from external sources. This external source, often called the "dependency injector”, is responsible for creating and managing the dependencies.  

Overall, Dependency Injection promotes decoupling, flexibility, and maintainability in software systems by separating the responsibility of managing dependencies from the components themselves.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Approach for Data Persistence

### coreData
Core Data is object-oriented, which makes it easy to store and manage complex data models. Core Data also provides a number of features that make it easy to query and update data, such as predicates and fetch requests.

### UserDefaults
UserDefaults is a simple key-value store that is used to store small amounts of data in iOS apps. UserDefaults is easy to use, but it is not as powerful as Core Data. UserDefaults also does not provide any features for querying or updating data.

## Singleton

Singleton is a design pattern that used to make sure that a class has only one instance. I usually use it as a user information manager, to make sure the state of user stay updated. I would create a class and create a private let property to store the instance of the class. And then make its init privately, to make sure there would never be second instance.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Trouble Shooting

### How do you debug and troubleshoot issues in an iOS app? Explain the tools and techniques you would use.

Logging is the most common way to identify potential problems, and breakpoint would come alone the way, print out the statements also give a lot of help, but I think the most efficient way for detecting UI error is using simulator.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Retain Cycle

### Can you explain what a retain cycle is? 

A retain cycle happens when two or more objects hold strong references to each other, creating a circular dependency. As a result, the reference count for each object never reaches zero, preventing them from being deallocated. This can lead to memory leaks and consume more memory than necessary.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Strong, Weak, Unowned

### Strong References:
Strong references increase the reference count of an object, keeping it alive in memory as long as there is at least one strong reference to it.
Use strong references when you want to ensure that an object remains in memory as long as it is needed.

### Weak References:
Weak references do not increase the reference count of an object. They are typically used to avoid strong reference cycles (retain cycles) and prevent memory leaks.  

Use weak references when you want to establish a relationship where the referenced object may become deallocated at some point, and you don't want to keep it alive artificially.  

Weak references are automatically set to nil when the referenced object is deallocated.

### Unowned References:
Unowned references are similar to weak references in that they do not increase the reference count. However, unowned references are assumed to always have a valid value.  

Use unowned references when you are confident that the referenced object will not be deallocated as long as the unowned reference exists.
Unlike weak references, unowned references are not optional types and should be used with caution. Accessing an unowned reference after the referenced object is deallocated leads to a runtime crash.

Choosing between strong, weak, and unowned references depends on the relationship and ownership between objects. Use strong references when you want to ensure an object remains in memory as long as it is needed.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>



## Automatic Reference Counting

### Reference Counting:
ARC keeps track of the number of references to each object using a reference count. It increments the count when a new reference is created and decrements it when a reference is no longer used.

### Retain and Release:
When an object is assigned to a new variable or stored in a collection, ARC automatically increases its reference count.  
	
 When a reference to an object is no longer needed, ARC automatically decreases its reference count.
 
### Automatic Deallocation:
When the reference count of an object reaches zero, meaning there are no more references to it, ARC automatically deallocates the object's memory.  

Deallocation triggers the object's deinitializer to perform any necessary cleanup.

### Strong and Weak References:
Objects can have strong or weak references.

Strong references increase the reference count and ensure that the object remains in memory as long as there is at least one strong reference to it.  

Weak references, on the other hand, do not increase the reference count. They allow objects to be deallocated when there are no strong references remaining.

### Avoiding Retain Cycles:
Retain cycles occur when objects hold strong references to each other, forming a reference cycle that prevents deallocation.  

To avoid retain cycles, ARC provides the weak and unowned reference types to create non-owning references between objects.



<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>


## Frame VS Bounds

### bounds: 
Represents the view's internal coordinate system, relative to its own origin (0,0). Used for drawing and layout within the view itself.  

The bounds property is especially useful when working with view drawing, animations, and transformations within the context of the view itself, without affecting its position and size within the superview.

### frame: 
Represents the view's position and size relative to its superview's coordinate system. Used to position and size the view within its superview.


<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>


## Combine

### That is Combine, and what problem does it solve?
Combine is a framework in Swift that provides a declarative API for processing asynchronous and event-driven code. It simplifies handling asynchronous operations, managing data flow, and responding to events over time.

### What are the main components of Combine?
The main components of Combine are Publishers, Subscribers, and Operators. Publishers emit a sequence of values over time, Subscribers receive and react to those values, and Operators are used to transform, filter, or combine the emitted values.

### How do you create a Combine Publisher?
You can create a custom Publisher by implementing the Publisher protocol. A simple example could be a custom publisher that emits a sequence of integers.

### What is the difference between a cold and hot Combine Publisher?
A cold publisher starts emitting values when a Subscriber subscribes to it, while a hot publisher emits values regardless of whether any Subscribers are listening.

### What are Operators in Combine, and how do they transform data?
Operators in Combine are methods that modify or combine values emitted by Publishers. For example, map transforms each value emitted by a Publisher, while combineLatest combines values from multiple Publishers into a tuple.

### What is backpressure, and how does Combine handle it?
Backpressure is a mechanism to handle overwhelming data flow when the Subscriber cannot keep up with the emitted values. Combine handles backpressure using strategies like .buffer, .drop, and .latest.

### What is the purpose of Subjects in Combine?
Subjects act as both Publishers and Subscribers. They can be used to inject values into a Combine pipeline, making them useful for bridging with imperative code or handling user inputs.

### How do you handle errors in Combine?
Errors in Combine are propagated downstream to Subscribers. You can handle errors using the catch operator to recover from an error or replace it with a default value.

### How can you handle multiple Combine subscriptions and cancellations?
To handle multiple subscriptions and cancellations in Combine, you can use cancelables, store(in:), or the Cancellable protocol to clean up subscriptions when they are no longer needed.
Explain the concept of Combine's Scheduler and how it affects data processing.
Combine's Scheduler determines the execution context for a Publisher's emissions and Subscribers' actions. Different Schedulers allow you to control when and where work is performed.

### How can you test Combine code?
Combine code can be tested using XCTest along with XCTestExpectation for asynchronous testing. Additionally, TestScheduler from Combine can be used to control the timing of events during testing.

### What are some common memory management issues related to Combine?
Common memory management issues include creating retain cycles when capturing self in Combine closures. Proper use of unowned, weak, and unowned(unsafe) is essential to avoid memory leaks.

### Can Combine replace other asynchronous programming paradigms in Swift, like DispatchQueue and delegation?
Combine can complement and, in some cases, replace other asynchronous paradigms, but it depends on the specific use case and the complexity of the code.

### How do you handle cancellation and cleanup in Combine?
Combine's Cancellable protocol helps manage cleanup tasks when a subscription is canceled. It's crucial to properly handle cleanup to avoid resource leaks.

### What are some common use cases of Combine in real-world iOS apps?
Combine can be used for handling API requests, updating UI components based on data changes, form validation, reactive UI bindings, handling user interactions, etc.

<div align="right">
  <a href="#overview">⬆️ Back to Overview</a>
</div>


