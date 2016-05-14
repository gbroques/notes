#Getting Started With Redux by Dan Abramov
Taken from the [Egghead.io](https://egghead.io/series/getting-started-with-redux) video series.

---

##The Single Immutable State Tree
__The first principle of redux__ - everything that changes in your application is contained in a javascript object called the state or state tree.

##Describing State Changes with Actions
__The second principle of redux__ - the state tree is immutable, you cannot modify or write to it.

Anytime you want to change the state, you must dispatch an action.

An _action_ is a plain javascript object describing, in the minimal way, the change you want to make.

Just like the state is the minimal representation of the data in your app, the action is the minimal representation of the change to that data.

The structure of the action object is up to you.

The only requirement is a `type` property that's not undefined.

Dan recommends you define the `type` property with a `string` because they're serializable.

##Pure and Impure Functions

__Important:__ Some functions in Redux have to be pure.

###Pure Functions
- Return values depend solely on the values of their arguments
- No observable side effects, such as network or database calls
- Predictable, if called with same arguments you get the same value
- Do not modify the values passed to them

###Impure Functions
- May call the database or network
- May have side effects
- May operate on the DOM
- May modify the values passed to them

```js
// Pure functions
function square(x) {
    return x * x;
}
function squareAll(items) {
    return items.map(square);
}

// Impure functions
function square(x) {
    updateXInDatabase(x);
    return x * x;
}
function squareAll(items) {
    for (let i = 0; i < items.length; i++) {
        items[i] = square(items[i]);
    }
}
```

##The Reducer Function
The UI or the view layer is most predictable when described as a _pure function_ of the application state.

Redux complements this approach with another idea.

__The third principle of redux__ - state mutations in your app need to be described as a pure function that takes in the _previous state_ and the _action being dispacted_, and returns the _next state_ of your application.

This function is called the __reducer__.

