## What's the difference between AppDelegate and SceneDelegate?

### AppDelegate:
AppDelegate is the main entry point for the app and has been present since the earlier versions of iOS.
It is responsible for managing the overall lifecycle of the app, including launching, backgrounding, terminating, and handling app-level events like push notifications and app state changes.

In AppDelegate, you typically set up the initial configuration of the app, register for remote notifications, handle app-wide URL schemes, and manage tasks that should occur when the app is in the foreground or background.

### SceneDelegate:
SceneDelegate was introduced in iOS 13 to manage multiple scenes within the app, especially on iPads and iPhones that support multiple windows.
A scene represents an instance of the app's user interface, and a single app can have multiple scenes running concurrently.

The SceneDelegate is responsible for configuring and managing the UI for each scene and responding to specific scene-related events, such as when a new scene is created, when a scene becomes active or inactive, or when a scene is about to be terminated.

It is in SceneDelegate where you set up the initial UI components for each scene, respond to user interactions, and handle the state transitions of individual scenes.

### In summary, the key difference between AppDelegate and SceneDelegate lies in their responsibilities:

#### AppDelegate: 
Handles the app's overall lifecycle, app-level events, and tasks that should occur irrespective of specific UI instances or scenes.

#### SceneDelegate: 
Manages individual instances of the app's user interface (scenes), including setting up the initial UI and responding to scene-specific events.
As a developer, you can leverage both files to control the behavior of your app at different levels. However, it's crucial to keep in mind that the responsibilities of these files are distinct, and actions related to the app's lifecycle and overall configuration should be placed in AppDelegate, while actions specific to user interface setup and scene management should be placed in SceneDelegate.



From: ChatGPT
