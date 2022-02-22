## 1) How come you chose Rust for this game? It's not exactly the most mature language for game development.

> Rust may seem like an unusual choice for a project like this. It's a new language that has yet to properly prove itself in production environments, and is still undergoing relatively rapid changes. We chose Rust because it has several unique features that we believe will come to benefit the project in the long-term.
>
> **Rust is safe**
> Code written in vanilla Rust cannot trigger undefined behaviour. Rust's design helps us avoid a plethora of bugs common in other compiled languages such as dangling pointers, buffer overflow, invalid/null pointers, data races, array bound errors, and many more. This makes it particularly suitable for a large collaborative project such as this because it makes it difficult for new code to introduce difficult to fix bugs into the codebase.
>
> **Rust is fast**
> Rust is a compiled language that doesn't require a garbage collector, exceptions, or many of the other runtime systems that make other languages so slow. In most scenarios, well-written Rust is at least as fast (and often faster) than well-written C++.
>
> **Rust is modular**
> Rust comes with the Cargo build system and package manager. It allows Rust to be compiled in a modular manner, borrowing other libraries (known as crates) from the rest of the Rust ecosystem with ease.
>
> **Rust is portable**
> Rust's compiler uses LLVM to target most major hardware platforms. By using Cargo as its build system, it allows for consistent compilation across many platforms. No more searching for header files or fighting linker errors!
>
> **Rust is well-designed**
> Rust's syntax is designed to be user-friendly (wherever it can without compromising on features) and well-suited to system programming. Its unique combination of low-level control and safety makes it perfect for building both game engines and high-level game logic.

## 2) Why use gitlab over github?

> Gitlab has better integrated ci/cd and offers everything else that Github has. Both of them are only a service on top of git on the computer, so not too much different.

## 3) What noise function do we actually use?

> Perlin, worley, simplex, value, gradient, and a few Zesterer invented.

## 4) How can I help? Do I have to be part of a team? I don't have experience in Rust but really want to learn and help.

> Generally speaking, you can help in every area you want to. You don't have to become part of a team. But as soon as you helped a bit and showed that you are interested you can get in the respective "team".

## 5) How is the movement/physics/mechanics programming handled?

> That's implemented in [`common`](developers/codebase-structure.md#common), which is a crate for code that's common between both the server and the client.
> (because the server needs to be the ultimate authority on physics, but the client needs to do physics prediction so that lag/latency doesn't look bad)

### 6) Does it have all the OOP stuff you need for a project like this? Are there times when you are coding in Rust and there is something you feel could be expressed much better in C++? I originally dismissed Rust when I first encountered it since it looked like it was just C with different syntax and some functional programming stuff, but I heard recently it is supposedly much more than that.

> Although Rust has features that on the surface appear to make it an object-oriented language (it has objects, methods, interfaces, etc.) it's not actually an object-oriented language.
> One of the common trip-ups new developers make is to try to force Rust to behave like an OO language when a particular problem is better solved in a more Rust-y way.

## 7) What flexibility does Rust provide that Unreal Engine does not? Is it simply because Rust makes the project modular while Unreal Engine is not modular enough for open source development?

> A voxel game is a rather specific kind of game. It deals with a lot of data that most engines simply aren't really designed to deal with. Along with that, a lot of the game is procedural, something that existing asset-driven engines aren't too well equipped to deal with either.
> An existing engine, for us, would provide relatively few advantages despite providing several pretty significant disadvantages.

## 8) Do you guys ever want to take this project to a fundraising platform like Kickstarter so that someone can work on it full time? Is it possible that this could become a goal one day? Or will this never be a goal?

> We probably won't go that route, though I guess it's hard to say anything for sure. We see this as a volunteer project. It's more likely that any fundraising we do would go towards maintaining servers and such.

## 9) I got a question on how to compile the game?

> Everything should be described in the [Contributors](introduction.md) section.
