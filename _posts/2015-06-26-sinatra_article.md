---
layout: post
title:  "Basic Definitions in Sinatra"
date:   2015-06-26 09:10:41
categories: ruby sinatra orm
---

#Assignment

Sumeet is having us answer the questions below.  I'm finding these short writing assignments help us learn technical terms now, but are also useful later.  We are learning so much that review is necessary.

#Article on Definitions for our ORM/Sinatra project

Answer these questions to the best of your ability in a Markdown document, which you add to your blog.

###What is a class?

A class is a blueprint for an object.  It is the building block of code in object-oriented programming.  The benefits of OOP are encapsulation, inheritance, and polymorphism.

  - encapsulation - data is protected within an object.  Black box design.  Input goes in, the object does something, and a message comes out.  Other objects do not have to understand how it works.  Private methods and variables are not even visible to outsiders.
  - inheritance - one class can inherit from another.  In Ruby, all classes inherit from the Object class.  Inheritance allows one class of objects to inherit all code form their parent class and still have their own specific child class methods/variables.
  - polymorphism - ability of an object to take on many forms - ie it can be operated on by child or parent methods, can be extended or included with modules or can be designed as a duck type with other objects.

###What is a model?

The model is a Ruby class that manages the data and business logic of a particular object type.  

The data should be persistent, so data is typically stored in a database, and the model is responsible for getting the data from the database, rendering it into an object, running business logic, and saving changes or new records back into the database.  

The model will typically have to convert ruby data types (objects, arrays, hashes) into the primitive data types that a database can store.  This is achieved using a relational database model.

###What is a method?

A method is a function that _does_ something and _returns_ something.  Instance methods should change or read an object's instance variables and return something as a result.  Class methods do and return something regarding a whole class, instead of an instance of it.  Sinatra's route methods are matched to the url request and return something that is rendered into html as a result.

The input a method might need to do its _something_ is called a parameter or argument.

###What is a variable?

A variable in programming is the same as a variable in mathematics.  It is a symbol used to stand in for something else.

An object's instance variable is defined by the class as an attribute of the object.

###What is a request?

A request in Sinatra refers to the url address that was sent from the browser to the server.  It's what the router receives and decides where to go.

###What is a route?

The route in Sinatra is a method that is matched to the request and returns something that can be rendered back to the client in their browser.  Routes, like switch statements, are evaluated in the order in which they are defined. The first matching url is the method that is invoked.

###In the context of a web application, what is a "response"?

A response is what the request returns.  Ideally, it should be returned in something that can be rendered by the browser - ie html.