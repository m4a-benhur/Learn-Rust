# Introduction to Rust

### What is Programming?
Programming is like writing a recipe that a computer can follow exactly. Just like a cake recipe tells someone step-by-step how to bake, we write instructions that tell the computer what to do.

### What is Rust?
**Definition:** A language empowering everyone to build reliable and efficient software" - especially perfect for handling money and financial applications safely.

### Installation Instructions
**Using Rustup (the official installer):**

1. **Install Rust:**
   - **Mac/Linux:** Open terminal and run:
     ```bash
     curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
     ```
   - **Windows:** Go to https://www.rust-lang.org/tools/install and download the installer
   - **Add to PATH:** Follow the prompts to add Rust to your system PATH
   - **Verify:** Type `rustc --version` to confirm installation

2. **Install VS Code:**
   - Download from https://code.visualstudio.com/
   - Install "rust-analyzer" extension
   - This gives us syntax highlighting and error checking

3. **Test Your Setup:**
   ```bash
   cargo new hello_stellar
   cd hello_stellar
   cargo run
   ```
   Should display: "Hello, world!"

**Tools You Now Have:**
- **Rustc:** The compiler (turns your code into programs)
- **Cargo:** Package manager and project organizer
- **Rustdoc:** Documentation generator

---

### Welcome & What We're Building
Welcome! Today we start learning Rust - a programming language specifically chosen by Stellar because it's incredibly safe for handling money. By the end of today, you'll write your first Rust program!

### Why Rust for Blockchain?
**The Big Problem:** "What happens if there's a bug in software that handles millions of dollars?"
- Traditional languages allow crashes that lose money
- Memory errors can be exploited by hackers
- Race conditions can duplicate transactions

**How Rust Solves This:**

- **Memory Safety:** Rust’s ownership system ensures programs use memory correctly, preventing crashes from errors like accessing invalid data. It’s like a librarian ensuring you only touch the right files.
- **No Null Pointer Dereferencing:** A null pointer happens when a variable points to no data, and trying to use it can crash a program. Rust avoids this entirely by using the Option type, which forces you to handle missing data explicitly. This ensures the compiler catches potential issues before the program runs, reducing unexpected crashes from missing values.
- **Concurrency Safety:** Rust prevents race conditions (errors when multiple tasks access data simultaneously) by enforcing strict rules on data sharing, ensuring tasks like web requests don’t clash.
- **Performance:** Rust runs as fast as C/C++ because it compiles to efficient code without a garbage collector, but it’s safer due to its memory and concurrency rules. Ideal for games or servers.
- **Modern Syntax:** Rust’s clear, concise syntax (e.g., println!("Hello, world!");) is easy to read and write, making coding less daunting for beginners.



---

## Part 1: Your First Rust Program

### Hello, World! - The Traditional First Program

**Let's create our first program together:**
```bash
cargo new hello_world
cd hello_world
```

**Open `src/main.rs` and you'll see:**
```rust
fn main() {
    println!("Hello, world!");
}
```

**Let's understand each part:**
- `fn main()` - "This is the main function - where our program starts"
- `println!` - "Print this text to the screen"
- `"Hello, world!"` - "The text we want to show"

**Run it:**
```bash
cargo run
```

### Make It Personal
**Let's change it to something fun:**
```rust
fn main() {
    println!("Hello, Stellar!");
}
```

**Key Points:**
- Every Rust program starts with `fn main()`
- `println!` shows text on screen
- Don't forget the `!` after println

---

## Part 2: Variables - Storing Information

### What is a Variable?
A variable is like a labeled box where we store information. In blockchain, we store things like account balances, addresses, and transaction amounts.

In Rust, variables have *types* that describe the kind of data they store. Rust is statically typed, meaning the compiler must know the type of every variable at compile time.

Types in Rust can be divided into scalar types (single values) and compound types (multiple values grouped together).



### Variables in Rust Are Immutable by Default

**Basic variable creation:**
```rust
fn main() {
    let x = 5;
    println!("The value of x is: {}", x);
}
```

**Why can't we change it?**
```rust
fn main() {
    let x = 5;
    println!("The value of x is: {}", x);
    
    // This won't work:
    // x = 6;  // Error! Cannot change immutable variable
}
```

**This is good for blockchain - prevents accidental changes!**

### When We Need to Change Variables

**Use `mut` to make variables changeable:**
```rust
fn main() {
    let mut y = 10;
    println!("The value of y is: {}", y);
    
    y = 15;  // Now this works!
    println!("The value of y is now: {}", y);
}
```

### Variable Naming Rules
**Simple, clear names:**
```rust
fn main() {
    let balance = 500;
    let name = "Alice";
    let age = 25;
    let is_active = true;
}
```

**Rules:**
- Use letters and numbers
- Use underscores to separate words: `user_name`
- Start with a letter
- Make names clear and simple!

### Shadowing - A Special Rust Feature
**You can reuse variable names:**
```rust
fn main() {
    let x = 5;
    let x = x + 1;
    let x = x * 2;
    
    println!("The value of x is: {}", x); // Prints 12
}
```

**This is different from `mut` - we're creating new variables with the same name.**

---

## Part 3: Data Types - Teaching the Computer What Things Are

### Why Data Types Matter
If I say 'add 25 and 30', you know I mean 55. But if I say 'add twenty-five and thirty', the computer needs to know these are numbers, not text!

### Rust's Type System
- **Strongly typed:** Every value has a specific type
- **Type inference:** Rust can often guess the type
- **Explicit types:** We can specify types when needed

### Scalar Types (Single Values)

#### Integer Types - Whole Numbers
```rust
fn main() {
    let x: i32 = 10;
    let y: u8 = 255;
    
    println!("x is: {}", x);
    println!("y is: {}", y);
}
```

**Simple explanation:**
- `i32` - can be positive or negative (−2,147,483,648 to 2,147,483,647)
- `u8` - only positive numbers (0 to 255)
- Use `i32` for most whole numbers

#### Floating-Point Types - Decimal Numbers
```rust
fn main() {
    let x: f32 = 2.5;
    let y: f64 = 3.14;
    
    println!("x is: {}", x);
    println!("y is: {}", y);
}
```

**Simple rule:**
- `f64` is the default (more precise)
- Use for prices, percentages, anything with decimals

#### Boolean Type - True/False
```rust
fn main() {
    let t: bool = true;
    let f: bool = false;
    
    println!("t is: {}", t);
    println!("f is: {}", f);
}
```

**Simple:** Only two values - `true` or `false`

#### Character Type - Single Characters
```rust
fn main() {
    let c: char = 'Z';
    let heart: char = '♥';
    
    println!("Character: {}", c);
    println!("Heart: {}", heart);
}
```

**Remember:** Single quotes for characters, double quotes for text

### Compound Types (Multiple Values)

#### Tuples - Group Multiple Values
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
    let (x, y, z) = tup;  // Extract values
    
    println!("x: {}, y: {}, z: {}", x, y, z);
    
    // Or access by index
    let first = tup.0;
    println!("First value: {}", first);
}
```

**Think of it as:** A box with multiple labeled compartments

#### Arrays - Lists of Same Type
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
    let first = a[0];
    let second = a[1];
    
    println!("First element: {}", first);
    println!("Second element: {}", second);
}
```

**Simple rule:** All items must be the same type, size is fixed

### Working with Strings
```rust
fn main() {
    let s1 = String::from("hello");
    let s = "world";  // This is a &str
    
    println!("String: {}", s1);
    println!("&str: {}", s);
}
```

**Don't worry about the difference yet - we'll learn more later!**

### Simple Blockchain Example
```rust
fn main() {
    let balance = 100;
    let owner = "Alice";
    let is_active = true;
    
    println!("Owner: {}", owner);
    println!("Balance: {}", balance);
    println!("Active: {}", is_active);
}
```

---

## Part 4: Ownership & Borrowing Basics

### The Core Concept
"Ownership is Rust's superpower for preventing bugs in financial software."

### Basic Ownership Rules
1. Each value has exactly one owner
2. When the owner goes out of scope, the value is freed
3. You can transfer ownership or borrow temporarily

### Simple Example
```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;  // s1 is moved to s2
    
    // println!("{}", s1);  // This won't work!
    println!("{}", s2);     // This works
}
```

### References - Borrowing Data
```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = &s1;  // Borrow s1
    
    // Both work!
    println!("s1: {}", s1);
    println!("s2: {}", s2);
}
```

**Key Point:** Use `&` to borrow without taking ownership.

---

## Part 5: Hands-On Exercise

### Simple Wallet Exercise
"Let's put it all together:"

```rust
fn main() {
    println!("=== My Wallet ===");
    
    // Create these variables:
    let owner = "Alice";
    let mut balance = 100;
    let is_premium = true;
    
    // Show wallet info
    println!("Owner: {}", owner);
    println!("Balance: ${}", balance);
    println!("Premium: {}", is_premium);
    
    // Buy something
    let cost = 25;
    balance = balance - cost;
    
    println!("After spending ${}:", cost);
    println!("New balance: ${}", balance);
}
```

**Try it yourself! Change the values and run it.**

---

## Session Wrap-Up (5 minutes)

### What We Accomplished Today

**Core Programming Concepts:**
- ✅ **Variables** - Storage with labels (`let` keyword)
- ✅ **Immutability** - Safe by default (`mut` when needed)
- ✅ **Data Types** - Numbers, text, boolean, characters
- ✅ **Compound Types** - Tuples and arrays
- ✅ **Basic Ownership** - One owner rule and borrowing with `&`

**Rust-Specific Features:**
- ✅ **Memory Safety** - No crashes from memory errors
- ✅ **Strong Type System** - Prevents mixing up data types
- ✅ **Cargo** - Project management tool
- ✅ **Macros** - `println!` and the `!` syntax

### Why This Matters for Stellar Smart Contracts
- **Variables** store account balances and addresses
- **Immutability** prevents accidental balance changes
- **Type safety** prevents mixing tokens with addresses
- **Ownership** prevents data races in financial code
- **Performance** ensures fast transaction processing

### Preview of Next Session
- **Functions** - Reusable code blocks
- **Control Flow** - if/else decisions and loops  
- **Error Handling** - What happens when things go wrong
- **Pattern Matching** - Rust's powerful decision-making tool

These turn our static data into dynamic programs!

Remember: **Every expert was once a beginner.** You've just written your first Rust programs - that's a huge accomplishment! The concepts we learned today are the foundation of every Rust program, including Stellar smart contracts."

---




