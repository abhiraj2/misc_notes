# Graphics

* Geometric Model: Refers to the model of an item that we may create in the future
* Mathematical Model: Refers to the model of computational process or a physical process.

When modelling a physical phenomenon, it is more important to understand the physical phenomenon first

### C++ (lol)
* `class` and `struct` act the same
* Constructors: ```class class_name(){public: class_name(){}};``` constructors have the same name as class
* `default` keyword is used to assign the same constructor
* Destructors: `~class_name(){}` the compiler calls the destructor automatically
* Virtual Functions are member functions which are defined in the base function and overridden in the child class, For a function to change its functionality, it must be virtual `virtual void print();`
* `vitual void print() const = 0` signifies that print is a pure vitual function which needs to overwritten
* Any inherited function must have the same signature, therefore override is used to keep track of this.
* Friend Functions, basically classes can have friend functions and classes that can access the private members of the og function `friend void print();`
* Ostream and Istream objects cannot be made copies of
* Difference between `Func1(int &a)` and `Func2(int &a)`:
*Except for pointers there is an additional datatype in C++ known as reference variables, variables of type int& are references whereas int<i>*</i> are pointers 
* References can be thought of as constant pointers where the compiler itself puts the dereference operators. Therefore you can just use reference variable as an alias for an already existing variables.
* References must be initialized while declaring. When declraring it must be initialized to the variable itself
* `this` is a pointer
* Ordinarily we use the same type of pointers to point to variables of same type, but Objects with inheritance are an exception. A pointer to a baseclass can point to an object of a child object
* protected properties are the ones that can be accessed by an inherited class unline private


##### Operator Overloading
* Basically functions with special names.
* When the operator function is a member function, implicitly the first parameter is this
* We can't overload `::` `.*` `.` `?:`
* Assignment operators, subscript, call, and arrow operators must be defined as members
* Compound Assignment operators don't need to be members
* IO operators must be non member
* Overloading `<<` and `>>` is also very possible, these just provide a way to manipulate the behaviour of the class when called with ostream or istream object, `cout << Object` and `cin >> Obj` are basic examples of this
```
ostream& operator<<(ostream &os, const Sales_data &item){
	os << item.isbn() << " " << " hiiii";
	return os;
}
```
* During operator overloading casting from var& to var or something like that is not allowed because references are constant af, therefore u need to use the const keyword in the parameters

## Unreal Engine 4
#### Parent Classes
* None: Default constructor and destructor
* Actor: Most basic type that can be placed/spawned in the world
* Pawn: Actor that can be possessed and controlled 
* Character: Pawn which can be moved around

#### Functions
* `AFloatingActor::Tick(float DeltaTime)` Tick is the function that is called when there is a need to execute something in real time.
* `T varName* = CreateDefaultSubobject<T>(TEXT("objectName"))` is used to create a new object of type T
* `GetRootComponent()` is the function that returns an actors Root Comonent. Return value is USceneComponent*
* `SetActorLocationAndRotation(Vector, Rotator)`

#### Objects
* StaticMeshComponent: Handles the visual data of an object
* FVector: Holds Vectors
* FRotator: Holds Rotation Values in degrees


## Godot
In godot a game is a tree of nodes, that are grouped together into scenes.

#### Scenes
Godot Scenes are flexible, they can be anything, entire level, menu, character, etc... Can be used as prefabs or as scenes lol. They can be nested as well

#### Nodes
The smallest building blocks of a scene. Examples are KinematicBody2D, Camera2D, Sprite, CollisionShape2D