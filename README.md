# luckcalc
Feeling unlucky? Want to find out if you're having good or bad luck today? For the low price of free ~~and a potential segfault~~ `luckcalc` can provide!

# Usage
Simple and easy:  
```
git clone https://github.com/TorchedSammy/luckcalc
cd luckcalc
make
```  
And run with `luckcalc.exe` (Or `./luckcalc` on \*nix)

# But..
> undefined behaviour

What??  

This program defines 2 uninitialized variables (`bad_luck` and `good_luck`) and reads them to figure out your luck.  
Uninitialized variables may not always be what you expect in a local scope. They can be (say for us with an `int` type) 69, 6467 or whatever.

As [this stackoverflow](https://stackoverflow.com/a/1597426/13641384) answer says (edited for C++):  
> Static variables (file scope and function static) are initialized to zero:

```cpp
int x; // zero
int y = 0; // also zero

void main() {
    static int x; // also zero
    std::cout << x;
}
```  
> Non-static variables (local variables) are indeterminate. Reading them prior to assigning a value results in undefined behavior.

```cpp
void main() {
    int x;
    std::cout << x; // the compiler is free to crash here
}
```