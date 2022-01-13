# Object-Oriented Programming in JavaScript

You are not the only one to feel that JavaScript is weird. This is very common for people coming from other backgrounds. That's because JavaScript is not like those traditional class based languages.

## 1 History

It is important to know the historical context around JavaScript's creation. In 1994 Netscape relased their web browser called Netscape navigator. The web browser was a major success. Brendan Eich convinced his boss at Netscape that the Navigator browser should have its own scripting language. At that time Java was very very popular. Netscape was negotiating with Sun to include it in Navigator. The big debate inside Netscape therefore became “why two languages? why not just Java?”.

They eventually decided to come up with a new language for their browser. But the diktat from upper engineering management was that the language must look like Java beceause they wanted to attract Java programmers. At the same time, they didn't want to compete with Java. So Brendan Eich did something different for JavaScript. He chose first-class functions from [Scheme](<https://en.wikipedia.org/wiki/Scheme_(programming_language)>) and prototypes from [Self](<https://en.wikipedia.org/wiki/Self_(programming_language)>) as the main ingredients.

## 2 What is an Object?

In order to understand OOP in JavaScript, it’s important to understand the concept of objects. They are a primary part of JavaScript. Almost everything in JavaScript is an object.

> An object in JavaScript is simply a key-value pair where key is a string and the value can be anything.

It's simillar to a data structure called hash table. However, the implementation can vary on different JavaScript engines.

### 2.1 Creating objects in JavaScript

#### 2.1.1 Object Literals

Just like we can create variables, we can create objects on the fly. An object literal can be created in serveral ways

- Using curley braces {}

  ```js
  const user = {
    firstName: "Naimul",
    lastName: "Haque",
    getFullName: function () {
      return `${this.firstName} ${this.lastName}`;
    },
  };
  console.log(user.firstName);
  console.log(user["lastName"]);
  console.log(user.getFullName());
  ```

- Using `new Object()`
  ```js
  const user = new Object(); /* creates an empty object */
  user.firstName = "Naimul";
  user["lastName"] = "Haque";
  user.getFullName = function () {
    return `${this.firstName} ${this.lastName}`;
  };
  ```

#### 2.1.2 Using `Object.create()`

It creates a new object, using an existing object as the prototype of the newly created object. It always returns an empty object.

```js
const user = Object.create(null);
user.firstName = "Naimul";
user.lastName = "Haque";
user.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};
```

Now the problem with the above 2 approach is that, if we want to define more users we have to repeat the same codes which is not a good practice. So we can define a function which will create an object for us.

```js
function createUser(firstName, lastName) => {
    const user = {}
    user.firstName = firstName
    user.lastName = lastName
    user.getFullName = function() {
        return `${this.firstName} ${this.lastName}`
    }
    return user
}
const user1 = createUser("Naimul", "Haque")
const user2 = createUser("John", "Doe")
```

We can create many users with this function. What if I told you, we can't use this in practice? The reason is simple, the `getFullName` method is created on the object everytime we create a new user. The `getFullName` is a common functionality and doesn't need to have its own copy it each object. So how do we share these common functionalities with the user objects we create?

### 2.2 Readings

[Performance of key lookup in JavaScript](https://stackoverflow.com/questions/7700987/performance-of-key-lookup-in-javascript-object)
