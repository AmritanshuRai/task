## Please fix, optimize, and/or modify the component as much as you think is necessary.

```javascript
import React, { useState, useEffect, memo } from "react";
import PropTypes from "prop-types";

// Single List Item
const WrappedSingleListItem = ({ index, isSelected, onClickHandler, text }) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? "green" : "red" }}
      // fixed below line of code from answerTwo.md
      onClick={() => onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};
// No need to memoize this component because this component will re-render anyway because of props change.
// And even if props do not change the inline function in Parent component will make this component re-render anyway.
// So, it's better not to invoke 'props comparison function' everytime in this component.

// const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({ items }) => {
  // fixed below line of code from answerTwo.md
  const [selectedIndex, setSelectedIndex] = useState(null);

  // removing this useEffect from here and putting the value directly in useState above because it does the same thing
  // useEffect(() => {
  //   setSelectedIndex(null);
  // }, [items]);

  const handleClick = (index) => {
    setSelectedIndex(index);
  };

  return (
    <ul style={{ textAlign: "left" }}>
      {items.map((item, index) => (
        <WrappedSingleListItem
          //just pass the function callback because we are already passing the index
          onClickHandler={handleClick}
          text={item.text}
          index={index}
          isSelected={selectedIndex}
        />
      ))}
    </ul>
  );
};

// fixed below line of code from answerTwo.md
WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(
    PropTypes.shape({
      text: PropTypes.string.isRequired,
    })
  ),
};

WrappedListComponent.defaultProps = {
  items: null,
};

const List = memo(WrappedListComponent);

export default List;
```
