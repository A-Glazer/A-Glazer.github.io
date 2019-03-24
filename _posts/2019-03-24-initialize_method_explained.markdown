---
layout: post
title:      "Initialize Method Explained"
date:       2019-03-24 18:40:36 +0000
permalink:  initialize_method_explained
---


## What is the initialize method and how is it defined?
The initialize method tells the program what to do when `.new` is called. For example, to create a new dog, one would call `brownie.new.` But what happens next? That’s where the initialize method comes in. The first thing the program will do when `.new` is called, is run the initialize method and do whatever is written there. If you want the puppy to have a name when it is initialized, the initialize method would instantiate with an argument of a name. So now if `brownie.new` was called, it would need to be written as `brownie.new(“Brownie”)`. 
Inside the initialize method each argument needs to be assigned to an instance variable. This step is important because it allows the program to access the information later on. To define an instance variable, put an @ sign before the word. For example: `def initialize(name), @name = name`.

## What is a reader and writer and how is it connected to initialize?
Any attribute brought into the initialize method needs to have a reader and writer, which tells the program how to find everything listed. This can be created via a method `name` and `name=`, but a much cleaner way is to use an `attr_accessor`. An attr_accessor is both the reader and writer method and is defined by putting a colon and then the attribute (:name). If you don’t want the property to be reassigned by a user, use an attr_reader instead. An attr_writer is what the user inputs, and a attr_reader is what the program outputs. 

## What is self and how can it be used to save an object?
Each of the attributes/arguments that are created upon initialization, are used to describe the object. Now that all the parts of the attributes of the object have been created, they need to be saved. The cleanest way to do this is by adding self to a class variable array. What is self? Self in this case is everything you have defined in your initialize method until now. So if you have `@name = name, @breed = breed, @color = color`, self would be @name, @breed, @color. (Note: if self is called in a method definition, it would refer to the class. If called inside a different method, it would be whatever is in that method). 

## How to create a default argument?
Sometimes you want to create a default for an argument. For example, if you want all new dogs to be alive when they are created, it should be defined in the initialize argument by putting an = sign after the argument. For example: `initialize(status = “alive”)`. The status can always be changed inside the initialize method, but if it is not, then it will remain alive.

To summarize, anything you always want to happen when a new object is created, should be defined in the initialize method. 

