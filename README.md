# InterviewFQA

## Overview
- [viewController - life cycle](#viewControllerLifeCycle)
- [App - life cycle](App_-_life_cycle)
- Optional
- @escaping
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

### init
- where we create the viewController
- setup data (example: for the injection)
### LoadView
- ViewController creates its custom view hierarchy or a single root view that will act as the container for other subviews.
- Once the view hierarchy is created, the viewController sets it as te value of its `view` property using the `view` property setter.
### ViewDidLoad
- This method will be called once in vc life cycle when all views are loaded.
- Do the things that need to be done once.
  - network calls
  - user interface
### ViewWillAppear
### viewWillLayoutSubviews
### viewDidLayoutSubviews
### ViewDidAppear
### viewWillDisappear
### viewDidDisapppear
### deinit

### didReceiveMemoryWarning
### viewWillTransistion(to: with:)

<h2 name="appLifeCycle">App - life cycle</h2>

















