<h2 style="margin-bottom: 0;" align="center">Android Interview Essentials</h2>
<h4 style="margin-top: 0;" align="center">Language Basics, Architecture In-depth, Android Vitals, Performance, Memory Optimizations and More</h4>
<p align="center">
	<a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-blue.svg"/></a>
	<a href="https://github.com/SaadAAkash/Native-Android-Interview-Basics"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg"/></a>
	<a href="https://github.com/SaadAAkash/Kotlin-Android-Interview-Basics/commits/master"><img src="https://img.shields.io/badge/Maintained%3F-yes-green.svg"/></a>
	<a href="https://github.com/SaadAAkash/Kotlin-Android-Interview-Basics/tree/master#license"><img src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103"/></a>
	<a href="https://saad.ninja"><img src="https://img.shields.io/badge/Made%20with-Love-1f425f.svg"/></a>
	<br> <br>
	
<a href="https://undraw.co/" target="_blank">
         <img src="https://github.com/SaadAAkash/Kotlin-Android-Interview-Basics/blob/master/resources/banner.jpg" alt="Native Android Interview Basics" style="width:200;height:200">
</a>


## Contents

| 1 | 2 | 3 | 4 | 5 | 6 |
| -------- | --------- | --------- | --------- | --------- | --------- |
| [Android Basics](README.md#android-basics) | [Android Specifics: Native](#android-specifics-native) | [Android Specifics: Cross-Platform](#android-specifics-cross-platform) | [Android Intermediate](#android-intermediate) | [Android Advanced](#android-advanced) | [Resources & Learning Guides](#resources-and-learning-guides) |

# Android Basics

<details>
<summary><strong>What are the core 4 app components? What elements/tags do we use to declare them in the Manifest file?</strong></summary>

There are four different types of app components:

* Activities
* Services
* Broadcast receivers
* Content providers

To declare all app components, we use the following elements:

* `<activity>` elements for activities.
* `<service>` elements for services.
* `<receiver>` elements for broadcast receivers.
* `<provider>`elements for content providers.
</details>

<details>
<summary><strong>What's Context?</strong></summary>
Context is the Interface to global information about an application environment
</details>

<details>
<summary><strong>What's an Activity?</strong></summary>
An Activity is an application component that provides a screen, with which users can interact in order to do something
</details>

<details>
<summary><strong>What's a Fragment? What's its relationship with Activity?</strong></summary>
A Fragment represents a behavior or a portion of user interface in an Activity. A fragment has to live inside the activity. Fragments do not need to be declared in the manifest.
</details>

<details>
<summary><strong>What's the use of Fragment?</strong></summary>
Fragments are used for its re-usability. For multi-pane layouts you have to use fragment that you can't achieve with activity. Use fragment only when you’re working with UI components or behavior that you’re going to use across multiple activities
</details>

<details>
<summary><strong>What's a Service?</strong></summary>
A service is a component that runs in the background to perform long-running operations without needing to interact with the user and it works even if application is destroyed
</details>

<details>
<summary><strong>What's an Intent? How many types of intent are in Android? Briefly explain their respective use cases.</strong></summary>

An Intent is a messaging object you can use to request an action from another app component.

Use Cases: Starting an Activity or a Service, Delivering a broadcast. 
* <b>Explicit intents</b> are used to start components in your own application. Use Case: You might start a new activity within your app in response to a user action, or start a service to download a file in the background.
* <b>Implicit intents</b> are most commonly used to communicate with components from other third party applications.  Use Case: If you want to show the user a location on a map, you can use an implicit intent to request that another capable app show a specified location on a map.

</details>

<details>
<summary><strong>What's a PendingIntent? How many types of intent are in Android? Briefly explain their respective use cases.</strong></summary>

A PendingIntent object is a wrapper around an Intent object. The primary purpose of a PendingIntent is to grant permission to a foreign application to use the contained Intent as if it were executed from your app's own process.

Use Cases: 
* Notification: Android system's NotificationManager executes the Intent
* App Widget: Home screen app executes the Intent
* A specified future time: Android system's AlarmManager executes the Intent

</details>

<details>
<summary><strong>What is the functionality of Intent filters? Point out a frequently-used scenario.</strong></summary>

This element is used in the Manifest file to declare the capabilities of an app component (i.e. an Activity) 

Use Case:
When we declare an Activity in the Manifest, we can include intent filters so it can respond to intents from other applications like the following:

```xml
<manifest>
    ...
    <application>
        <activity android:name="com.example.SendEmailActivity">
            <intent-filter>
                <action android:name="android.intent.action.SEND" />
                <data android:type="*/*" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

</details>

<details>
<summary><strong>What are the core components of RecyclerView?</strong></summary>

* RecyclerView.Adapter
* RecyclerView.ViewHolder
* RecyclerView.LayoutManager
* RecyclerView.ItemAnimator

</details>

<details>
<summary><strong>What are the functionalities/use cases of using Guideline & Barries in a ConstraintLayout?</strong></summary>

Link to the resources with graphical explanation:

* [Constrain to a guideline](https://developer.android.com/training/constraint-layout#constrain-to-a-guideline)
* [Constrain to a barrier](https://developer.android.com/training/constraint-layout#constrain-to-a-barrier)

</details>

<details>
<summary><strong>Which method is called only once in a fragment life cycle?</strong></summary>
onAttached()
</details>



# Android Specifics: Native

### Android Specifics: Kotlin

<details>
<summary><strong>How many visibility modifiers are there in kotlin? Explain their scope</strong></summary>  

There are 4 visibility modifiers in Kotlin:

* Public: Visible everywhere
* Protected: Not available for top-level declarations
* Internal: Visible everywhere in the same module (a module is a set of Kotlin files compiled together: IntelliJ IDEA, Gradle source set etc)
* Private: Only visible inside the file containing the declaration

```kotlin
class EventViewModel internal constructor()
```

In the previous code snippet, internal makes class available to public, but constructor only to inside module

</details>

<details>
<summary><strong>What are Companion Objects?</strong></summary>  

If you need a function or a property to be tied to a class rather than to instances of it, you can declare it inside a companion object. If you declare a companion object inside your class, you'll be able to call its members with the same syntax as calling static methods in Java/C#, using only the class name as a qualifier. It is similar to `static` keyword in Java or `@staticmethod` in Python.

```kotlin
companion object {
@Volatile private var instance: EventRepository? = null

fun getInstance(eventDao:EventDao) =
  instance ?: synchronized(this) {
      instance ?: EventRepository(eventDao).also { instance = it }
  }
}
```
   
</details>

<details>
<summary><strong>Give the output of the following code with nullable variables</strong></summary>

```kotlin
var a: String = "abc"
a = null 
var b: String? = "abc"
b = null 
print(b)
```

* `a =null` will produce a compilation error
* `b = null` will not produce any error

</details>

<details>
<summary><strong>What's a Safe call operator?</strong></summary>

```kotlin
val a = "Kotlin"
val b: String? = null
println(b?.length) //prints null
println(a?.length) //prints 6
```

</details>
 
<details>
<summary><strong>Explain !! VS ? in the following cases</strong></summary>  

A quick Overview of some possible cases:

| 1 | 2 | 3 | 4 | 
| -------- | --------- | --------- | --------- | 
| a: String? | a.length | a?.length | a!!.length | 
| "cat" | Compile time error | 3 | 3 |
| null | Compile time error | null | NullPointerException |
   
!! is an option for NPE-lovers. ```a!!.length``` will return a non-null value of a.length or throw a NullPointerException if a is null. And ```a?.length``` returns a.length if a is not null, and null otherwise:

```kotlin
val a: String? = null
print(a!!.length) // >>> NPE: trying to get length of null
```

```kotlin
val a: String? = null
print(a?.length) // >>> null is printed in the console
```

</details>
   
<details>
<summary><strong>What's the ternary operator (condition ? expression1 : expression2;) of Java alternative in Kotlin?</strong></summary>  
Unlike Java, there is no ternary operator in kotlin. You need to use if-else instead.
</details>

<details>
<summary><strong>What's an Elvis Operator? Why is it a Smarter Type-Safe If</strong></summary>  

```
val list = mutableList ?: mutableListOf() 
```
is a shorter form of
```
val list = if (mutableList != null) mutableList else mutableListOf()
```

The name,howver, comes from the famous American singer Elvis Presley. His hairstyle resembles a Question Mark [Ref](https://stackoverflow.com/questions/48253107/what-does-do-in-kotlin/48304523#48304523)

![alt text](https://i.stack.imgur.com/bVG64.png "Elvis Operator")

</details>

<details>
<summary><strong>Given the 2 code snippets, choose which one is more preferred.</strong></summary>  

1st Code Snippet:

```kotlin
return if (x) foo() else bar()
return when(x) {
    0 -> "zero"
    else -> "nonzero"
}
```

2nd Code Snippet:

```kotlin
if (x)
    return foo()
else
    return bar()

when(x) {
    0 -> return "zero"
    else -> return "nonzero"
}
```

The above is preferable to the latter one.

</details>

<details>
<summary><strong>What does the keyword/block init do?</strong></summary>  

Out Initialization code can be placed in initializer blocks, which are prefixed with the ```init``` keyword:

```kotlin
class InitOrderDemo(name: String) {
    val firstProperty = "First property: $name".also(::println)  //inits a val & also, prints the name

    init {
	println("First initializer block that prints ${name}")
	println("Second initializer block that prints ${name.length}")
    }
}
```
</details>

<details>
<summary><strong>How to call a High Order Functions in Kotlin?</strong></summary>  

```kotlin
fun main() {
//both of the ways are correct!
    test( { println(it) } ) 
    test(::println)
}

fun test(block: (String) -> Unit ) {
    block("okay")
}
```

</details>

<details>
<summary><strong>What does @Volatile mean?</strong></summary>  

`@Volatile` before a field means that writes to this field are immediately made visible to other threads.

</details>

<details>
<summary><strong>Why do we need to use @Suppress("UNCHECKED_CAST")?</strong></summary>  

In Kotlin, there's no way to check the generic parameters at runtime in general case (like just checking the items of a ```List<T>``` or here in this ViewModelFactory, ```modelClass: Class<T>``` which is only a special case), so casting a generic type to another with different generic parameters will raise a warning, which needs to be suppressed

```kotlin
@Suppress("UNCHECKED_CAST")
override fun <T : ViewModel?> create(modelClass: Class<T>) = EventViewModel(eventRepository, lifecycleOwner) as T
```
  
</details>

<details>
<summary><strong>How to use Bitwise Operator in Kotlin?</strong></summary>  

```kotlin
val andResult  = a and b
val orResult   = a or b
val xorResult  = a xor b
val rightShift = a shr 2
val leftShift  = a shl 2
```
</details>


<details>
<summary><strong>What's reified keyword in Kotlin?</strong></summary>  

Generic parameters are a great way to provide type safety, but can be limiting when accessing class info type. 
The `reified` keyword allows get type of generic variable in inline function.

```kotlin
inline fun <reified T> printType() {
	print(T::class.java)
}

fun printStringType() {
        //calling with String type  
	printType<String>()
}
```

Some rules to follow:

* Reified can be used only with inline functions
* Reified functions can not be accessed from Java, because Java doesn't support inlining

More on [Reified](https://www.youtube.com/watch?v=Xj45hobMI78) and [Inline functions](https://www.youtube.com/watch?v=wAQCs8-a6mg) on Kotlin Vocabulary
</details>

<details>
<summary><strong>What are the differences among flatMap(), map() and flatten() in Kotlin? Explain with code example.</strong></summary>  

* `flatMap()` merges two collections into a single one 
* `map()` results in a list of lists
* `flatten()` produces the same result as `flatMap()`. So `flatMap()` is a combination of the two functions: `map()` and then `flatten()`

The following code example with commented output illustrates their use cases:

```kotlin
class Data(val items : List<String>)

val dataObjects = listOf(
    Data(listOf("a", "b", "c")), 
    Data(listOf("1", "2", "3"))
)

val items: List<String> = dataObjects.flatMap { it.items } //[a, b, c, 1, 2, 3]
val items2: List<List<String>> = dataObjects.map { it.items } //[[a, b, c], [1, 2, 3]] 

val nestedCollections: List<Int> = listOf(listOf(1,2,3), listOf(5,4,3)).flatten() //[1, 2, 3, 5, 4, 3]
```

</details>


### Android Specifics: Java

<details>
<summary><strong>What's the access modifier of a method that no child class can extend/access/override?</strong></summary>
	
`final`
</details>


<details>
<summary><strong>What's the instantiation and initialization of an object?</strong></summary>
	
* Initialization: is the process of the memory allocation, when a new variable is created.
* Instantiation: is the process of explicitly assigning definitive value to a declared variable.
   
</details>


<details>
<summary><strong>Are static local variables allowed in Java?</strong></summary>

No. In Java, a static variable is a class variable (for whole class). So if we have static local variable (a variable with scope limited to function), it violates the purpose of static. Hence compiler does not allow static local variable. So the following code throws a `Error: Static local variables are not allowed`:

```java
class Test { 
   public static void main(String args[]) {  
     System.out.println(fun()); 
   } 
  
   static int fun() 
   { 
     static int x= 10;  //throws an error here
     return x--; 
   } 
}  
```

</details>

<details>
<summary><strong>Can we access a non-static variable from a static method in Java?</strong></summary>
No. The concept of static is not associated with any instance. And non-static variable are associated with a specific instance of an object.
</details>

<details>
<summary><strong>Can a static method be overridden in Java?</strong></summary>
No. Method overriding is based on dynamic binding at runtime and the static methods are bonded using static binding at compile time.
We can declare static methods with the same signature in the subclass, but it is not considered overriding as there won't be any run-time polymorphism. 
</details>

<details>
<summary><strong>How to make a member variable not to be serialized inside a Serialized object?</strong></summary>

Using Java keyword `transient`. This keyword, when applied to a field, tells the Java object serialization subsystem to exclude the field when serializing an instance of the class

</details>

<details>
<summary><strong>What's the Parent class of Error & Exception?</strong></summary>
Throwable
</details>

<details>
<summary><strong>What is a Generic in Java?</strong></summary>
Generics is parameterized types (Integer, String, … etc, and user-defined types) to methods, classes, and interfaces. Generics is used to create classes that work with different data types as such:
	
```java
class Test<T> 
{ 
    T obj; 
    Test(T obj) {  this.obj = obj;  } 
    public T getObject()  { return this.obj; } 
} 

class Main 
{ 
    public static void main (String[] args) 
    { 
        Test <Integer> iObj = new Test<Integer>(15); 
        System.out.println(iObj.getObject()); 
	
        Test <String> sObj = new Test<String>("GeeksForGeeks"); 
        System.out.println(sObj.getObject()); 
    }
}
```
</details>

<details>
<summary><strong>What is the difference between == and .equals()?</strong></summary>

* The `equals()` method compares two strings, character by character, to determine equality
* The `==` operator checks to see whether two object references refer to the same instance of an object

</details>

<details>
<summary><strong>Are String objects mutable? If so, why is that? Explain shortly.</strong></summary>
No. String objects are immutable. In the String constant pool, a String object is likely to have one or many references. If several references point to same String without even knowing it, it would be bad if one of the references modified that String value. That's why String objects are immutable.
</details>

<details>
<summary><strong>When to use StringBuffer and when to StringBuilder?</strong></summary>
	
StringBuffer and StringBuilder are classes used for String manipulation. These are mutable objects, which provide methods such as `substring()`, `insert()`, `append()`, `delete()` for String manipulation. They are similar, but StringBuilder is faster and preferred over StringBuffer for single threaded program. However, StringBuilder operations are not thread-safe are not-synchronized. So StringBuffer is preferred over StringBuilder when thread safety is required.

</details>

<details>
<summary><strong>How many types of polymorphism is there in Java?</strong></summary>
	
There are two types of polymorphism in Java: 

* **Compile-time polymorphism**: Compiler itself determines which method should call. Method overloading is an example of static/compile-time polymorphism. 
* **Runtime polymorphism**: Compiler cannot determine the method at compile time. Method overriding is an example of dynamic/run-time polymorphism 

</details>

<details>
<summary><strong>Which class is widely used to implement thread safe counters in Java?</strong></summary>
	
[AtomicInteger](https://developer.android.com/reference/java/util/concurrent/atomic/AtomicInteger)

</details>



# Android Specifics: Cross-Platform

### Android Specifics: Flutter

<details>
<summary><strong>What is the difference between StatelessWidget and StatefulWidget?</strong></summary>
	
If a widget can change when a user interacts with it, it’s stateful. If it can't, it's stateless.

* StatelessWidget is an immutable class that acts as a blueprint for some part of the UI layout. You use it when the widget doesn’t change while displaying and, therefore, has no State
* StatefulWidget is also immutable, but it’s coupled with a State object that allows you to rebuild the widget with new values whenever calling setState(). Use StatefulWidget whenever the UI can change dynamically

</details>

<details>
<summary><strong>Give some frequently used Stateless and Stateful widgets</strong></summary>
	
* Stateless: `Icon`, `IconButton`, and `Text`
* Stateful: `Checkbox`, `Radio`, `Slider`, `InkWell`, `Form`, and `TextField`

</details>

<details>
<summary><strong>Explain the difference between hot reload and hot restart briefly</strong></summary>
	
* Hot reload maintains the app state while updating the UI almost instantaneously
* Hot restart resets the app state to its initial conditions before updating the UI

Hot Restart takes a bit longer than Hot Reload, in comparison

</details>

<details>
<summary><strong>What is BuildContext and how is it useful?</strong></summary>
	
`BuildContext` is the widget's element in the Element tree. Every widget has its own BuildContext. It's used to get a reference to the theme or to another widget.

</details>

<details>
<summary><strong>How to decrease/optimize the iterations of rebuilding stateful widgets?</strong></summary>
	
* Creating dedicated smaller widgets that updates states instead of handling states on larger widgets
* Factoring out only the stateful part of a widget and passing a child argument to it
* Using `const` widgets to cache and reuse
* Avoiding frequent changes of the depth of the subtree since it requires rebuilding

More technique on [official doc on Perfomance Considerations on Flutter](https://api.flutter.dev/flutter/widgets/StatefulWidget-class.html#performance-considerations)

</details>


<details>
<summary><strong>Name some of the steps of StatefulWidget lifecycle.</strong></summary>
	
* createState()
* mounted == true
* initState()
* didChangeDependencies()
* build()
* didUpdateWidget()
* setState()
* deactivate()
* dispose()
* mounted == false

More in-depth analysis of every step on the following [aticle](https://flutterbyexample.com/lesson/stateful-widget-lifecycle)

</details>






# Android Intermediate

### General Concepts

<details>
<summary><strong>We know that when one activity starts another, they both experience lifecycle transitions. Briefly explain the order of operations that occur when Activity A starts Activity B.</strong></summary>
	
* Activity A's `onPause()` method executes.
* Activity B's `onCreate()`, `onStart()`, and `onResume()` methods execute in sequence. (Activity B now has user focus.)
* Then, if Activity A is no longer visible on screen, its `onStop()` method executes.

</details>

<details>
<summary><strong>What type of stack does Android use for managing tasks?</strong></summary>
	
Android manages tasks and the back stack, by placing all activities started in succession in the same task and in a *Last In First Out* (LIFO) stack
</details>

<details>
<summary><strong>What are the 3 principal intent flags for managing tasks in Activity Back Stack?</strong></summary>

* `FLAG_ACTIVITY_NEW_TASK`
* `FLAG_ACTIVITY_CLEAR_TOP`
* `FLAG_ACTIVITY_SINGLE_TOP`
	
[More explanation](https://developer.android.com/guide/components/activities/tasks-and-back-stack#IntentFlagsForTasks)
</details>

<details>
<summary><strong>On Android 10 or higher, how can an app start activities?</strong></summary>
	
By displaying notifications. But there are some exceptions and apps running on Android 10 or higher can start activities only when [one or more of these conditions](https://developer.android.com/guide/components/activities/background-starts#exceptions) are met.


</details>

<details>
<summary><strong>How to retrieve NavController in Java and Kotlin?</strong></summary>

You can retrieve a NavController by using one of the following methods:


* Kotlin:

```kotlin
Fragment.findNavController()
View.findNavController()
Activity.findNavController(viewId: Int)
```

* Java:

```java
NavHostFragment.findNavController(Fragment)
Navigation.findNavController(Activity, @IdRes int viewId)
Navigation.findNavController(View)
```

</details>

<details>
<summary><strong>What are the major components of Room?</strong></summary>

3 major components in Room:

* Database
* Entity
* DAO

</details>

<details>
<summary><strong>What's Scoped Storage in Android 10?</strong></summary>
	
Apps that use scoped storage have access only to their app directory on external storage plus any media the app created.
More details on this [article](https://www.raywenderlich.com/9577211-scoped-storage-in-android-10-getting-started).

</details>

<details>
<summary><strong>What's the improved data storage solution aimed at replacing SharedPreferences?</strong></summary>
Jetpack  DataStore
</details>

<details>
<summary><strong>When to use MutableLiveData & when to use LiveData? Explain a scenario.</strong></summary>
When you don't want your data to be modified use LiveData If you want to modify your data later use MutableLiveData. 
A scenario of fetching data from an API needs a MutableLiveData where there are changes in data. This fetched data then can be stored in a LiveData if there's no requirement to change it afterwards & just use cases of using it for the view purposes.
</details>

<details>
<summary><strong>When do we need a Parcelables and when a Bundle? Explain a scenario.</strong></summary>
Parcelables and Bundles are usually used to transfer data between activities. To transfer primitive data types we use Bundle and for complex object types we use Parcelable. 
In a scenario of sending a String from one activity to another a Bundle object can be used. But in case of sending an ArrayList, Bundle can not be used. In this case we need to use Parcelable.   
</details>

<details>
<summary><strong>What are sealed classes in Kotlin? Explain a possible use case in any of the RecylcerView components for Android.</strong></summary>

Sealed classes are used for representing restricted class hierarchies, when a value can have one of the types from a limited set, but cannot have any other type. 

They are, in a sense, an extension of enum classes: the set of values for an enum type is also restricted, but each enum constant exists only as a single instance, whereas a subclass of a sealed class can have multiple instances which can contain state.

A use case can be when to display a list of a specific type of object in a RecyclerView, where each object has its own ViewHolder.

```kotlin
sealed class Fruit {
    class Apple : Fruit()
    class Orange : Fruit()
}

class FruitAdapter : RecyclerView.Adapter<RecyclerView.ViewHolder>() {
    private val fruits = arrayListOf<Fruit>()
    override fun getItemCount() = fruits.size
        
    override fun getItemViewType(position: Int): Int {
        return when (fruits[position]) {
            is Fruit.Apple -> R.layout.item_apple
            is Fruit.Orange -> R.layout.item_orange
        }
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): RecyclerView.ViewHolder {
        val layoutInflater = LayoutInflater.from(parent.context)
        return when (viewType) {
            R.layout.item_apple -> {
                val itemView = layoutInflater.inflate(R.layout.item_apple, parent, false)
                AppleViewHolder(itemView)
            }
            R.layout.item_orange -> {
                val itemView = layoutInflater.inflate(R.layout.item_orange, parent, false)
                OrangeViewHolder(itemView)
            }
            else -> throw UnknownViewTypeException("Unknown view type $viewType")
        }
    }

    override fun onBindViewHolder(holder: RecyclerView.ViewHolder, position: Int) {
            val fruit = fruits[position]
            when (fruit) {
                is Fruit.Apple -> (holder as AppleViewHolder).bind(fruit)
                is Fruit.Orange -> (holder as OrangeViewHolder).bind(fruit)
            }
    }
}
```

</details>


### Common App Architectures

<details>
<summary><strong>What's the relation between using ViewModel and Memory Leak?</strong></summary>
While you're rotating the screen orientation or perform any changes in configruation, data may be lost (i.e. while filling up a google form activity & changing the rotation on device). ViewModel prevents memory leak, by hodling the data of UI.
</details>

<details>
<summary><strong>What's the use of LiveData? Explain a use case</strong></summary>
While fetching data from some API, some data can come after the initilization of the activity & its view. LiveData, an observer class, detects & changes the data in the UI if there's any change. LiveData is a data wrapper class, which is observable within a Lifecycle of Activity, Fragment, meaning that the observers are going to be notified only when the Activity or Fragment it’s active. If A is a LiveData instance and B is observing it, anytime A’s data changes, B is notified about this change and gets the latest value of A’s data.
</details>

<details>
<summary><strong>How is MVVM lifecycle aware & decoupled?</strong></summary>
Lifecycle awareness means that a LiveData will only update observers (such as Activities, fragments or services) which are in an active lifecycle state and thus, avoiding NPE. 
There is no reference to the View from a ViewModel so the communication between them must happen via a subscription. Hence, ViewModels expose events like openTaskEvent and views subscribe to them
</details>





# Android Advanced

<details>
<summary><strong>The last callback in the lifecycle of an activity is onDestroy(). The system calls this method on your activity as the final signal that your activity instance is being completely removed from the system memory. Usually, the system will call onPause() and onStop() before calling onDestroy(). Describe a scenario, though, where onPause() and onStop() would not be invoked.</strong></summary>
If you detect an error during onCreate() and call finish()
</details>

<details>
<summary><strong>When a LayoutManager asks a RecyclerView to provide a View at position X”, explain briefly the internal processes that take place.</strong></summary>
	
* Searches changed scrap
* Searches attached scrap
* Searches non-removed hidden views
* Searches the view cache
* If Adapter has stable ids, searches attached scrap and view cache again for given id
* Searches the ViewCacheExtension
* Searches the RecycledViewPool
* If it fails to find a suitable View in all of the aforementioned places, it creates one by calling adapter’s `onCreateViewHolder()` method. It then binds the View via `onBindViewHolder()` if necessary, and finally returns it

</details>

<details>
<summary><strong>Give me a scenario when onCreateViewHolder() & onBindViewHolder() needs to get called in a RecylerView?</strong></summary>
	
If a ViewHolder can not be found in Scrap, or Pool, or View Cache, RecyclerView calls its adapter's onCreateViewHolder() and then binds the created view by calling `onCreateViewHolder()` method.

</details>

<details>
<summary><strong>Give me a scenario when onCreateViewHolder() & onBindViewHolder() does not get called in a RecylerView? </strong></summary>

When a ViewHolder is in the view cache, we hope to to reuse it “as-is”, without rebinding, at the same position as the one it was at before it got into the cache.

</details>

<details>
<summary><strong>Give me a scenario when only onBindViewHolder() gets called in a RecylerView? </strong></summary>
If a ViewHolder was found in pool, it is bound.
</details>

<details>
<summary><strong>Suppose you have a News App that shows an Image with a text for each news article preview. It has 2 types of views implemented with RecyclerView. One view is a grid gallery of article previews & the other is a down-scroll feed of article previews. In which view may we need to extend RecyclerView's cache capacity?</strong></summary>
	
With the given scenario, it's assumable that users would not scroll up/go back to previously read articles too often. So we may need to extend the capacity of the cache in the latter as the grid needs to be updated more frequently.

</details>

<details>
<summary><strong>What method of a RecylerView do we need to call to detect if a certain View is present/visible on the device screen? </strong></summary>

`onViewAttachedToWindow()` and `onViewDetachedFromWindow()` callbacks of the RecyclerView's Adapter

</details>

<details>
<summary><strong>What's the difference between the activity lifecycle in a multi-windowed environment where multiple applications are running simultaneously in separate windows?</strong></summary>

There's no difference becaused multi-window mode does not change the activity lifecycle.

</details>

<details>
<summary><strong>Given a scenario of multiple apps running simultaneously in a multi-windowed environment, how to detect which of those application is on top of the other in the back stack of tasks?</strong></summary>

When apps are running simultaneously in a multi-windowed environment, supported in Android 7.0 (API level 24) and higher, the system manages tasks separately for each window; each window may have multiple tasks. Since it's managed by the System as a per-window basis, 2 applications in 2 windows are not in the same back stack of tasks in any way.

</details>

<details>
<summary><strong>What's the highest amount of data that you can keep as a savedInstanceState?</strong></summary>

For the specific case of `savedInstanceState`, the amount of data should be kept small because the system process needs to hold on to the provided data for as long as the user can ever navigate back to that activity (even if the activity's process is killed). Less than 50k of data in saved state is recommended. [Ref](https://developer.android.com/guide/components/activities/parcelables-and-bundles#sdbp)

</details>


<details>
<summary><strong>Name some of the types of Observables & Observers in RxJava??</strong></summary>

Types of Observables in RxJava:

* Observable
* Flowable
* Single
* Maybe
* Completable

Types of Observers in RxJava:

* Observer
* SingleObserver
* MaybeObserver
* CompletableObserver

</details>

<details>
<summary><strong>What's a Single, Maybe & Completable in RxJava??</strong></summary>

* A Single in RxJava is an Observable which emits only one item if completed or returns error.
* A Maybe in RxJava is used when the Observable needs to emit a value or a no value or an error.
* A Completable in RxJava is an Observable which just completes the task and does not emit anything if completed. It returns an error if anything fails. It is similar to reactive concept of runnable.

</details>

<details>
<summary><strong>What's the difference between Observable & Flowbale? What's Backpressure & how is it related to them?</strong></summary>

**Backpressure** is when your observable (publisher) is creating more events than your subscriber can handle. So you can get subscribers missing events, or you can get a huge queue of events which just leads to out of memory eventually. 

`Flowable` takes backpressure into consideration. `Observable` does not. 
</details>

<details>
<summary><strong>What's the difference between Lazy and Lateinit in Kotlin? Explain a use case & a code example where you illustrate what to use when.</strong></summary>

Comparison:
* `by lazy {...}` delegate can only be used for `val` properties, whereas `lateinit` can only be applied to `var` types
* `lateinit` var can be initialized from anywhere the object is seen from, wherease `by lazy {...}` can only be initialized from its initializer lambda 
* `by lazy {...}` is thread safe by default, it guarantees that the initializer is invoked at most once, whereas `lateinit` is not thread safe, the user is responsible for initialize in multi-thread inveronments

Use Cases:
* If you want your property to be initialized from outside/externally in a way probably unknown beforehand, use `lateinit`.
* If you want your property restrict to only using dependencies internal to your object, use `by lazy {...}`

Code example:
A code snippet where `lateinit` is allowed or not:

```
lateinit var name: String       //Allowed
lateinit val name: String       //Not Allowed in val
lateinit var name: String?      //Not Allowed if nullable
```

Here's a resourceful thread on [Stack Overflow](https://stackoverflow.com/questions/36623177/kotlin-property-initialization-using-by-lazy-vs-lateinit)
</details>





# Resources and Learning Guides

## Android Resources 

### Language/Framework Basics

* [Main Reference Guide](https://kotlinlang.org/docs/reference/)
* [From Java to Kotlin](https://github.com/MindorksOpenSource/from-java-to-kotlin)
* [Kotlin Tutorial Series Playlist by Navir Reddy](https://www.youtube.com/playlist?list=PLsyeobzWxl7rooJFZhc3qPLwVROovGCfh)
* [Understanding Kotlin Sealed Classes](https://proandroiddev.com/understanding-kotlin-sealed-classes-65c0adad7015)
* [Flutter Interview Questions and Answers - raywenderlich](https://www.raywenderlich.com/10971345-flutter-interview-questions-and-answers)

#### UI Components

* [Anatomy of RecyclerView: a Search for a ViewHolder](https://android.jlelse.eu/anatomy-of-recyclerview-part-1-a-search-for-a-viewholder-404ba3453714)
* [Anatomy of RecyclerView: a Search for a ViewHolder (continued)](https://android.jlelse.eu/anatomy-of-recyclerview-part-1-a-search-for-a-viewholder-continued-d81c631a2b91#.dcsykhoh9)

#### Best Practices/In-depth

* [Sunflower: A gardening app illustrating Android development best practices with Android Jetpack.](https://github.com/android/sunflower)
* [Understanding Types Of Observables In RxJava](https://blog.mindorks.com/understanding-types-of-observables-in-rxjava-6c3a2d0819c8)

#### LeetCode Resources

* [Read this before you start solving problems on Leetcode (Prep Work)](https://www.alimirio.com/posts/read-this-before-you-start-solving-problems-on-leetcode-prep-work)
* [Best Practice Questions on Leetcode](https://yangshun.github.io/tech-interview-handbook/best-practice-questions)
* [LeetCode Solution Explainer Videos by Nick White](https://www.youtube.com/playlist?list=PLU_sdQYzUj2keVENTP0a5rdykRSgg9Wp-)
* [LeetCode Java solutions by Fisher Coder](https://github.com/fishercoder1534/Leetcode)
