## What problems / warnings are there with code?

### first correction

```javascript
WrappedListComponent.propTypes = {
  items: PropTypes.array(
    PropTypes.shapeOf({
      text: PropTypes.string.isRequired,
    })
  ),
};
```

The above code is wrong and should be replaced with

```javascript
WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(
    PropTypes.shape({
      text: PropTypes.string.isRequired,
    })
  ),
};
```

### second correction

```javascript
const [setSelectedIndex, selectedIndex] = useState();
```

above code on line 47 should be replaced with

```javascript
const [selectedIndex, setSelectedIndex] = useState();
```

### third correction

Add optional chaining in below code to

```javascript
 {items?.map((item, index) => (
```

so that map is never run on `undefined` and throw error.

### fourth correction

Add a key here below

```javascript
<SingleListItem
  onClickHandler={() => handleClick(index)}
  text={item.text}
  index={index}
  isSelected={selectedIndex}
  key={index}
/>
```

Key should be unique and assigning it's value of `index` should be avoided

### fifth correction

`onClick` wants a function body, not directly invoke the function inside it.
Below is the corrected code

```javascript
<li
  style={{ backgroundColor: isSelected ? "green" : "red" }}
  onClick={() => onClickHandler(index)}
>
  {text}
</li>
```
