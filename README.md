# Kotlin-Android

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

* [Main Reference Guide](https://kotlinlang.org/docs/reference/)
* [From Java to Kotlin](https://github.com/MindorksOpenSource/from-java-to-kotlin)
* Declare a variable as nullable string (var_name?):

  ```
	var a: String = "abc"
	a = null // compilation error
	var b: String? = "abc"
	b = null // no error
	print(b)
  ```
 
* Safe call operator (?.)

  ```
	val a = "Kotlin"
	val b: String? = null
	println(b?.length)
	println(a?.length)

	output:
	null
	6 
   ```
* !! vs ? 

   ```
   	+------------+--------------------+---------------------+----------------------+
	| a: String? |           a.length |           a?.length |           a!!.length |
	+------------+--------------------+---------------------+----------------------+
	|      "cat" | Compile time error |                   3 |                    3 |
	|       null | Compile time error |                null | NullPointerException |
	+------------+--------------------+---------------------+----------------------+
   ```
   
   !! is an option for NPE-lovers. ```a!!.length``` will return a non-null value of a.length or throw a NullPointerException if a is null. And ```a?.length``` returns a.length if a is not null, and null otherwise:

   ```
   val a: String? = null
   print(a!!.length) // >>> NPE: trying to get length of null
   ```

   ```
   val a: String? = null
   print(a?.length) // >>> null is printed in the console
   ```
   
* Ternary Operator: **Unlike Java, there is no ternary operator in kotlin. Use if-else instead**

* Bitwise Operator:

   ```
   val andResult  = a and b
   val orResult   = a or b
   val xorResult  = a xor b
   val rightShift = a shr 2
   val leftShift  = a shl 2
   ```

* Elvis Operator: The Smarter Type-Safe If

   ```
   val list = mutableList ?: mutableListOf() 
   ```
	is a shorter form of
   ```
   val list = if (mutableList != null) mutableList else mutableListOf()
   ```
   
   The name,howver, comes from the famous American singer Elvis Presley. His hairstyle resembles a Question Mark [Ref](https://stackoverflow.com/questions/48253107/what-does-do-in-kotlin/48304523#48304523)
   
   ![alt text](https://i.stack.imgur.com/bVG64.png "Elvis Operator")

* when, if
   ```
	return if (x) foo() else bar()
	return when(x) {
	    0 -> "zero"
	    else -> "nonzero"
	}
    ```
    
     The above is preferable to:
     ```
	if (x)
	    return foo()
	else
	    return bar()

	when(x) {
	    0 -> return "zero"
	    else -> return "nonzero"
	}
     ```
     
* Functions

  ```
	fun double(x: Int): Int {
	    return 2 * x
	} 
	//SYNTAX: 
	fun funName( param : paramType ) : returnType
	{

	}
   ```

* Visibility Modifiers (public, protected, internal, private): public is used by default, means it will be visible everywhere.	If a declaration's private, it will only be visible inside the file containing the declaration.	If it's internal, it is visible everywhere in the same **module** (a module is a set of Kotlin files compiled together: IntelliJ IDEA, Gradle source set etc) and if protected, it's not available for top-level declarations.

 ```
 class EventViewModel internal constructor(
	)
	//internal makes class available to public, but constructor only to inside module
 ```

* Always declare local variables and properties as ```val``` rather than ```var``` if they are not modified (not variable) after initialization
* Prefer using immutable (whose state cannot be modified after it is created) data to mutable.
* Out Initialization code can be placed in initializer blocks, which are prefixed with the ```init``` keyword:

  ```
  class InitOrderDemo(name: String) {
	    val firstProperty = "First property: $name".also(::println)  //inits a val & also, prints the name
	    
	    init {
	        println("First initializer block that prints ${name}")
	        println("Second initializer block that prints ${name.length}")
	    }
	}
  ```
  

## Android + Kotlin:

* [Swipe Left/Right](https://stackoverflow.com/questions/49754979/capture-events-by-sliding-left-or-right-using-kotlin)
* [Custom Stroke Border EditText/TextViews Like Gmail](https://stackoverflow.com/questions/50619360/custom-edit-text-with-borders)

* Activity
	```
	class SplashActivity : AppCompatActivity() {

		override fun onCreate(savedInstanceState: Bundle?) {
		super.onCreate(savedInstanceState)

	    }
	}
	```
* Intent

	```
	val intent = Intent(this, MainActivity::class.java)
	startActivity(intent)
	finish()
	```

* SharedPref

## Extras (Kotlin)

* @Volatile before a field means that writes to this field are immediately made visible to other threads.
* Suppress Warnings: In Kotlin, there's no way to check the generic parameters at runtime in general case (like just checking the items of a ```List<T>``` or here in this ViewModelFactory, ```modelClass: Class<T>``` which is only a special case), so casting a generic type to another with different generic parameters will raise a warning, which needs to be suppressed

 ```
	 @Suppress("UNCHECKED_CAST")
	 override fun <T : ViewModel?> create(modelClass: Class<T>) = EventViewModel(eventRepository, lifecycleOwner) as T
 ```
* Companion Objects: if you declare a companion object inside your class, you'll be able to call its members with the same syntax as calling static methods in Java/C#, using only the class name as a qualifier.

 ```
  companion object {
      @Volatile private var instance: EventRepository? = null

      fun getInstance(eventDao:EventDao) =
          instance ?: synchronized(this) {
              instance ?: EventRepository(eventDao).also { instance = it }
          }
  }
 ```
 
## Extras-Random (Java/OOP in General)

* How does Thread communicate? - Threads communicate in 3 ways: ```wait()```, ```notify()```, ```notifyAll()```
* What's the access modifier of a method that no child class can extend/access/override: final
* Interface VS Abstract: Interface can have only abstract methods. Abstract class can have both abstract and non-abstract methods.  Variables declared in a Java interface are by default final. Abstract class can have final, non-final, static and non-static variables. Interface has only static and final variables.

  
