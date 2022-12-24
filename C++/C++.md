## Namespaces

Region which provides a scope to the identifiers. Mainly used to prevent name collisions. Define Methods, Variables, and Classes

```
namespace name{
	//Definitions
}
```
It is a declarative region
`using namespace name` will be used to include all the declarations of a namespace

*endl flushes out as well as prints a newline*

## Functions
### Overloading
Different types of args
Different number of args
Different order of args

Function overloading leads to Polymorphism
Static Polymorphism: Code binding happens at compile time

Default values are just like Python
Ellipsis operator(...): allows us to take variable number of argument

#### Inline Functions
Whenever the control comes to that function, it does not go out of the parent block, therefore saving some finite time. Instead it places the code there and flow of the program continues. **Making a function inline is just a request to the compiler not a gauranteed thing**

#### Lambda Functions
```
auto greet = [](){
	//statements
}
```
[] -> lamda
() -> Parameters 
To include explicit return types we use arrow ops, by default it returns int
```
auto greet = []() -> double{
	//statements
}
```


## Strings and Vectors

#### Strings
```
string s1 // init string, empty
string s2(s1) //copy s1
string s2 = s1 // copy s1
```

Range based for
```
for(auto c:str){
	//statements
}
```

`typeid(var).name()` gives the name for the variable

#### Vectors
Collection of objects of the same type. It is a template not a type. You have to include the type as well when defining Vectors. Inside std only
```
vector<int> a;
vector<int> a(n);
vector<int> a(n, val);
```

#### Arrays
Two extra function, begin and end. They give the pointers to beginning and 
one past the end of the arrays.

### Error Handling
Using Try and Catch statements
```
try{

}
catch(std::exception& e){
	std::cerr << e.what() << std::endl;
}
```

### Trippy Features
