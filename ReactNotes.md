# React Basics:

> React is a **JavaScript** library which is used to make the UI for the application.

It was developed by facebook or Meta. It helps in creation of the single page application where the pages does not reload multiple time but rather only once.

Some of the core concepts you will be working with:
1. Component
2. JSX (JavaScript XML)
3. props
4. state
5. Events
6. Hooks

---

Getting stated with the react application:

```Bash

npm create vite@latest

```

This command will generate the basic boiler plate code for the application

---

### Information about the different concepts:

1. Component:

> Reuseable block of code is called as a component in React.
Following are the type of component avaiable in React application:

1. Functional component
    - It runs based on the function
    ```JavaScript
    import React from "react";

    export function FuncationalComponent(props) {
        console.log(props);
        return (
            <h2>{"Functional component"}</h2>
        )
    }

    ```
2. Class Component
    - We create the class which extends React.component for the application.
    ```JavaScript

    import React, {Component} from "react";

    export class ClassComponent extends Component {

        constructor(props) {
            super(props);
        }

        render() {
            return (
                <h2>{"Class Component"}</h2>
            )
        }
    }
    ```

You can call Component from other Component in the following manner
```JavaScript
import React, { useState } from 'react'
import { ClassComponent } from './components/ClassComponent'
import { FuncationalComponent } from './components/FunctionalComponent'

function App() {

  return (
    <div className="App">
      <FuncationalComponent />
      <hr />
      <ClassComponent />
    </div>
  )
}

export default App

```

NOTE: Now a days it is more common to make use of the Functional component over the Class based component

Some more example showcasing the example for component in React 

```JavaScript

export function EmployeeDisplay({ data }) {
    return (
        <>
            <table className="table table-hover">
                <thead>
                    <tr>
                        <th>Id</th>
                        <th>Name</th>
                        <th>Role</th>
                    </tr>
                </thead>
                <tbody>
                    {
                        data.length ? data.map(row => (
                            <tr key={row.id}>
                                <td>{row.id}</td>
                                <td>{row.name}</td>
                                <td>{row.role}</td>
                            </tr>
                        )
                        ) : <tr><td colSpan="3">No data found</td></tr>
                    }
                </tbody>
            </table>
        </>
    )
}

```

---

### Hooks in React

1. useState:

- useState is a react hook that lets you add the state (data which can change) to a functional component
- It will re-render the component as soon as the application's state changes

```JavaScript

import {useState} from "react";

export function StateComponent() {
    const [data, setData] = useState(0); // this 0 is the inital value for the application.
    return ();
}

```

There are 3 major things when working with the state
- data -> will store the currect value of the state
- setData -> a function to update that state
- initalValue -> starting value for the application

- You can also use state to manage the different form values.
- You can can also pass the value from parent component to the child component, using props

```JavaScript
// App.jsx
export function App() {
    return (
        <>
            <Testing data={"hello"} />
        </>
    )
}
// Testing.jsx
export function Testing({data}) {
    return (
        <p> Value passed is {data} </p>
    )
}

```


```JavaScript

import {useState} from "react";

export function TestingFunction(){ 
    const [name, setName] = useState("");
    return (
        <input type="text" name="name" id="name" value={name} onChange={(e) => setName(e.target.value)}>
        {name}
    )
}

```

2. useEffect

- useEffect lets you run function in a special way. 
- Some of the use cases where you may need to make use of the use effect would be 
    - fetching the data
    - subscribing to event
    - updating the document
    - setting timers

- Base syntax for the application looks like:

```JavaScript

useEffect(() => {}, [])

```

- There are 2 major things when we are working with the use effect hooks
    - **() => {}** : call back function the function that needs to execute for the side effects
    - []           : this array is called as dependancy array, here you will place the state which will help you re render the use effect hooks

- There are 4 major ways you will be working with the useEffect hooks for the application:
    1. **NO DEPENDANCY ARRAY** : if you dont provide a dependancy array for the application, you will be running your useEffect hook for all the state that will get changed
    2. **EMPTY DEPENDANCY ARRAY** : if you dependacy array is empty your useEffect hook will run just once
    3. **ELEMENTS IN DEPENDANCY ARRAY**: if your dependancy array has any state or variable in place, it will re render every time the state is updated
    4. **Return function**: clean up (like removing listener and stopping timer)

```JavaScript

import { useEffect, useState } from "react"

export function UseEffectDemoComponent() {
    const [data, setData] = useState([]);

    useEffect(() => {
        console.log("Use effect is called only once");
    }, []) // this type of function will be called only once

    useEffect(() => {
        console.log(`updated count value is ${count}`);        
    }, [count]) // this will be called only when count is updated

    useEffect(() => {
        console.log(`WITHOUT DA: updated count value is ${count}`);        
    }) // this will be called when the value of any variable changes
    
    function updateCount() {
        setCount(prevCount => prevCount + 1)
    }

    return (
        <>
            <h3>Use Effect demo component is called!!</h3>
            <hr />
            <p>The value for the count is : {count}</p>
            <button onClick={updateCount}>Click</button>
        </>
    )
}



```

3. Router 

> React router is a library that lets you handle navigation in a React app

It allows you to move between different pages and component based on the certain URL and reloads

For you to make use of the application you will need to install for the dependacy for the application

```Bash

npm install react-router-dom

```

For basic Application you will need to work on the following things:

**BrowserRouter** -> wraps the whole app for routing
**Routes** -> group of routes
**Route**  -> Defines each path and component
**Link**   -> Just like a tag with href value

```JavaScript

// main.jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import {BrowserRouter} from "react-router-dom"

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <BrowserRouter>
    <App />
    </BrowserRouter>
  </StrictMode>,
)

// App.jsx
import { Link, Route, Routes } from 'react-router-dom';
import './App.css'
import { ClassBasedComponentDemo } from './component/ClassBasedComponentDemo';
import { UseEffectDemoComponent } from "./component/UseEffectDemoComponent";
import { InsertOperation } from './component/InsertOperation';

function App() {

  return (
    <>
      <Link to="/class">Class Component</Link> <br />
      <Link to="/function">Functional Component</Link> <br />
      <Link to="/add">Input Component</Link>

      <Routes>
        <Route>
          <Route path='/class' element={<ClassBasedComponentDemo />} />
          <Route path='/function' element={<UseEffectDemoComponent />} />
          <Route path='/add' element={<InsertOperation />} />
        </Route>
      </Routes>
    </>
  )
}

export default App
```

4. Connecting the restful web application

> We can make use of the axios dependancy to connect to the application. 

There are 3 ways in which you can connect your backend to the front end
1. axios
2. fetch
3. xhr

For using axios in the react application you need to perform the following operation

```Bash

npm install --save axios

```

```JavaScript

async function fetchData() {
            const data = await axios.get("http://localhost:3000/api/user/");
            console.log(data.data);
            setData([...data.data]);
        }
        fetchData();

```

```JavaScript

async function postMethod(e) {
    e.preventDefault();
    let responseData = await axios.post("http://localhost:3000/api/user/", data);
    console.log(responseData);
}

```

```JavaScript

async function putMethod(e) {
    e.preventDefault();
    let responseData = await axios.put("http://localhost:3000/api/user/", data);
    console.log(responseData);
}

```

```JavaScript

async function deleteMethod(e) {
    e.preventDefault();
    let responseData = await axios.delete("http://localhost:3000/api/user/"+id);
    console.log(responseData);
}

```

5. Redux

> Redux is a state management toolkit / library

- It help you manage the application's state with you having to pass props everywhere
- Useful when the application gets a bit bigger for us to handle with a lot of compoent
- There are 5 specific things you need to work on the when working with redux
    - Store
        - A single place where all the app state lives
        - It is kind of a big data for your front end
    - Action
        - An object to describe what happened to the code
    - Reducer
        - A function that take the current state and an action, then a new state is returned
    - Dispatch
        - A function that sends an action to the store
    - Selector
        - A way to get the data for the application
- Installation for the application will require following dependancy 
```Bash
    npm install @redux/toolkit react-redux
```
- Following are the steps you will be taking when working with the redux

1. Create a redux slice
```JavaScript

import { createSlice } from "@reduxjs/toolkit";

const initialState = {
    value: []
}

const userSlice = createSlice({
    name: "user",
    initialState: initialState,
    reducers: {
        add: (state, action) => {state.value.push(action.payload)}
    }
})

export const {add} = userSlice.actions;
export default userSlice.reducer;

```
2. Create store

```JavaScript

import { configureStore } from "@reduxjs/toolkit";

import userReducer from "../features/user/userSlice";
import counterReducer from "../features/counter/counterSlice";

export const store = configureStore({
    reducer: {
        user: userReducer
    }
})

```

3. provide Store to app (main.jsx)

```JavaScript

import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import App from './App'
import { Provider } from 'react-redux'
import { store } from './app/store'

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
)


```

4. use redux in component

```JavaScript

import { useSelector, useDispatch } from "react-redux";
import { add } from "./userSlice";
import React, { useState, useEffect } from "react";

export default function User() {
    const user = useSelector((state) => state.user.value);
    const dispatch = useDispatch();

    useEffect(() => {
        console.table(user);
    }, [user])

    const [formData, setFormData] = useState({
        id: 0,
        name: "",
        contact: ""
    })

    const [errorFormData, setErrorFormData] = useState({
        id: "",
        name: "",
        contact: ""
    })

    function validate() {
        if (formData.id < 0) { errorFormData.id = "Id is not present"; return }
        if (formData.name == "") { errorFormData.name = "Name is not present"; return }
        if (formData.contact == "") { errorFormData.contact = "Contact is not present"; return }

        setErrorFormData({
            id: "",
            name: "",
            contact: ""
        })

        console.log(errorFormData);
        return true;
    }

    function handleSubmit(e) {
        e.preventDefault();
        if (validate()) {
            console.log("Submit button is handled");
            console.log(`Form: ${JSON.stringify(formData)}`)

            dispatch(add(formData));
        }
    }

    function handleInput(e) {
        e.preventDefault();
        const { name, value } = e.target;
        setFormData(prevFormData => ({ ...prevFormData, [name]: value }))
    }

    return (
        <div className="container">
            <form className="form-group" method="post">
                <div>
                    <label htmlFor="id" className="form-label">Id</label>
                    <input type="text" name="id" id="id" value={formData.id} className="form-control" onChange={(e) => handleInput(e)} onBlur={() => validate()} />
                    {errorFormData.id !== "" && <span className="text-danger">Please check id</span>}
                </div>
                <div>
                    <label htmlFor="name" className="form-label">Name</label>
                    <input type="text" name="name" id="name" className="form-control" onChange={(e) => handleInput(e)}  onBlur={() => validate()} />
                    {errorFormData.name !== "" && <span className="text-danger">Please check id</span>}
                </div>
                <div>
                    <label htmlFor="contact" className="form-label">Contact</label>
                    <input type="text" name="contact" id="contact" className="form-control" onChange={(e) => handleInput(e)}   onBlur={() => validate()}/>
                    {errorFormData.contact !== "" && <span className="text-danger">Please check id</span>}
                </div>
                <button className="w-100 btn btn-primary mt-3" onClick={(e) => { handleSubmit(e) }}>Click to submit</button>
            </form>
        </div>
    )

}

```
