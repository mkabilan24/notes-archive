Typescript 

This is the session we will be taking a base idea about the typescript part for learning about the angular framwork.

#### What is TypeScript

> TypeScript is basically an extention of JavaScript. 

TypeScript can be called as a superset of JavaScript. It can be also called as developer dependancy for the application, cause your typescript application will be first converted in the javascript application and then will be executed.

Typescript do provide you with a lot of interesting feature for the application like static typing, classes, interface (which we dont have in javascript) and you can also get strong typing for the application, which can assist you with the developing with more deterministic application's i.e. you will be aware what is the input and what will be the output for the applciation.

Some of the key feature for the TypeScript:

1. Static typing
	- Typescript allows you to define type like string, number, and so on. For the variables, function parameter and return values
	- This helps catch the compile time error rather than catching them at run time.
2. Object oriented Programming:
	- TypeScript supports classes, inheritance, interfacem and access modifiers (public, private, protected) which are important while developing the complex application.
3. Imporvised Tooling and Autocomplete:
	-  Dure to its type system typescript provides better tooling support such as autocompletion, error detection and navigation in code editor like Visual Studio code.
4. Enhanced Readability:
	-  The use of types and interfaces makes the code easier to read and maintain which is especially helpful in larger projects or teams.

### Setting up a basic program for the typescript practice.

You can use some online editor for the practice of typescript, we will try to perform the same on the local enviornment so that we can get a better feels for how the progam is executed in the application.

You can try and execute the following steps to get yourself started with the typescript

```Bash

# installing the base package.json file to set the config for the project

npm init -y

```

```Bash

# install the developer dependency for the npm

npm install --save-dev typescript

```

```Bash

# generating the configuration

npx tsc --init

```

```JSON

{
  "compilerOptions": {
    "target": "es6",                      // Specify ECMAScript target version
    "module": "commonjs",                 // Module code generation
    "outDir": "./dist",                   // Output directory for compiled files
    "rootDir": "./src",                   // Root directory of source files
    "strict": true,                       // Enable strict type-checking options
    "esModuleInterop": true               // Enables compatibility with CommonJS modules
  },
  "include": ["src/**/*.ts"],             // Include all TypeScript files in src
  "exclude": ["node_modules"]             // Exclude node_modules
}
```

```Bash

# create the typescript file with the extention of .ts

touch 1_typescript.ts

```


```Bash
# to run the typescript

npm run build

```

Observe the state of the directory.

---

### Example 

1. String
```TypeScript

let name: stirng = "Sahil";
console.log(name);
name = "sahil upadhye"
// name = 26; // This will give the error

```

2. Number

```TypeScript

let age: number = 25;
let decimal: number = 10.1;
let hex: number = 0xf00d;

```

3. Boolean

```TypeScript

let isLoggedIn: boolean = true;
isLoggedIn = false;

```

4. Array

```TypeScript

// declaring the array can be done in 2 ways
let numbers: number[] = [1,2,3,4,5];
let strings: Array<string> = ["hello", "world"];

```

5. Tuple
	- Fixed-length array with specific type

```TypeScript

let user: [string, number];

user = ["sahil", 121];
// user = [23, "sahil"] // this will give error


```

6. Enum
	- Enum are named constant. It will start with 0 by default

```TypeScript

enum Color {
  Red,
  Green,
  Blue
}
let favoriteColor: Color = Color.Green;
console.log(favoriteColor);  // Output: 1

```

7. Any
	- Used for values with unknow types. Avoid using any if possible as it disables type-checking

```TypeScript

let data: any = "Hello";
data = 42;  // valid
data = true;  // valid

```

8. Null and Undefined
	- TypeScript has null and undefined types, which can be assigned only if strictNullChecks is off.

```TypeScript
let x: null = null;
let y: undefined = undefined;
```

9. Union Types
	- Allows a variable to hold more than one type.

```TypeScript
let value: string | number;
value = "hello";  // valid
value = 123;  // valid
```


#### Basic example for interface

#### Interface

> Interface defines the structure of an ojectm including properties and methods. They are ofter used to define the same of an object or function

```TypeScript

interface User {
	id: number;
	name: string;
	isAdmin: boolean;
}

```

-> You can also use inhertance for the application's interface.

--- 

Loops in Typescript part for the application:


There are three type of loop for the Typescript application. Some of the loop that make use of the TypeScript would be as follow

**Simple For loop and conditional statement**:

```TypeScript

let numbers: number[] = [1, 2, 3, 4, 5];

//simple for loop for the application
for (let i = 0; i < numbers.length; i++) {
  console.log(numbers[i]);
}

// enhanced for loop
for (const number of numbers) {
  console.log(number);
}

const data = { id: 1, name: "Sahil", email: "sahil@tcs.com" };
for (let key in data) {
  console.log(key, data[key as keyof typeof data]);
}

///while and do While
let counter = 0;
while (counter < 5) {
  console.log(counter);
  counter++;
}

counter = 0;
do {
  console.log(counter);
  counter++;
} while (counter < 5);

// simple example for the map loops in TypeScript
const mapexample = numbers.map((tempData) => tempData * 2);

console.log(mapexample);

// simple example for the filter loops in TypeScript
const filterexample = numbers.filter((tempData) => tempData !== 2);

console.log(filterexample);

```

---

### Function

Following are the some the example for the function in TypeScript

```TypeScript

// simple function in TypeScript

function add(let a: number, let b: number){
	return a + b;
}

const add = (let a: number, let b: number) => {
	return a + b;
}

```


----

#### oop concept for the application

Here are examples demonstrating how to create classes in TypeScript, including inheritance and access modifiers.

1. Basic Class

```TypeScript
class Animal {
  // Properties
  name: string;
  age: number;

  // Constructor
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  // Method
  makeSound(): void {
    console.log("Animal sound");
  }
}

const animal = new Animal("Lion", 3);
console.log(animal.name);  // Output: Lion
animal.makeSound();        // Output: Animal sound
```


2. Class with Access Modifiers

TypeScript has public, private, and protected access modifiers.

public - Accessible from anywhere (default).

private - Accessible only within the class.

protected - Accessible within the class and subclasses.


```TypeScript
class Person {
  public name: string;         // Can be accessed from outside
  protected age: number;       // Can be accessed by subclasses
  private ssn: string;         // Only accessible within this class

  constructor(name: string, age: number, ssn: string) {
    this.name = name;
    this.age = age;
    this.ssn = ssn;
  }

  public getDetails(): string {
    return `Name: ${this.name}, Age: ${this.age}`;
  }
}

const person = new Person("Alice", 30, "123-45-6789");
console.log(person.getDetails());   // Output: Name: Alice, Age: 30
// person.ssn;  // Error: Property 'ssn' is private and only accessible within class 'Person'
```

3. Inheritance

You can extend a class to create a subclass that inherits properties and methods from the parent class.

```TypeScript
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound(): void {
    console.log("Some generic animal sound");
  }
}

class Dog extends Animal {
  breed: string;

  constructor(name: string, breed: string) {
    super(name);  // Call the parent class constructor
    this.breed = breed;
  }

  // Method overriding
  makeSound(): void {
    console.log("Woof! Woof!");
  }

  showBreed(): void {
    console.log(`Breed: ${this.breed}`);
  }
}

const myDog = new Dog("Buddy", "Golden Retriever");
console.log(myDog.name);       // Output: Buddy
myDog.makeSound();             // Output: Woof! Woof!
myDog.showBreed();             // Output: Breed: Golden Retriever
```

4. Abstract Classes

Abstract classes cannot be instantiated directly and are meant to be extended by subclasses. They can define abstract methods that must be implemented by subclasses.

```TypeScript
abstract class Shape {
  abstract area(): number; // Abstract method (no implementation)

  printArea(): void {
    console.log(`Area: ${this.area()}`);
  }
}

class Circle extends Shape {
  radius: number;

  constructor(radius: number) {
    super();
    this.radius = radius;
  }

  area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

const circle = new Circle(5);
circle.printArea();  // Output: Area: 78.53981633974483
```

5. Interfaces with Classes

Classes can also implement interfaces to ensure they have specific properties or methods.

```TypeScript
interface Movable {
  move(): void;
}

class Car implements Movable {
  move(): void {
    console.log("Car is moving");
  }
}

const myCar = new Car();
myCar.move();  // Output: Car is moving
```


These examples cover basic class creation, inheritance, abstract classes, and implementing interfaces, which are essential for object-oriented programming in TypeScript.

----

#### Decorators:

> Decorators in the TypeScript are special function that can be attacjed to classes method and other places for the application. 

It basically suggest what kind of action needs to be performed in the applciation.
