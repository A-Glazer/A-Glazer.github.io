---
layout: post
title:      "Converting Functional to Class Components"
date:       2020-03-27 17:52:52 +0000
permalink:  converting_functional_to_class_components
---


## Functional vs. Class Components
There are a couple differences between `functional` and `class components`. `Functional components` are simple components that don’t create anything new and used mainly as `presentational components`. They have no `state` or `render`, all the props are passed in as an argument and it is written in plain javaScript. `Class components` are much more complex. They require a `render()` method, can have `state`/`setState`, lifecycles, and need to extend a component. 

Imagine you had a `functional component` you wanted to add a checkbox to. If the checkbox is not ticked, you would display all arrays. If it is ticked, you would display only the arrays that are not empty. The best way to do this would be creating a `state` of `checkbox: false` and changing the value to `true` if ticked.  Because you need to use `state`, a `class component` should be used instead of a `functional component`. 

Here is the original function:
```
Functional Component:

const Slots = ({ babysitter, deleteSlot }) => {
    return (
        <div>
            {babysitter.slots.map(slot => { return card(slot) })}
        </div>
    )
}
export default Slots
```

To switch to a class component: 

```
Class Component:

	class Slots extends React.Component { 
	
	// when using a class component, you need to extend Component or you can import it: import React, {Component} from ‘react’
	// notice how no props/arguments are imported. This is because they are imported by default in a class component
	
	state = {checkbox: false}
	
  // state does not need to be defined unless you are adding a new state. In our case, we are adding a checkbox.


    handleChange = () => {
       this.setState( (state) => {
          return { checkbox: !state.checkbox }
       // in this function, we are taking in the state and switching the boolean to either true or false
       })
    }

    render() {
        let { babysitter, deleteSlot } = this.props
        let slotList = this.state.checkbox ? babysitter.slots.filter(s => {
            return s.time_of_day.length != 0
        }) : babysitter.slots
        return (
            <div>
                <input type="checkbox" onChange={this.handleChange} />
                {slotList.map(slot => { return card(slot) })}
            </div>
        )
}
export default slots
```

Note: Since `render` is a pure method, any `onChange`,` onSubmit`, `onClick` etc. needs to be defined outside of the `render`  


## Binding Functions to This
Look at the `onChange={this.handleChange}` function written above. `This` can't be used in a `functional component`, but it can be in a `class component`. Even so, `this` can be accessed inline, but can't be passed down to the called functions. However, in the example above, you will notice `onChange` is calling of `this.handleChange`. How does the `onChange` function have access to `this`? There are a few ways.

The easiest way is to make an `arrow function`. `Arrow functions` always represent the object it is being called on and therefore have access to `this`. 

Another option is to `bind this`. You would call `onChange = {this.handleChange.bind(this)}`. This allows `this` to be called in the function. *Note: when passing down `this`, it will pass down whatever `this` is at the time of being called.*

## Comparing Objects and Arrays
The method we are trying to create needs to display the ` time_of_day` that had available slots (ie. not empty arrays). It would seem you can just call `s.time_of_day != []`. However, since you cannot compare arrays and objects to each other, the log will always come back `true`. Instead, you would need to compare the values or length in the array to check if it is empty. In javaScript, strings and numbers are compared by their value, but objects and arrays are compared by their reference location. So even if there are 2 arrays with the same item in each, they won’t equal each other since they are not from the exact same reference location. To solve this, you would need to be more specific. If you are looking to see if the array is empty, try `array.length != 0`. If you want to find both arrays contain the same item, check the array’s values.
```
render() {
        let { babysitter, deleteSlot } = this.props
        let slotList = this.state.checkbox ? babysitter.slots.filter(s => {
            return s.time_of_day.length != 0
        }) : babysitter.slots
        return (
            <div>
                <input type="checkbox" onChange={this.handleChange} />
                {slotList.map(slot => { return card(slot) })}
            </div>
        )
```

