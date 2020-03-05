# PropTypes

Please don't use
- `PropTypes.any`
- `PropTypes.object`
- `PropTypes.array`
- `PropTypes.string` // for enums

use instead:
- `PropTypes.oneOfType`
- `PropTypes.shape`
- `PropTypes.arrayOf`
- `PropTypes.oneOf`


## Examples


```javascript
Dropdown.propTypes = {
  options: PropTypes.arrayOf(
    PropTypes.shape({
      label: PropTypes.string,
      value: PropTypes.string
    })
  ),
  //...
}
```

```javascript
// sectionTypes lives in constants and is used in the app logic
export const sectionTypes = [PANE, TABLE, CODE]

export const sectionProp = {
  type: PropTypes.oneOf(sectionTypes), // 'pane' is default
  title: PropTypes.string,
  titleHelper: PropTypes.string,
  count: PropTypes.number,
  column: PropTypes.number,
  valueAlign: PropTypes.oneOf(['left', 'right']), // 'left' is default
  data: PropTypes.oneOfType([
    simplePaneProp,
    codeProp,
    keyValuePaneProp,
    tableProp
  ])
}
```


# JSDoc

Specially Document reuseable functions and hooks
same rule apply specially for `object` don't js define the params as objects

## Examples

```javascript
/**
 * a hook that runs everytime the name changes and resets when the page changes
 * the breadcrumb populates the label from the url, this is used when wanting to
 * info that is not in the url, like name instead of id
 * @param {string} name the name to set the last section to
 */
export const useUpdateBreadcrumbLastSection = name => {..}
```

```javascript
/**
 * This is intended to be used inside the validate function of the whole form in redux-form
 * A validation function that validates ranges with the following rules:
 * - every item in the range has a start and an end
 * - range must start with 1 and ends with 999
 * - the first start of the first item in the range must be 1
 * - the last end of the last item in the range must be 999
 * - there can't be any gabs, for example if first item is 1-10, then 2nd item must start with 11
 * - there can't be any intersection, for example if the first item is 1-10, then 2nd item can't start with any item between 1-10
 * @param {array} range the range array must have options.fromKey and
 * options.endKey props
 * @param {object} [options] optional options to specify the prop keys in the
 * ranges
 * @param {string} [options.fromKey=fromDay] the from day key in each range item
 * @param {string} [options.toKey=toDay] the to day key in each range item
 * @return {array} the returned validation for the range, used inside the
 * `validate` function in a form
 */
const validateRange = ( range,
  options = { fromKey: 'fromDay', toKey: 'toDay' }
) => {
  // ...
}
```
