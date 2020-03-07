---
layout: post
title:      "The Importance of Debugging"
date:       2020-03-07 18:54:15 +0000
permalink:  the_importance_of_debugging
---


Creating the final project in Flatiron School has been an amazing learning experience. One of the most fundamental concepts in programming, is the value of debugging. When working on an app that has both front-end and backend, it is important to pinpoint exactly where the issues are coming from. Here is a great process to accomplish this.

## Step 1

The first step in creating the application is the backend. This will help minimize the errors and help you map out what is needed for the project. After creating the CRUD methods, it is important to test out the controller to make sure it is working properly. To do this in Rails, run the console and try adding a new object. Make sure it is saving correctly to the database. 

## Step 2
Once you are confident the backend is working, it is time to create the front-end. One of the most common errors that can occur is the object is undefined. Here are a few common reasons: 

1. The object is not fully loaded 
2. The object is not being passed down correctly via props
3. The object is not being called correctly

It is very important to use `console.log` or debugger after every new line of code. `Console.log` is great in finding out what the object is returning. Often the object may be returning something you weren't expecting and a `console.log` could prevent further errors. Every time you call on an object or pass down props, `console.log` the title to find out what it is. 

### Is Loading

An object not fully loading is a common error. Since React is async, the functions are not being run in order. This can be especially problematic when there is a fetch request. Async means that all the functions will run at once and it will be displayed when ready. However, if you are relying on the existance of the object for the rest of the functions to work, you need a way in making the fetch synchronous. To achieve this, create a loading action.

```
export const addBabysitter = data => {

    return (dispatch) => {
        dispatch({ type: 'LOADING_BABYSITTERS' })
        fetch('http://localhost:3000/api/v1/babysitters', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            body: JSON.stringify(data)
        })
            .then(response => response.json())
            .then(babysitter => dispatch({
                type: "ADD_BABYSITTER",
                payload: babysitter
            }))
    }

}
```

Notice how dispatch is being called before the fetch request. This is telling the app that the first action it should do is the `LOADING_BABYSITTERS` request. The app will go to the babysitterReducer and run the code defined in under `LOADING BABYSITTERS`. Since the application is asyncronous, the app will be running the fetch request and creating a new babysitter at the same time. Once it is complete, it will make the response json and run the `ADD_BABYSITTER` action. 
But how does the app know to only return the babysitters once the fetch is complete? That is where loading comes in to play. In the reducer, there is a default state of `loading: true`. This will make sure that it runs any case that has `loading: true`. The `LOADING_BABYSITTERS` case has a loading of true and therefore it will run automatically. `ADD_BABYSITTERS` has a loading value of false. This will prevent the babysitter from displaying until loading is completed. 
*Note: creating a loading action is extremely important. This will avoid many undefined errors since the object will not display or be called on until it has loaded.

## Step 3
So let’s say your app is loading properly and you’ve tried `console.log` and you still can’t find an error? Next option is to try `debugger` and finding out where your app is running into an issue. Try each step until you find out what is going wrong. I learned to put a `debugger` in each method and see if it is hitting it. Often you will see that it is skipping over a method. 
It is also important to put in `binding.pry` in the backend. If the object is not creating properly, it could be it is not being sent correctly to the backend. With pry in place, you can check the params to see what is happening on the backend side. 

### Fetch Requests
Having a fetch request can cause a series of bugs if not done properly. I had an error that got me stuck for days: `Problems loading reference 'https://schemastore.azurewebsites.net/schemas/json/package.json': Unable to load schema from 'https://schemastore.azurewebsites.net/schemas/json/package.json': connect ETIMEDOUT 168.62.224.13:443.(768) ?`The network tab showed `sockjs-node type:websocket status: 101 time: pending`. 
After many days of searching the web and asking advice, I added a `console.log` to my fetch request. The `console.log` showed that the fetch was not working properly! Since I hadn’t put in a `console.log(error`, I had no clue what was wrong! So yes, as annoying as `console.log`, `debugger`s and `binding.pry`s are, they can save you A LOT of time avoiding later issues.

