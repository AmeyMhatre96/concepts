## Why client side rendering

4. **Offline Capabilities**: Client-side rendering, when combined with technologies like service workers, enables web applications to work offline or in low-network conditions. This is a crucial feature for progressive web apps (PWAs) and mobile apps developed using web technologies.

5. **Dynamic Content Updates**: Client-side rendering allows for real-time updates of content without refreshing the entire page. This is essential for applications that rely on live data, such as social media feeds, chat applications, or collaborative tools, as it provides a more seamless and responsive user experience.

6. **Reduced Server Load**: By offloading rendering to the client side, the server can focus on serving data and APIs, reducing the computational load on the server. This can lead to cost savings and improved server scalability.

7. **Rich User Interfaces**: Client-side rendering empowers developers to create rich and interactive user interfaces with modern JavaScript frameworks and libraries. This flexibility enables the development of sophisticated, feature-rich web applications with complex UI components and animations.

8. **Single Page Applications (SPAs)**: Client-side rendering is a core concept in SPAs, which provide a fluid and app-like experience by loading content dynamically as the user navigates. This approach can simplify navigation, reduce page flicker, and maintain a consistent layout.

9. **API Integration**: Client-side rendering allows applications to integrate with third-party APIs easily. Developers can make asynchronous requests to APIs and render the data on the client side, creating a more seamless user experience and enabling integration with various data sources.

10. **Cross-Platform Compatibility**: Web applications using client-side rendering are accessible from a wide range of devices and platforms, including desktops, smartphones, and tablets. This broad accessibility is crucial for reaching a diverse user base.

11. **Improved User Retention**: The smooth and responsive user experience provided by client-side rendering can lead to higher user retention rates and increased user satisfaction, as users are more likely to engage with and return to a well-designed, interactive application.

It's essential to strike a balance between the benefits and potential drawbacks of client-side rendering, such as search engine optimization (SEO) challenges, initial load times, and browser compatibility. Careful planning and optimization are necessary to harness the advantages while mitigating the disadvantages.


## ES6?
ES6 comes with significant changes to the JavaScript language. It brought several new features like, let and const keyword, rest and spread operators, template literals, classes, modules and many other enhancements to make JavaScript programming easier and more fun. 

**1. let and const keywords :**
The keyword "let" enables the users to define variables and on the other hand, "const" enables the users to define constants. Variables were previously declared using "var" which had function scope and were hoisted to the top. It means that a variable can be used before declaration. But, the "let" variables and constants have block scope which is surrounded by curly-braces "{}" and cannot be used before declaration.
```javascript
let i = 10;
console.log(i);   //Output 10

const PI = 3.14;
console.log(PI);  //Output 3.14
```
**2. Arrow Functions**
ES6 provides a feature known as Arrow Functions. It provides a more concise syntax for writing function expressions by removing the "function" and "return" keywords.

Arrow functions are defined using the fat arrow (=>) notation.
```javascript
// Arrow function
let sumOfTwoNumbers = (a, b) => a + b;
console.log(sum(10, 20)); // Output 30
```
It is evident that there is no "return" or "function" keyword in the arrow function declaration.

We can also skip the parenthesis in the case when there is exactly one parameter, but will always need to use it when you have zero or more than one parameter.

But, if there are multiple expressions in the function body, then we need to wrap it with curly braces ("{}"). We also need to use the "return" statement to return the required value.

**3. Multi-line Strings**
ES6 also provides Multi-line Strings. Users can create multi-line strings by using back-ticks(`).

It can be done as shown below :
```javascript
let greeting = `Hello World,     
                Greetings to all,
                Keep Learning and Practicing!`
```
                
**4. Default Parameters**
In ES6, users can provide the default values right in the signature of the functions. But, in ES5, OR operator had to be used.
```javascript
//ES6
let calculateArea = function(height = 100, width = 50) {  
    // logic
}

//ES5
var calculateArea = function(height, width) {  
   height =  height || 50;
   width = width || 80;
   // logic
}
```
**5. Template Literals**
ES6 introduces very simple string templates along with placeholders for the variables. The syntax for using the string template is ${PARAMETER} and is used inside of the back-ticked string.
```javascript
let name = `My name is ${firstName} ${lastName}`
```
**6. Destructuring Assignment**
Destructuring is one of the most popular features of ES6. The destructuring assignment is an expression that makes it easy to extract values from arrays, or properties from objects, into distinct variables.

There are two types of destructuring assignment expressions, namely, Array Destructuring and Object Destructuring. It can be used in the following manner :
```javascript
//Array Destructuring
let fruits = ["Apple", "Banana"];
let [a, b] = fruits; // Array destructuring assignment
console.log(a, b);

//Object Destructuring
let person = {name: "Peter", age: 28};
let {name, age} = person; // Object destructuring assignment
console.log(name, age);
```
**7. Enhanced Object Literals**
ES6 provides enhanced object literals which make it easy to quickly create objects with properties inside the curly braces.
```javascript
function getMobile(manufacturer, model, year) {
   return {
      manufacturer,
      model,
      year
   }
}
getMobile("Samsung", "Galaxy", "2020");
```
**8. Promises**
In ES6, Promises are used for asynchronous execution. We can use promise with the arrow function as demonstrated below.
```javascript
var asyncCall =  new Promise((resolve, reject) => {
   // do something
   resolve();
}).then(()=> {   
   console.log('DON!');
})
```

**9. Classes**
Previously, classes never existed in JavaScript. Classes are introduced in ES6 which looks similar to classes in other object-oriented languages, such as C++, Java, PHP, etc. But, they do not work exactly the same way. ES6 classes make it simpler to create objects, implement inheritance by using the "extends" keyword and also reuse the code efficiently.

In ES6, we can declare a class using the new "class" keyword followed by the name of the class.
```javascript
class UserProfile {   
   constructor(firstName, lastName) { 
      this.firstName = firstName;
      this.lastName = lastName;     
   }  
    
   getName() {       
     console.log(`The Full-Name is ${this.firstName} ${this.lastName}`);    
   } 
}
let obj = new UserProfile('John', 'Smith');
obj.getName(); // output: The Full-Name is John Smith
```
**10. Modules**
Previously, there was no native support for modules in JavaScript. ES6 introduced a new feature called modules, in which each module is represented by a separate ".js" file. We can use the "import" or "export" statement in a module to import or export variables, functions, classes or any other component from/to different files and modules.
```javascript
export var num = 50; 
export function getName(fullName) {   
   //data
};
import {num, getName} from 'module';
console.log(num); // 50
```

## What is a transpiler?

A transpiler is a tool that converts code from one programming language to another. For example, Babel is a transpiler that converts ES6 code to ES5 code. This allows developers to use the latest JavaScript features while still supporting older browsers.

## What is a polyfill?

A polyfill is a piece of code that provides the functionality of a newer API in an older browser. For example, the fetch polyfill provides the fetch API in browsers that don't support it natively.

## What is a shim?

A shim is a piece of code that provides the functionality of a newer API in an older browser. For example, the fetch polyfill provides the fetch API in browsers that don't support it natively.

## What is a bundler?

A bundler is a tool that combines multiple JavaScript files into a single file. This allows developers to use the latest JavaScript features while still supporting older browsers.

## What is a module loader?

A module loader is a tool that loads JavaScript modules. For example, Webpack is a module loader that loads JavaScript modules.

## What is a module bundler?

A module bundler is a tool that combines multiple JavaScript files into a single file. This allows developers to use the latest JavaScript features while still supporting older browsers.
