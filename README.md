# Welcome in the NEW CHAPTER Typescript!

### Table of contents

- [What is Typescript?](#what-is-typescript)
- [Why Typescript?](#why-typescript)
- [How to install Typescript?](https://github.com/LunashaGit/Javascript-TO-Typescript-skills-Power-Rangers-Group/tree/main/Installation)

## What is Typescript?

![Typescript](./Images/js-ts.jpg)

Typescript is a superset of Javascript. It is a language that compiles to complete Javascript. It adds optional static typing to the language.

## Why Typescript?

In your professional career, you will use Typescript generally, because in (Both) Frontend and Backend, you need to use some TYPES for data Generally, Functions, Classes, Variables, etc. For example, if you call an API, every data can be different & with JS, Generally, an API will give you an OBJECT, with Differents Arrays or String inside of it. But generally, in the back-end ( Each Framework ), you need to types each data, in your database, if an object is a string, it can explose your application. So, Typescript is a good way to avoid this problem.

It's for that, like PHP or Java, Typescript is a typed language.

36 -> Can Be a string, Number, Float and he can confuse the application. (36 -> Number, "36" -> String, 36.0 -> Float)

And you can do some conditions with Typescript, if a variable is a string do this else do that.

```js
// never -> It's a type, it's like void, but void can return something, never can't return something
// infer -> It's a keyword, it's like "as" in Typescript, but it's for generics
// ArrayValues -> Name of the function Type
// T & R -> It's a generic, it's like a variable, but it's a generic

type ArrayValues<T> = T extends Array<infer R> ? R : never;
```

But for the moment, it's not the most important thing, the most important thing is to understand the basics of Typescript. And how improve your code with Typescript!

## How to use Typescript?
