Angular basics
# Some information for the angular application

---

Pre request: 

- [[JavaScript Basics]]
- [[JavaScript Advance]]
- [[TypeScript]]

---
# some information for the angular component

### Introduction to the angular component

---

-   what is a component?
-   component based architecture in Angular
-   Structure of a component:
    -   @Component decorator
    -   template
    -   styles
    -   logic
-   Component lifecycle overview

---

-   Angular is a client-side front end framework developed by team of developers at google based on the TypeScript. It is used for building dynamic and single-page web applications SPAs. Also, angular is a versatile framework for building web application allowing us to get a lot of features and tools.

-   Angular architecture Overview:

    -   To develop the angular application we will be required to make use of the MVC (MODEL, VIEW, CONTROLLER) or MVVM (Model, view and ViewModel).
    -   These type of design pattern is eaiser to manage code, improve maintainability and testable application.
    -   It also provide a reuseability of the code for the application.

-   Different modules for the application development in angular applications:

    1. Modules
    2. Components
    3. Templates
    4. Directive
    5. Service
    6. Router
    7. HTTP Client

Note:  
- We will try to create simple application to makes use of all different component to create application
- We will see how we can work with a sensible project Structure, data binding in forms dependancy injection and so on.

---

### Angular architecture

> Angular is a framework for building client application in HTML and either language like JavaScript or Typescript that com piles to Javascript.

The framework consist of various thing like libraries some of them include core, some of them include optional.

At a very high level if I had to break up the application
1. Compose **HTML Template** with Angularised Mark up ( { } )
2. writing the **component** to manage those HTML templates.
3. adding applications logic in the **service**, which can be called from **component**.
4. Boxing the **component** and **service** in **modules**
5. At last you bootstrap your angular application with the root module, which will be then presented by browser accor ding to the instruction created by you

![[Pasted image 20241021161844.png]]

- --

## Modules

> Angular applications are modular and has its own modularity systems called Angular modules or NgModules.

** Every angular applications has at least one Angular module class, root module conventionally named as App Module. **

While the root module in any angular application might be just 1, many apps have many more feature, each cohesive block of code dedicated on performing a specific functionality,  workflow, and close set of capabilities.

If you went to know if a module is a **root module**, you will see a class with **@NgModule** decorator

##### what is a decorator ?

> Decorators are the functions that modify Javascript classes. Angular has many different type of decorators that has attached Meta data for the application, so that it knows What is class about and what type of functionality are we trying to achive.  

@NgModule is a decorator that takes in 1 object as argument for defining metadata. some of the most important properties are
- declaration:
	- The view classes belong to this module. Angular has 3 kind of view classes Component directives and pipes.
- exports:
	- The subset of declarative that should be visible and useable in the component template of modules
- imports:
	- other modules whose exported classes are needed by component template declared in this modules.
- providers:
	- creators of service that this module contributes to the global collective of services.
- bootstrap:
	- Th e main application view, called the root component that hosts all other view. only the root modules should set this bootstrap properties

``` TypeScript

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule,AppRoutingModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

---
### Components 

Components are Fundamental building blocks of Angular application. Each angular application is made up of a hierarchy of Component, where each component represents a piece of user interface handles logic and portion of the code.

A component controls a patch of screen called a view. It consists of TypeScript Class an HTML template and a css Style sheet.

The typescript class defines, the interaction with the HTML template and the renderd DOM structure while styre sheet defines its appearance. 

An angular application uses the individual components to define and control different aspect of application for example
- A component with navigation links.
- list of customers
- list of banks

#### Basic Information of @Component

The component decorator identifies the class immediately below class as component and also specify its metadata . The metadata for a component tells the angular component where to get the building blocks for the application to be created and resent the component and its view. In particular its association with a template either directly inline code or by reference.

Example for a component

``` TypeScript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'sample-application';
}

```

You are see there are a couple of infomration for the components meta data for the application:

- selector: A CSS selector that tells angular to create and insert an instance of this component wherever it finds the corresponding tag in template HTML.
	- For example: if an application HTML content contains \<app-root\>\<\/app-root\> then angular inserts an instance of the AppCompoenntA 

#### Things we will be doing in the component and Template

-   Generating a component using angular CLI
-   Component folder Structure (.HTML, .CSS, .ts, .spec.ts)
-   using component in other component

```

npx @angular/cli@15.2.7 new sample-application

npx @angular/cli@15.2.7 generate component sample-component

```

### Component Templates

-   Inline templates vs Templates files 
-   Binding Data to templates
    -   interpolation ({{data}})
    -   Property Binding ([property])
    -   Attribute binding (attr.binding)
    -   class and style binding
-   Template Directive
    -   \*ngIf
    -   \*ngFor
    -   etc
-   Event binding : $event
-   two-way data binding ([ngModel])

#### Examples for the above mentioned component's component

--- 

**Inline template vs Template files**:

In AngularJS, templates are used to define the structure of what users see on the screen.

1. Inline Template:
	- The HTML is written directly inside the component's code.
	- It’s like putting a mini-HTML page directly into your code.

Example:
```TypeScript
template: '<h1>Hello, User!</h1>'
```

> **When to use**: For very small or simple components where just a few lines of HTML are needed.

2. Template File:
	- The HTML is stored in a separate file, not directly in the component's code.
	- Instead of writing the HTML in the code, you link to the file with templateUrl.

Example:
```TypeScript
templateUrl: 'path/to/template.html'
```


> **When to use**: For more complex components where the HTML is long or has many elements. This helps keep the code organized and clean.


> Simple Summary: Think of inline templates as writing a quick note directly in a message, while template files are like writing a full document and attaching it for better readability.

--- 

**Binding Data to templates**

> In Angular, **data binding** is a way to connect the data in  your code to what the user sees on the screen (using the HTML template). 

There are different type of data binding 

1. Interpolation ({{data}})
	- **what does it do?** It displays data inside the HTML 
	- **How it works?** You wrap the data in {{}} and Angular replaced it with the actual value

Example for interpolation
```HTML
<h1>Hello, {{name}}</h1>
```

> **Think of it as:** Filling in a blank with data, like a form letter with a blank space that you fill in.

2. Property binding ([property]):
	- **What it does?** It binds a property like src of an image in the HTML to variable code from the typescript.
	- **How it works?** You use square brackets around the property to like it to the code.
Example

```HTML 
<!-- HTML file for the application -->

<img [src]="imageSrc">

```

```TypeScript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  imageSrc = 'https://dummyimage.com/600x400/000/fff';
}

```

> **Think of it as** : Setting a property in HTML using the values from your code.

3. **Attribute Binding:**

	- **What it does?** Binds an HTML attribute (like aria-lavel for accessibilty) to data in your code.
	- **How it works?:** you use attr. before the attribute name to bind it to the data.
```HTML
<div>
    <!-- Interpolation -->
    <h1>{{ title }}</h1>

    <!-- Attribute Binding -->
    <button [attr.title]="tooltipText" (click)="changeTooltip()">
        Hover over me!
    </button>

    <!-- Class Binding -->
    <div [class.active]="isActive">
        This div is active: {{ isActive }}
    </div>

    <!-- Style Binding -->
    <button [style.background-color]="buttonColor">Styled Button</button>
</div>
```

```TypeScript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  // Define properties for data binding
  title = 'Welcome to My Angular App!';
  tooltipText = 'Click here to submit the form';
  isActive = false;
  buttonColor = 'red';

  // Method to change tooltip text
  changeTooltip() {
    this.tooltipText = 'You clicked the button!';
  }
}
```

> **Think if it as**: Setting specific HTML attributes based on data in your code.

4. **Class and Style Binding**
	- **What it does?:** Binds CSS classes or style to your HTML based on the values in your code.
		- Class Binding: You can dynamically add or remove CSS classes.
		- Style Binding: You can set styles like color, background.
	- **How it works?** You bind a class or style directly to data in your code.

Example: 
```HTML

<div [ng-class]="{'highlight': isActive}">Content here</div>
<div [ng-style]="{'color': textColor}">Text here</div>

```

> **Think of it as**: Dynamically changing how something looks based on conditions in your code.

---

#### Template Directive:

> In Angular, template directives like \*ngIf and \*ngFor are powerful tools that control the display and creation of elements based on certain conditions or data structures.

1. \*ngIf
	- What it does: \*ngIf conditionally includes or excludes elements from the DOM (HTML stucture) based on whether a given expression is true or false.
	- Use Case: Show or Hide an element based on a condition.

Example:
```TypeScript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  isActive:boolean = true;
}

```

```HTML

<div>
    <div *ngIf="isActive">
        <p>You have Active</p>
    </div>
    <div *ngIf="!isActive">
        <p>You are not Active</p>
    </div>
</div>

```

2. \*ngFor
	- What it does? : \*ngFor is used to loop over an array and create an element for each item in the array.
	- Use case: Display a list of items dynamically.

Example

```TypeScript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  isActive:boolean = true;
  todos: Todo[] = [
    {id: 1, desc: "Todo1"},
    {id: 2, desc: "Todo2"},
    {id: 3, desc: "Todo3"},
    {id: 4, desc: "Todo4"},
  ];
}

interface Todo {
  id: number,
  desc: String
}

```

```HTML

<div>
    <div *ngIf="isActive">
        <p>You have Active</p>
    </div>
    <div *ngIf="!isActive">
        <p>You are not Active</p>
    </div>
    <div>
        <ul *ngFor="let todo of todos">
            <li>{{todo.id}} : {{todo.desc}}</li>
        </ul>
    </div>
	<div>
		<p *ngIf="todos.length === 0">No Todos Found</p>
	</div>
</div>

```


---

#### Sending the data from parent to child 

> To send data from a parent component to a child component, you can use @Input property in the child component. This allows the parent component to bind data directly to a property of the child component.

Following are the steps we will be taking to communicate with the parent and child:

1. First we will start with the Parent component where we will write the message variable which we will pass to the child.
2. In the second step we will use **@Input** which will help us catch the input which is passed down from the parent component.

![[Pasted image 20241027171429.jpg]]

**PARENT COMPONENT**

```TypeScript

//parent component

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  message: String = "Hello from the parent class"  
}

```

```HTML

<!-- Parent Component --> 

<div>
    <h1>Parent component</h1>
    <hr />
    <app-child-component [message]="message"></app-child-component>
</div>

```

**CHILD COMPONENT**

```TypeScript

// child component

import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child-component',
  templateUrl: './child-component.component.html',
  styleUrls: ['./child-component.component.css']
})
export class ChildComponentComponent {
  @Input() message!: String; // !: will be used to tell typescript that this variable will be initialized later.
}

```

```HTML
<p>This is child component: {{message}}</p>
```

#### Sending the data from the child to parent

> To send infomration from a child component to a parent component you can use @Output with **EventEmitter**. This allows the child component to emit an event with data, and the parent component can listen for this event and receive the data.

1. Set up the child component with @Output
	- Import EventEmitter and output from @angular/core
	- Create a new property with the @Output() decorator and assign it an instance of EventEmitter
	- Use emit() on the EventEmitter to send data to the parent.
2. Set up the parent component to receive the event:
	- Om the parent component's template, use the child component's selector and bind to the @Output event with () syntax
	- Define a method in the parent component to handle the data emitted from the child.

**CHILD COMPONENT:**

```HTML

<div>
    <p>This is child component: {{message}}</p>
    <input type="text" name="output" id="output" [(ngModel)]="output" />
    <button (click)="sendMessage()">Send message from child to parent</button>
</div>

```

```TypeScript

import { Component, EventEmitter, Input, Output } from '@angular/core';

@Component({
  selector: 'app-child-component',
  templateUrl: './child-component.component.html',
  styleUrls: ['./child-component.component.css']
})
export class ChildComponentComponent {
  @Input() message!: String;
  @Output() messageOutput = new EventEmitter<String>();

  output!: String;

  constructor(){
    this.output = "";
  }

  sendMessage() {
    this.messageOutput.emit(this.output)
  }
}

```

**PARENT COMPONENT**

```HTML

<div>
    <h1>Parent component</h1>
    <hr />
    <app-child-component [message]="message" (messageOutput)="receiveMessage($event)"></app-child-component>
    <p>Message from the child: {{messageFromChild}}</p>
</div>

```

```TypeScript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  message: String = "Hello from the parent class";
  messageFromChild: String = "";

  receiveMessage(message: String){
    this.messageFromChild = message;
  }

}

```

---

#### Component Liftcycle

Here's an Angular component that logs each lifecycle hook to the console. This will help you see the order in which the hooks are called and understand how Angular manages component lifecycles.

Full Example Component with Lifecycle Hooks

In this example, each lifecycle hook will log a message to the console when it’s triggered.

lifecycle-demo.component.ts:

``` TypeScript

import { Component, OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy, Input, SimpleChanges } from '@angular/core';

@Component({
  selector: 'app-lifecycle-demo',
  templateUrl: './lifecycle-demo.component.html',
  styleUrls: ['./lifecycle-demo.component.css']
})
export class LifecycleDemoComponent implements OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {

  @Input() someInput!: string;

  constructor() {
    console.log('Constructor called');
  }

  ngOnChanges(changes: SimpleChanges): void {
    console.log('ngOnChanges called', changes);
  }

  ngOnInit(): void {
    console.log('ngOnInit called');
  }

  ngDoCheck(): void {
    console.log('ngDoCheck called');
  }

  ngAfterContentInit(): void {
    console.log('ngAfterContentInit called');
  }

  ngAfterContentChecked(): void {
    console.log('ngAfterContentChecked called');
  }

  ngAfterViewInit(): void {
    console.log('ngAfterViewInit called');
  }

  ngAfterViewChecked(): void {
    console.log('ngAfterViewChecked called');
  }

  ngOnDestroy(): void {
    console.log('ngOnDestroy called');
  }
}

```

Explanation of Lifecycle Hooks

**ngOnChanges**: Called before ngOnInit and whenever an @Input property changes. It receives a SimpleChanges object containing previous and current values of the changed properties.

**ngOnInit**: Called once after the component’s first ngOnChanges. Ideal for initialization logic.

**ngDoCheck**: Called during every change detection cycle, allowing custom change detection logic.

**ngAfterContentInit**: Called once after content (like \<ng-content\> projected into the component) is initialized.

**ngAfterContentChecked**: Called after every content check. Runs after ngAfterContentInit and ngDoCheck.

**ngAfterViewInit**: Called once after the component's view and child views are initialized.

**ngAfterViewChecked**: Called after every check of the component’s view and child views.

**ngOnDestroy**: Called right before Angular destroys the component. Useful for cleanup logic like unsubscribing from Observables.

Template for the Component:

lifecycle-demo.component.html:

```html
<p>Lifecycle demo component loaded</p>
<p>Input property: {{ someInput }}</p>
```

Using the Component

To see all the lifecycle hooks in action, you can add this component to a parent component and change the someInput value.

parent.component.html:

```HTML
<h2>Parent Component</h2>
<app-lifecycle-demo [someInput]="parentInput"></app-lifecycle-demo>
<button (click)="changeInput()">Change Input</button>
```

parent.component.ts:
```TypeScript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './parent.component.html',
  styleUrls: ['./parent.component.css']
})
export class ParentComponent {
  parentInput = 'Initial value';

  changeInput() {
    this.parentInput = 'Changed value';
  }
}
```

Running the Example

When you load the component, you’ll see logs from Constructor, ngOnChanges, ngOnInit, ngDoCheck, ngAfterContentInit, ngAfterContentChecked, ngAfterViewInit, and ngAfterViewChecked.

If you click "Change Input," ngOnChanges, ngDoCheck, ngAfterContentChecked, and ngAfterViewChecked will be called again.

When the component is removed, ngOnDestroy will be called.


This setup will give you a clear view of how each lifecycle hook is triggered in Angular.

---

# Forms in the angular application:

There are 2 main type of form that you can develop in the angular application:

1. Template Driven form
2. Reactive form or Model driven forms

Both of them have their own use case to develop, both of them can be used to make the application more reliable as well. Each type has its own structure, approch and use case.

## Template driven form

We will start with the **template driven form** for the application:

> Template driven forms are easier to set up for the simpler forms, using the angular directives within the HTML to manage form logic.

This is more **declarative** and is more suitable for simpler form with **less complex logic**.

### **Key Characteristics:**

- Good for small form.
- uses angular directive directly in the HTML template
- Automatic binding from form data to model in the component class.
- Suitable for application that dont require highly dynamic form validation or conditional fields.

### Steps to achive Template form

To get started with the template form you need to take up 3 main steps as stated following:

1. Import **FormModule** in app.module.ts
2. Set up the form in the template
3. Access form values and handle submission in the component.

Lets take a deeper dive in the same:

1. Import FormModule in app.module.ts

```TypeScript

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { ChildComponentComponent } from './child-component/child-component.component';
import { FormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    AppComponent,
    ChildComponentComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule // Form modules will be imported in the imports
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

2. Set up the form in the application:
	- We wil try and make the simple user login kind of for the application.
```HTML
<!-- root html -->
<div>
    <app-login></app-login>
</div>
```

```HTML
<!-- LOGIN modules -->


<div>
    <h1>Login form</h1>
    <form #userForm="ngForm" (ngSubmit)="submitEvent(userForm)">
        <div><label for="username">username</label><input type="text" name="username" id="username" ngModel required></div>
        <div><label for="password">password</label><input type="text" name="password" id="password" ngModel required></div>
        <button>Log the information</button>
    </form>
    {{username}}
    {{password}}
</div>
```

3. Accessing the form values and perform some operation on the same.
	- We will be creating the application and we will be logging the same along with printing the values user has entered, in the HTML using interpolation

```TypeScript
import { Component } from '@angular/core';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css']
})
export class LoginComponent {

  username!: String;
  password!: String;

  submitEvent(form: any): void {
    console.log(form.value);

    //TODO: change this to perform some type of operator on the application.

    this.username = form.value.username;
    this.password = form.value.password;
  }

}
```


## Reactive form or Model driven form

Reactive forms, also known as "model-driven forms," are more powerfull and sturctured. They provide more control and flexibility, especially useful for complex forms that require dynamic validation and advance form controls.

**Key Characteristics:**

- Best suited for complex forms with dynamic or conditional field.
- Uses **FormControl, FormGroup, FormArray** to manage form state and validations.
- Validation is handled in the component class rather than the template.
- Allows for more programmatic control makeing it easier to test and maintain.

#### Steps needed to take in order to set up the Reactive forms:

Following are the steps you need to take while creating the reactive forms:

1. **Step 1:** Import **ReactiveFormsModules** in app.module.ts
2. **Step 2:** Set up the form in the component.
3. **Step 3:** Binding the form to the template.

Step 1:

```TypeScript

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { ReactiveFormExampleComponent } from './reactive-form-example/reactive-form-example.component';
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    AppComponent,
    ReactiveFormExampleComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    ReactiveFormsModule // we will be adding this Module for us to make use of formControl and formGroup
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }


```

Step 2:

```TypeScript

import { Component } from '@angular/core';
import { FormControl, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-reactive-form-example',
  templateUrl: './reactive-form-example.component.html',
  styleUrls: ['./reactive-form-example.component.css']
})
export class ReactiveFormExampleComponent {

  userForm: FormGroup = new FormGroup({
    id: new FormControl(0, [Validators.required, Validators.max(10), Validators.min(2)]),
    email: new FormControl('', [Validators.required, Validators.email]),
    name: new FormControl('', [Validators.required, Validators.minLength(2)])
  })

  onSubmit() {
    console.log(`Form values: ${this.userForm.value}`)
  }
}
```

Step 3: 

```HTML

<div>
    <form action="" [formGroup]="userForm" (ngSubmit)="onSubmit()">
        <div><label for="id">ID</label><input type="number" name="id" id="id" formControlName="id"/></div>
        <!-- error handling -->
        <div *ngIf="userForm.get('id')?.invalid && userForm.get('id')?.touched">
            Id is not in the valid format
        </div>

        <div><label for="username">User Name</label><input type="text" name="username" id="username" formControlName="username" /></div>
        <!-- error handling -->
        <div *ngIf="userForm.get('username')?.invalid && userForm.get('username')?.touched">
            username is not in the valid format
        </div>

        <div><label for="email">Email</label><input type="text" name="email" id="email" formControlName="email"/></div>
        <!-- error handling -->
        <div *ngIf="userForm.get('email')?.invalid && userForm.get('email')?.touched">
            email is not in the valid format
        </div>

        <!-- Values to submit the form -->
        <button type="submit" [disabled]="userForm.invalid">Print the data</button>
    </form>
</div>


```

---

#### Service Layer for the Angular application

In this section we will see how we can make use of the service layer for the application. The concept for the service for the angular application do remain the same as any other programming language. 

> The main use of the **service** file is to provide the functionality or data and can be shared across different component in the application. Service are used to organized and manage business logic.

Some of the example where you can make use of the Service class would be as follow:

- Handling HTTP method
- Managing state or data for the application.
- making the reusable code avaialble across the application.

**Why to generate the service file?**

- **Code Reuseability**: Service allow you to reuse code by providing functionality in a centralized place.
- **Separation of Concern**: Service keep business logic or data operations separate from the components, making the application easier to understand and maintain.
- **Dependancy Injections:** Angular's dependancy injection system allows you to inject service into components and other services imporving modularity and testability.
- **State Management**: Services can hold data that needs to accessed by multiple component allowing them to share state.

**How to generate a service file?**

In order for you to generate the service file you can write following command

```Bash

npx @angular/cli@15.2.0 generate service userService

```

This file will generate you 2 file:
1. Service file where you will be keeping all the service file
2. Testing file for the service where you can write some basic testing for the service you have created.

The service file would look something like :

```TypeScript

import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UserServiceService {

  constructor() { }
}

```

A high level explaination for the Decorators:

- @Injectable({providedIn: 'root'}): Marks the class as available for the dependancy injection and registers it at root level, meaning you will be able to use this service throguh out the application

----
#### Dependancy injection for the application from the service layer

We can also inject the dependacy for the application we will try to create some simple application to add, get and remove the application's data, which right now will be in the angular application it self.

We will try and follow the MVC pattern for the application development. We will create the following classes for the development:

1. UserService which we created in the previous step
2. User for the model file; so that it becomes easier to pass the data from controller/ component to the service file.
3. We will be using the Reactive component form that we had used in the previous part for the notes.

```TypeScript

// user model file

class User {
  constructor(
    public id: number,
    public name: string,
    public email: string
  ) {}
}

export default User;


```

```TypeScript

// user service file

import { Injectable } from '@angular/core';
import User from './User';

@Injectable({
  providedIn: 'root',
})
export class UserServiceService {
  data: User[] = [
    { id: 1, name: 'sahil', email: 'sahil@gmail.com' },
    { id: 2, name: 'sid', email: 'sid@gmail.com' },
    { id: 3, name: 'dave', email: 'dave@gmail.com' },
  ];
  constructor() {}

  // add
  add(newData: User): User {
    this.data.push(newData);
    return newData;
  }

  // remove
  remove(id: number): User[] {
    this.data = this.data.filter((tempData) => tempData.id != id);
    return this.data;
  }

  // get
  get(): User[] {
    return this.data;
  }

  getUser(id: number): User {
    let user = this.data.find((tempData) => tempData.id === id)!; // this ! (bang) operator will be used to tell my typescript compiler that this value should never be null
    return user;
  }
}

```

```HTML

<div class="container">
    <form action="" [formGroup]="userForm" class="form-group">
        <div><label for="id" class="form-label">ID</label><input type="number" name="id" id="id" formControlName="id" class="form-control"/></div>
        <!-- error handling -->
        <div *ngIf="userForm.get('id')?.invalid && userForm.get('id')?.touched" class="text-danger">
            Id is not in the valid format
        </div>

        <div><label for="username" class="form-label">User Name</label><input type="text" name="username" id="username" formControlName="username" class="form-control" /></div>
        <!-- error handling -->
        <div *ngIf="userForm.get('username')?.invalid && userForm.get('username')?.touched" class="text-danger">
            username is not in the valid format
        </div>

        <div><label for="email" class="form-label">Email</label><input type="text" name="email" id="email" formControlName="email" class="form-control"/></div>
        <!-- error handling -->
        <div *ngIf="userForm.get('email')?.invalid && userForm.get('email')?.touched" class="text-danger">
            email is not in the valid format
        </div>

        <!-- Values to submit the form -->
        <button type="submit" [disabled]="userForm.invalid" (click)="onSubmit()" class="btn btn-primary form-control mt-3">Print the data</button>
        <button type="submit" [disabled]="userForm.get('id')?.invalid" (click)="onRemove()" class="btn btn-danger form-control mt-3">Print the data</button>
    </form>
</div>


```

```CSS

@import "https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css";

```

```Typescript

import { Component } from '@angular/core';
import { FormControl, FormGroup, Validators } from '@angular/forms';
import User from '../User';
import { UserServiceService } from '../user-service.service';

@Component({
  selector: 'app-reactive-form-example',
  templateUrl: './reactive-form-example.component.html',
  styleUrls: ['./reactive-form-example.component.css'],
})
export class ReactiveFormExampleComponent {
  constructor(private userService: UserServiceService) {}

  userForm: FormGroup = new FormGroup({
    id: new FormControl(0, [
      Validators.required,
      Validators.max(10),
      Validators.min(2),
    ]),
    email: new FormControl('', [Validators.required, Validators.email]),
    username: new FormControl('', [
      Validators.required,
      Validators.minLength(2),
    ]),
  });

  onSubmit() {
    let user: User = this.userForm.value;
    console.log(user);
    this.userService.add(user);
    console.log(`-----------------------`);
    console.log(this.userService.get());
    console.log(`-----------------------`);
  }

  onRemove() {
    let id: number = this.userForm.value.id;
    this.userService.remove(id);
    console.log(`-----------------------`);
    console.log(this.userService.get());
    console.log(`-----------------------`);
  }
}

```

**Common Use Cases for Services**:

1. Data Services: Services for managing API data, typically via HTTP requests, as shown in the example.
2. State Management Services: Services to share and manage the state across components, often useful when multiple components need access to the same data.
3. Utility Services: Services that provide common utility functions (e.g., date formatting or data transformation functions) that can be reused across the application.
4. Authentication Services: Services to manage user authentication, handle login, logout, and manage JWT tokens or other security mechanisms.
5. Notification Services: Services to handle user notifications or alerts, often used to show success/error messages to the user.

Breif idea for the Dependancy injections:

 Dependancy injection is a core concept in Angular that allows classes like component services or other object to request dependancy from external source rather than creating them themselves.

With this you can also promote modularity, flexibility and easier testing.

> Dependancy injection is a design pattern where object (dependancy) are "injected" intot class instead of the class creating the object itself. 

In Angular, DI allows you ro inject dependancies like services directly into component, pipes or other service.

It is usually done with the constructor for the component, where Angular's DI system automatically provides the required dependancies when class is instantiated.

Following are the benifits of using the Angular application:

- Modularity
- Reusability
- Testability
- Maintainability

----
#### HTTP client part for the application

Before we start the application to call the API we will start with understanding the Observable and subscriber pattern for the aplication.

##### Observable

> An observable is like a string that can emit data, complete or throw an error over time. 

In Angular HttpClient method such as get and post returns Observable, which are powerful for managing asynchronous data.

Observable allow you to define a data source and specify what should happen when data is emmited, completed or encounters an error.

These will emit only then the subscriber will be able to emit the request.

Basic Observable Example:

```TypeScript

import { Observable } from 'rxjs';

const observable = new Observable(observer => {
  observer.next('Hello');   // Emit a value
  observer.next('World');   // Emit another value
  observer.complete();      // Signal that the observable is complete
});

observable.subscribe({
  next: (value) => console.log(value),  // Handle emitted values
  error: (error) => console.error('Error:', error),  // Handle errors
  complete: () => console.log('Completed')  // Handle completion
});

```

##### Subscriber:

> A subscriber is an entity that "listens" to an observable.

When you subscripe to an observable you specify what should happen when the observable 
- Emit a new value
- Complete successfully
- Encounters an error

```TypeScript

const subscription = observable.subscribe({
  next: (value) => console.log('Received:', value),
  error: (err) => console.error('Error:', err),
  complete: () => console.log('Done receiving values')
});

```

Key concept for the **Observable** and **subscriber**:

- Asynchornous Handling - it handles the emit in an async manner.
- Laziness - observable will not emit the request, until there is no subsciber listening to it
- Unsubscribing - it can be used for preventing memory leaks

### How to use the same with the HTTP Client?

In Angular, HttpClient is part of the *@angular/common/http* package andis the main way to handle HTTP request to interact with a backend or external API. 

There are 4 main steps you need to work with when working with the HttpClient:

1. Setting up the HttpClient in Angular appliaction in *app.module.ts*

```Typescript

// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, HttpClientModule], // Add HttpClientModule here
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}

```

2. Creating the service file for the application to fetch the application

```TypeScript

// data.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private apiUrl = 'https://jsonplaceholder.typicode.com/posts';

  constructor(private http: HttpClient) {}

  getPosts(): Observable<any> {
    return this.http.get(this.apiUrl); // This returns an Observable
  }

  addPost(post: any): Observable<any> {
	return this.http.post(this.apiUrl, post);
  }

  updatePost(id: number, post: any): Observable<any> {
    return this.http.put(`${this.apiUrl}/${id}`, post);
  }

  deletePost(id: number): Observable<any> {
    return this.http.delete(`${this.apiUrl}/${id}`);
  }

}

```

3. Calling method for the service from the component application.

```TypeScript

// app.component.ts
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-root',
  templateURL: `./app.component.html`
  styleURL: `./app.component.css`
})
export class AppComponent implements OnInit {
  posts: any[] = [];

  constructor(private dataService: DataService) {}

  ngOnInit(): void {
    this.dataService.getPosts().subscribe(
      (data) => {
        this.posts = data;
      },
      (error) => {
        console.error('Error fetching posts:', error);
      }
    );
  }
}

```

4. Updating the HTML Template file for the application

```HTML

<h1>Posts</h1>
<ul>
  <li *ngFor="let post of posts">{{ post.title }}</li>
</ul>
  

```

---

# Angular Routing

Angular routing is an important part for the application for building the application's (SPA).

> With angular application is part for the angular application were you can navigate between the different component for the application's component. 

It can comprise of the different application's view, pages or component.

**Steps for having the angular routing for the application**:

Following are the steps you need to take while working with the angular's routing.

1. Setting up the angular routing
	- To add routing to your application you usually would have an option while creating the project. If you have not specificed the same while creating the application we will be creating them from scratch.
	- To add routing to your existing application you will be required to create the file with the name of **app-routing.module.ts**.
2. Creating the routes
	- For creating the route for the application you will be requiring a couple of modules in the file *app-routing.module.ts*.
	- Most common things you will be requiring would be 
		- RouterModules, Router from the @angular/route
		- Components you want to render (*Login component* and *Register Component*)
		- @NgModule to set up the proxy for the application. 

Following is the example for the base configruration for the application that we can take up for the routing.

```TypeScript

import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { LoginComponent } from './home/login.component';
import { RegisterComponent } from './about/register.component';

const routes: Routes = [
  { path: 'login', component: LoginComponent },  // default route
  { path: 'register', component: RegisterComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

```

3. Importing the route modules for the application's app.module.ts
	- We will be required to import the application in the *app.module.ts* file for getting the functionality for the routing enabled everywhere in the application.
	- Following is the example about how the application would look like for the application in the app.module.ts

```TypeScript

import { AppRoutingModule } from './app-routing.module';

@NgModule({
  declarations: [
    // components
  ],
  imports: [
    AppRoutingModule // this is the routing modules that we had developed in the previous step.
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }


```

4. Router outlet
	- To display the routed component add a \<router-outlet\>\<\/router-outlet> tag  in the application where you want to show the patch of the component being rendered for the application.
	- This will serve as a placeholder for the application, where routed component are rendered.
	- Following is the example for the application.

```HTML

<router-outlet></router-outlet>

```

5. Navigation
	- Angular provides the RouterLink directive for navigation in templates. 
	- You can set the parg you want to navigate to by using the \[routerLink\] in your HTML code.
	- Following would be a base example for the application

```HTML

<a routerLink="/login">Login</a>
<a routerLink="/register">Register</a>

```


**Some of the advance concept for the angular routing would include the following concept**


1. Router with the parameter
	- Say for example you have to pass some data from the browser URL, to other component that can be achived by passing the parameter for the router link.
	- Following is the example for the applicaiton's routing

```TypeScript

{ path: 'user/:id', component: UserComponent }

```

Component
```TypeScript

import { ActivatedRoute } from '@angular/router';

// this will be in the component that needs to be called for the application.
constructor(private route: ActivatedRoute) {
  this.route.params.subscribe(params => {
    const userId = params['id'];
    // Use userId as needed
  });
}

```


2. Redirects and Wildcards
	-  You can also have some wildcard charcter that you can make use of \*\* to catch unknow path and redirect to specific component in the route.
```TypeScript

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: '**', component: PageNotFoundComponent }
];

```


#### Guard 

In Angular, **Guards** are used to control access to routes in an application. They allow you to determine if a route can be accessed, activated or deactivated based on certain conditions. Guards are commonly used for authentication, authorization or preventing navigation if a form is unsave. 

You need to take following three steps to work with the guards for the application developement.

1. Geneating the guard

```TypeScript

ng generate guard auth

```

2. Writing the logic implimentation for the guards.
	1. This might differ from project to project you can make use of it by using the API, or you can also add it to the local storage for the application's browser

3. Add the guards to the route for the application:

```TypeScript

import { AuthGuard } from './auth.guard';

const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] },
  { path: 'profile', component: LoginComponent }
];

```
---