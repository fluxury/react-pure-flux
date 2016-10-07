# react-pure-flux

[![CircleCI](https://circleci.com/gh/WebsiteHQ/react-pure-flux.svg?style=svg)](https://circleci.com/gh/WebsiteHQ/react-pure-flux)

Bind [pure-flux](https://github.com/WebsiteHQ/pure-flux) stores to [React.js](https://facebook.github.io/react/).

## Install

```sh
npm install --save react-pure-flux pure-flux
```

## Example

Wrap any component with a connect component.

```js
var Component = require('react').Component;
var {createStore, dispatch} = require('pure-flux');
var {connectStore} = require('react-pure-flux');

var countStore = createStore("CounterStore", (state={ count: 0 }, action) => {
  switch (action.type) {
    case 'increment':
    return { count: state.count+1 };
    default:
    return state;
  }
});

class MyComponent extends Component {

  handleUpClick() {
    dispatch('increment')
  }

  handleDownClick() {
    dispatch('decrement')
  }

  render() {
    return (
      <div>
        <p>{this.props.count}</p>
        <button onClick={this.handleUpClick}>+1</button>
        <button onClick={this.handleDownClick}>-1</button>
      </div>
    );
  }

});

EnhancedComponent = connectStore(countStore, MyComponent, (state) => {
  count: state
})
```
