# TypeScript up and running

![image](https://user-images.githubusercontent.com/25086862/229640282-ff11a7e0-8593-45ce-a505-f1fb4ab5ea83.png)

Woooooah look who decided to show up after so many time! Ok i know it's been a while since my last blogpost hehe 😬
but i promised you a part two for this topic so let's get to it 🤓

And yeah, if you haven't already go check out the first part of this blogpost here 👉🏼 https://medium.com/p/aa3e3d9de047

## Classes

Typescript does not have a preference when it comes to JavaScript patterns, so it's important to know how it behaves with classes; If im beign honest, i don't use that much POO in my day to day in JavaScript, but it's always good to know how Typescript behaves with it, and if you do use classes in your day to day, this chapter is a no brainer.

### Class Methods

When we talk about class methods, TS pretty much does the same type cheking that it does with traditional functions. it checks their params types and their return type, if any of it are incorrect, you will get an error:

```javascript
class Alexa {
  sayTime(time: string) {
    console.log("The current time is", time);
  }
}

new Alexa().sayTime("10:15"); // Cool
new Alexa().sayTIme(); // Error, Expected 1 arguments, but got 0
```

### Class Properties

Properties are checked the same way as interfaces, for example:

```javascript
class Dog {
  name: string;

  constructor(name: string) {
    this.name = name;

    this.bankAccount = name; // Error: Property
    // 'bankAccount' does not exist on type Dog
  }
}
```

And, when it comes to Function properties, Typescript checks for both kinds of declaring a member on a class :

- Method (Using the same function per Class)
- Property (Re-creating the same function per instance)

And threats them as a regular Javascript function, checking his params and return types:

```javascript
class Netflix {
  // Method
  playVideo(title: string) {}

  // Property
  closeVideo: (title: string) => {};
}

new Netflix().playVideo === new Netflix().playVideo; // true
new Netflix().closeVideo === new Netflix().closeVideo; // false
```

Two more important notes about properties: we can have optional properties (similar to interfaces) and read-only properties:

```javascript
class Cat {
  name?: string; // Optional property
  readonly birthDate: Date; // Read-only property
}

```

### Classes as Types

One interesting feature is that we can use our classes as types, similar to when we have an Object and an Interface:

```javascript
class Artist {
  sing() {
    console.log("I'm Singing!!");
  }
}

let alejandroFernandez: Artist;

alejandroFernandez = new Artist(); // Ok
alejandroFernandez = "some text..."; // Error: Type 'string' is not assignable
// to type 'Artist'
```

### Classes and Interfaces

We can extend our classes using one or many interfaces using the _implements_ keyword:

```javascript
interface Game {
  type: string;
}

class BoardGame implements Game {
  type: string;

  constructor(type: string) {
    this.type = type;
  }
}
```

When we extend our classes, TS will check that our subclass properties or methods matches his base class types, for example:

```javascript
interface Game {
  type: string;
}

class BoardGame implements Game {
  type: number;
  // Type 'number' is not assignable to type 'string'

  constructor(type: number) {
    this.type = type;
  }
}
```

### Abstract classes

In certain situations, we may want to enforce that our classes have certain properties, but let the subclasses to implement their own signatures.
We can do this with the keyword _abstract_ :

```javascript
abstract class Programmer {
  abstract drinkFavoriteDrink();

}

class JavascriptProgrammer extends Programmer {
  drinkFavoriteDrink() {
    console.log("I'm drinking Beer!")
  }
}

class RubyProgrammer extends Programmer {
  drinkFavoriteDrink() {
    console.log("I'm drinking Cherry soda!")
  }
}
```

## Member Visibility

We can have private class members that can only be accessed by instances of their class

- public (Accessible by everybody)
- protected (Accessible only by the class and subclasses)
- private (Accessible only by the class)
- '#' Before member name (This is built in Javascript, Accessible only by the class)

```javascript
class Human {
  eyeColor = 'Brown' // public
  protected dayOfBirth = new Date() // protected
  private numberOfSecrets = 29 // private
  #nickName = 'Alien' // also private
}


class Rodrigo extends Human {
  sayInformationAboutMe(){
    this.eyeColor // Ok
    this.dayOfBirth //Ok
    this.numberOfSecrets // Error: Property 'numberOfSecrets' is private
    // and only accessible within class 'Human'
    this.#nickName // Property '#nickName' is not accessible outside
    //class 'Human' because it has a private identifier
  }
}

new Rodrigo().eyeColor // Ok
new Rodrigo().dayOfBirth // Error: Property 'dayOfBirth' is protected
// and only accessible within class 'Human' and its subclasses
new Rodrigo().numberOfSecrets // Error: Property 'numberOfSecrets' is private
// and only accessible within class 'Human'

```

However it's important to remember that these annotations (All but Javascript's # annotation) only exist in the type system and they are removed when compiling to Javascript
