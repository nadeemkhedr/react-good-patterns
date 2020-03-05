So many different solutions (CSS modules, styled-components, Emotion, etc), all of them have one goal maintainable css
- the ability to add and **REMOVE** css without worrying of breaking the app


We use css-modules (with sass), looks like this:

```javascript
import styles from './Button.module.scss'

const Button = () => {
  return (
    <button className={`${styles.button} ${styles.primary}`}>button</button>
  )
}
```


```css
.button { ... }
.primary { ... }
```
