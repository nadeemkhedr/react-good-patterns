# Hooks

Hooks are cool!

Check https://usehooks.com/ for cool ideas on hooks
some cool ideas:

```javascript
useLocalStorage(key)
useLockBodyScroll()
useDebounce(term, delay)
```

## Basic example (setState)

```javascript
import React, { Component } from "react"

class CounterExample extends Component {
  state = {
    counter: 0
  }
  incrementCount = () => {
    this.setState({ counter: this.state.counter + 1 })
  }
  render() {
    return (
      <div>
        Counter: {this.state.counter}
        <button onClick={this.incrementCount}>Increment</button>
      </div>
    )
  }
}
```

### Hooks

```javascript
import React, { useState } from "react"

const Counter = props => {
  const [counter, setCounter] = useState()
  return (
    <div>
      Counter: {Counter}
      <Button onClick={e => setCounter(++counter)}>Increment</Button>
    </div>
  )
}
```

## Api Listener

```javascript
import React, { Component } from "react"

class ApiListener extends Component {
  componentDidMount() {
    this.listenToApiUpdates(this.props.id)
  }
  componentDidUpdate(prevProps) {
    if (this.props.id !== prevProps.id) {
      this.removeApiListener(prevProps.id)
      this.listenToApiUpdates(this.props.id)
    }
  }
  componentWillUnmount() {
    this.removeApiListener(this.props.id)
  }
  removeApiListener(id) {
    //...
  }
  listenToApiUpdates(id) {
    //...
  }
  render() {
    //...
  }
}
```

### Hooks

```javascript
import React, { useEffect } from "react"

const ApiListener = ({ id }) => {
  useEffect(() => {
    // listenToApiUpdates implementation
    return () => {
      // removeApiListener implementation
    }
  }, [id])
  return // render
}
```


# Custom Hooks

The real reason why hooks are awesome


Example hooks that we use daily:

```javascript
useGetErrorMessage(input)
useUpdateBreadcrumbLastSection(name)
useFormValues(formName, ...fields)
useFormChange(formName)
```
