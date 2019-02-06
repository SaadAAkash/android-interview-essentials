# Kotlin-Android

## Java/OOP in General

* How does Thread communicate? - Threads communicate in 3 ways: ```wait()```, ```notify()```, ```notifyAll()```
* What's the access modifier of a method that no child class can extend/access/override: final
* Interface VS Abstract: Interface can have only abstract methods. Abstract class can have both abstract and non-abstract methods.  Variables declared in a Java interface are by default final. Abstract class can have final, non-final, static and non-static variables. Interface has only static and final variables.


## Android

* Context is the Interface to global information about an application environment.
* An Activity is an application component that provides a screen, with which users can interact in order to do something.
* A Fragment represents a behavior or a portion of user interface in an Activity
* A fragment has to live inside the activity. Fragments do not need to be declared in the manifest.
* Fragments are used for its re-usability. For multi-pane layouts you have to use fragment that you can't achieve with activity. Use fragment only when you’re working with UI components or behavior that you’re going to use across multiple activities.
* A service is a component that runs in the background to perform long-running operations without needing to interact with the user and it works even if application is destroyed
* Explicit intents are used to start components in your own application (startnewactivty, start another class), 
* And Implicit intents are most commonly used to communicate with components from other third party applications (call, sms, mail)

## MVVM

* ViewModel: While you're rotating the screen orientation or perform any changes in configruation, data may be lost (i.e. while filling up a google form activity & changing the rotation on device)
* ViewModel prevents memory leak, by hodling the data of UI.
* While fetching data from some API, some data can come after the initilization of the activity & its view.
* LiveData, an observer class, detects & changes the data in the UI if there's any change. LiveData is a data wrapper class, which is observable within a Lifecycle of Activity, Fragment, meaning that the observers are going to be notified only when the Activity or Fragment it’s active.
* When data is ready on the VM side, it’s time to wrap it in LiveData object using MutableLiveData
* Unlike the Presenter, VM is automatically retained on configuration changes with the help of ViewModelProviders, and finished only when Activity finishes or Fragment gets detached without saving state.
 
## Kotlin
