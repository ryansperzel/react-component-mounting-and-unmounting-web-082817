# React: Component Mounting and Unmounting

## Objectives

1. Describe what happens in the mounting phase of a React component's lifecycle
2. Describe what happens in the unmounting phase of a React component's
   lifecycle

## Overview

A React compoment has distinct phases for creation and deletion. In coding terms, these are called **mounting** and **unmounting**. These phases are conceptually quite a lot like "setup" and "cleanup".

If you were going to have a picnic for example, before you lay down the picnic blanket, you'd make sure the ground was level and clean. Afterwards when you clear up your picnic blanket, you'd make sure you've taken all your belongings off it first and cleared up any rubbish left on the grass so next people could easily use the same spot.

That's pretty much what happens with React somponents as well. The browser window is almost like a great big field which loads of components can use, and when they leave, it's only polite to clean up the space they were using so that other components could reuse the same space without difficulties due to things left behind.

## Mounting

In the mounting (or creation, or "setup") phase, we have two **lifecycle methods** we can have access to: **componentWillMount** and **componentDidMount**.

### componentWillMount

In picnic terms, **componentWillMount** is when you arrive at the field with your picnic blanket and you check of the spot you've chosen is nice and level. You might find some twigs or little rocks you need to clean up before you out your blanket down.

In React terms, the use-cases for this are quite subtle, but for example, suppose you wanted to keep the time and date of when the component was created in your component state, you could set this up in **componentWillMount**.

```javascript
componentWillMount: function(){
  this.setState({ startDateTime: new Date(Date.now())});
}
```

### componentDidMount

In picnic terms, this is the moment just after you've laid out your blanket. Now you can lay out all your food and drinks, maybe take out a radio and put some music on.

In React terms, this is where you would set up any long-running processes, for example fetching data. Suppose we were building a weather app which fetches current weather data and displays it to the user. We would want this data to update every 15 seconds without the user having to refresh the page. **componentDidMount** to the rescue!

```javascript
componentDidMount: function(){
  this.interval = setInterval(this.fetchWeather, 15000);
}
```

## Unmounting

I the unmounting (or deletion, or "cleanup") phase, we have just one **lifecycle** method to help us out: **componentWillUnmount**.

In picnic terms, **componentWillUnmount** is just before you pick up your picnic blanket. You need to clean up all the food and drinks you've set on the blanket first or they'd spill everywhere! You'd also have to shut down your radio. Only when that's all done, you can pick up your picnic blanket and put it back in the bag.

In React terms, this is where you would clean up any of those long running processes that you set up in **componentDidMount**. For the above data fetching example, that would just be clearing the interval:

```javascript
componentWillUnmount: function(){
  clearInterval(this.interval);
}
```

## Summary

The mounting step is important as here we can set up any special requirements we may have for that particular component: fetch some data, start counters etc. It is extremely important to clear any of these things we set up in the unmounting stage in **componentWillUnmount**, as not doing so may lead to some pretty nasty consequences - even your website crashing!


### Mounting lifecycle methods
Called once on initial render:

| Method             | nextProps | nextState | can call this.setState | called when?               | used for                                                                                    |
|--------------------|:---------:|:---------:|:----------------------:|:--------------------------:|:-------------------------------------------------------------------------------------------:|
| **componentWillMount** |     no    |     no    |           yes          | once, just before mounting | setting initial state based on props                                                        |
| **componentDidMount**  |     no    |     no    |           no           | once, just after mounting  | setting up side effects (e.g. creating new DOM elements or setting up asynchronous functions |


### Unmounting lifecycle method
Called only once, just before the component is removed form the DOM:

|        Method        | nextProps | nextState | can call this.setState |                     called when?                    |                         used for                        |
|:--------------------:|:---------:|:---------:|:----------------------:|:---------------------------------------------------:|:-------------------------------------------------------:|
| **componentWillUnmount** |     no    |     no    |           no           | once, just before component is removed form the DOM | destroying and side effects set up in componentDidMount |


## Resources

- [React: Component Specs and Lifecycle](https://facebook.github.io/react/docs/component-specs.html)
