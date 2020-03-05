Reasons for nested routing:

## Nested UI

```javascript
const Component = () => {
  return (
    <Header />
    <Sidebar />
    <Tab to={TAB1}>Tab 1</Tab>
    <Tab to={TAB2}>Tab 2</Tab>

    <Switch>
      <Route
        path={`${match.url}/tab1`}
        component={TabOneContainer}
      />
      <Route
        path={`${match.url}/tab2`}
        component={TabTwoContainer}
      />
    </Switch>
  )
}
```


## State management

```javascript
const Clients = () => {
  useFetchReferences()
  return (
  <Switch>
    <Route exact path={match.url} component={List} />
    <Route path={`${match.url}/:id`} component={Client} />
  </Switch>
  )
}
```


