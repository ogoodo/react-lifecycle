
# 此模块仅作组件生命周期的分析, 没有实质性作用  by:ogoodo


# react-lifecycle

Always get stuck in why `componentXXXX` method not being called? Try this useful mixin to log all lifecycle method calls in your component.

## Usage

```
var React = require('react/addons');
var LifeCycle = require('react-lifecycle');

var MyComponent = React.createClass({
  mixins: [LifeCycle],

  render: function(){
    console.log('render');
    return null;
  }
});

React.render(<MyComponent />, document.body);  // 1
React.unmountComponentAtNode(document.body);   // 2
React.render(<MyComponent />, document.body);  // 3
React.render(<MyComponent />, document.body);  // 4
```

which produces the following output:

    // 1
    getDefaultProps
    getInitialState
    componentWillMount
    render
    componentDidMount
    // 2
    componentWillUnmount
    // 3
    getInitialState
    componentWillMount
    render
    componentDidMount
    // 4
    componentWillReceiveProps
    shouldComponentUpdate
    componentWillUpdate
    render
    componentDidUpdate

## Note

Since there should be only one `render` method, this mixin won't log `render` for you, you have to do it yourself.

Thanks to React's great mixin design you don't have to worry about this mixin messing up with your business logic. Anyway, don't forget to remove this mixin when go to production!

See more at [React homepage](http://facebook.github.io/react/docs/reusable-components.html#mixins).
