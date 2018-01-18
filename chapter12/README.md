# Chapter 10. Iterator and Generator  

> all scripts in this chapter needed running by node-v9.3.0 with `--harmony_array_prototype_values` flag   
## Iterator  
+ iterable objects can produce iterators by its `value()` method  
+ `next()` advance the iterator by one, and return (demo as `iterator/basics.js`)  
  - `done`: `true` or `false`
  - `value`
    * For `done` as `false`, underlying object anchored by this current iterator   
    * Otherwise, `undefined`  
+ the `for...of` loop will work with anything that provides an iterator  
+ iterators help to emulate a `for...of` loop with a while loop (demo as `iterator/for-of-sim.js`)   
+ iterators are distinct (demo as `iterator/distinctness.js`)   

## The Iteration Protocol  
> **Definition**: A class is iterable if it provides a symbol method `Symbol.iterator` that returns an object with iterator behavior (i.e., it has a `next()` method that returns an object with `value` and `done` properties) (demo as `iterator-proto/proto{1,2}.js`)   

+ Iterators can also be used to represent object that never run out of values (e.g. the generation of Fibonacci sequence)

## Generator  
> **Definition**: Generators are functions that use an iterator to control their execution  

(demo as `generator/basic.js`)  
+ two ability  
  - control the execution of a function, having it execute in discrete steps  
  - communicate with the function as it executes  
+ two exceptions to regular functions  
  - generator can *yield* control back to the caller at any point  
  - calling the generator returns an iterator, and the execution of the generator is triggered by invoking `next()` on the iterator  
+ signatures  
```javascript
function* generator-name() { ... }
```
+ use `yield` and `return` to switch control  

### yield Expressions and Two-Way Communication  
+ communication by `yield` expression  
+ value evaluated by `yield` is the argument passed into `next()` by the caller (demo as `generator/interrogate.js`)  
> Generators cannot be created with arrow notation

### Generators and return  
+ Calling `return` from anywhere in the generator will result in `done` being true, with the `value` property being user-defined  
+ `for...of` loop ignores the value paired with `done=true`  