### Misc
* `assert_eq!(x,y)` if x=y then move on, otw crash
* `assert!(x)` if x is true, move on, otw crash
* `{:?}` is used to format print in debug mode, `{1:?}` will map that braces to the 1st arguument.
* `std::any::type_name::<T>()`
* Functions such as `abs` and `pow` are avaliable to most numeric types, but the numeric type must not be left to be determined automatically. It should be explicitly typed.
* `1..100` iterates from 1 till 99, Range type object
* `1..=100` iterates from 1 to 100, RangeInclusive type object
* Rust uses Unicode Scalar, better than ASCII. 4 bit char
* Unit Type `()` has size 0, seeexxxxxyyyyyyy `let _v: () = ();`

### Variables
```
let x: i32;
assert_eq!(x, 3)
```
Uninitialized but used var will generate an error
```
let x: i32;
```
Uninitialized but unused var will generate a warning

* *Rust defaults to i32 initialization for an integer*
* *`x as u32` casts x to unsigned 32
* To cast constants to a particular type, use __ : `38u16`

*Sexy Example on typecasting*
```
// Remove something to make it work
fn print_type_of<T>(_: &T) {
    println!("{}", std::any::type_name::<T>())
}

fn main() {
    let x = 5;
    let mut y: u32 = 5;
    print_type_of(&x);

    //y = x;
    /*When the above line is commented, type of x is default i32, but if u uncomment the above line it becomes u32*/
    let z = 10; // Type of z ? 

    println!("Success!");
}

```

### Functions

```
fn another_function(x: i32){
	println!("Hello {}", x);	
}
```
