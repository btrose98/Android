# Android Lifecycles

## Activity Lifecycle:

onCreate:

    - Called as the first method when an activity is created. Only called once during the activity lifecycle.
    - Set the app screen content by using setContent.
    - Initialize state, class-scope variables,UI components and set event handlers (ie: click listeners).
    - Start a new Coroutine or set up data observers in the case of LiveData or Flow.

onStart:

    - Called when the activity is visible, but not interactive, to the user.
    - Check app permissions and send any prompts to the user.
    - Start animations/visual effects
    - Register listeners that are visible to the user

onResume:

    - Called when the user can interact with the activity.
    - Start any interactive processes (ie: ).
    - Resume any animations or threads that were paused in onPause.
    - Register any listeners that should be interactive to the user (ie: device sensor).

onPause:

    - Called when the system is about to resume a different activity or an interrupt event happens (ie: phone call).
    - Commit any unsaved changes.
    - Pause any ongoing actions that shouldn't continue while the activity isn't in the foreground.
    - Unregister any listeners that were registered in onResume.

onStop: 

    - Called when the activity is no longer visible to the user.
    - Release any expensive resources that are no longer needed because the app isn't visible (ie: ).
    - Save application state and user progress.
    - Unregister any listeners that were registered in onStart.

onDestroy:

    - Called when the activity is being destroyed (ie: Configuration change, app cleared from memory, etc.)
    - Final cleanup of resources (terminate threads, close database connections)
    - Release any resources created in onCreate.
    - Save any persistent state the activity should remember.
    - ** NOT GURANTEED TO BE CALLED BY THE SYSTEM **

![Android Activty Lifecycle](https://static.javatpoint.com/images/androidimages/Android-Activity-Lifecycle.png)

## Service Lifecycle

### Started vs Bound services

**Started**:

An application component (ie: Activity) calls startService(). Once started, a service can run in the background indefinitely, even if the component that started it is destroyed.

**Bound**:

An application component binds to the service by calling bindService(). A bound service offers a client-server interface that allows components to interact with the service, send requests, get results and even do so across processes with interprocess communication.

onCreate:

    - Called when the service if first created
    - Perform one-time setup procedures (ie: create data structures or start thread)

onStartCommand:

    - Called when the service is started (Component uses startService()).
    - Often, this is where the logic for the work the service is performing will be placed.

onBind:

    - Called when a component wants to bind with the service (Component uses bindService()).
    - bindService() returns an *instance of ServiceConnection* that serves as a client-side representation of the service and can be used to make public calls to the service.
    - This method must return an *IBinder*, which acts as an interface that the client uses to communicate with the service.

onUnbind:

    - Called when all clieants have disconnected from a particular interface published by the service.
    - Perform cleanup of resources related to the connections.

onRebind:

    - Called when new clients connect to the service, after having previously been notified that all had disconnected in onUnbind().

onDestroy:

    - Called when service is no longer used and is being destroyed.
    - Clean up any resources such as threads, registered listeners, receivers, heavy memory allocations, etc.


#### Additional Notes: ####
A service runs in the main thread of the hosting process, meaning it does NOT create it's own thread nor run in a seperate process. Therefore, if the service performs intensive or blocking operations, then a new thread should be created within the service.

![Android Service Lifecycle](https://androidclarified.files.wordpress.com/2017/07/service_lifecycle.jpg?w=636)

## Context

![Android Context](https://i.stack.imgur.com/00s1L.png)
