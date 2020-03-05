Dispatching fail actions and loading states in reducer is redundant in a way

Examples on why its redundant.

```javascript
// actions
function usersFetchStart() {
  return {
    type: USER_FETCH_START
  }
}
function usersFetchFail() {
  return {
    type: USER_FETCH_FAIL
  }
}
function usersFetchSuccess(users) {
  return {
    type: USER_FETCH_SUCCESS,
    users
  }
}

// reducer
switch (action.type) {
  case USER_FETCH_START:
    return {
      ...state,
      isLoading: true
    }
  case USER_FETCH_FAIL:
    return {
      ...state,
      isLoading: false,
      error: action.error
    }
    case USER_FETCH_SUCCESS:
    return {
      ...state,
      isLoading: false,
      users: action.users
    }
}
```

## What you can do right now:

Loading state:
- use state
- Use middlewares (if you still wanna save data in ur reducers
- Wait for concurrent mode (react suspense)

### if you want react to set the "in progress" state in a component locally, just use `useState`

```javascript
const useGetItems = props => {
  const { getItems } = props
  const [isLoading, setIsLoading] = useState(true)

  useEffect(() => {
    getItems().then(
      () => { setIsLoading(false) }
    )
  }, [getItems])
  return { isLoading }
}
```


### If you want a global spinner
- use ajax interceptors (check axios, `axios.interceptors.request` & `axios.interceptors.response`
- use a wrapper to the `fetch` method that dispatches the actions

If you use an interceptors the solution can be as elegent as have a hook `useGlobalSpinner` that you can use in ur `App.js`


### Eventually best solution:

(https://reactjs.org/docs/concurrent-mode-suspense.html)
```javascript
<Suspense fallback={<Spinner />}>
  <ProfilePage />
</Suspense>
```

## Error state
- use error boundaries (`componentDidCatch`)
- use response interceptors to dispatch fail actions



