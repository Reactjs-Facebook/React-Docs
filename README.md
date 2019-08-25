# React-Tutorial

* http://designwebkit.com/tutorials/learn-react-js/
## Component Specification
* methods dealing with the component life cycle, such as `componentDidMount`, `componentShouldUpdate`
* setting initial data, such as `getInitialState` and `getDefaultProps`
### Props and states
Data within a component can come from the outside (props) or be instantiated from the inside (states).
* The `render` method is the only required method in a ReactJS component. 
* `Props` cannot be modified and should be treated as immutable.
* You can send as many properties as you want, and they are always available under this.props

### State
A state is primarily used when you make changes that only make sense within the component.
`...state` - spread operator is used for return current state
