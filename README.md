# TypeScript up and running
![image](https://user-images.githubusercontent.com/25086862/229640282-ff11a7e0-8593-45ce-a505-f1fb4ab5ea83.png)


Woooooah look who decided to show up after so many time! Ok i know it's been a while since my last blogpost hehe 😬
 but i promised you a part two for this topic so let's get to it 🤓


And yeah, if you haven't already go check out the first part of this blogpost here 👉🏼  https://medium.com/p/aa3e3d9de047 

## Classes 
Typescript does not have a preference when it comes to JavaScript patterns, so it's important to know how it behaves with classes; If im beign honest, i don't use that much POO in my day to day in JavaScript, but it's always good to know how Typescript behaves with it, and if you do use classes in your day to day, this chapter is a no brainer.

### Class Methods
When we talk about class methods, TS pretty much does the same type cheking that it does with traditional functions. it checks their params types and their return type, if any of it are incorrect, you will get an error:

```javascript
class Alexa {
  sayTime(time: string){
    console.log("The current time is", time)
   }
 }
 
 new Alexa().sayTime("10:15") // Cool
 new Alexa().sayTIme() // Error, Expected 1 arguments, but got 0
```
