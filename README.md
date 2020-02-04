# Testing Workshop

***This repository follows along the FrontEndMasters (FEM) react-testing workshop by Kent C. Dodds.


👋 hi there! My name is [Kent C. Dodds](https://kentcdodds.com)! This is a
workshop repo to teach you about testing JavaScript applications.


## Writing a React Test Solution

The basic setup of a test is:
  1. arrange
  2. act
  3. assert
 
 The basic setup of a jest test is:
 ```typescript jsx
import ReactDOM from 'react-dom';

test('Test description goes here', () => {
  // Arrange  
  const container = document.createElement('div');
  // Act  
  ReactDOM.render(<ItemList items={[ 'apple', 'orange', 'pear' ]}/>, container);
  // Assert  
  expect(container.textContent).toBe('appleorangepear');
});
```
This is the component we're testing:
```typescript jsx
import React from 'react'

function ItemList({items}) {
  return items.length ? (
    <ul>{items.map(i => <li key={i}>{i}</li>)}</ul>
  ) : (
    <div>no items</div>
  )
}

export default ItemList

```
...and this is what the test looks like

```typescript jsx
test('Test the case where the items provided is empty', () => {
  const container = document.createElement('div');
  ReactDOM.render(<ItemList items={[]}/>, container);
  expect(container.textContent).toBe('no items');
});
```
**Note:** We're not using `container.innerHTML` because if we ever change the type of HTML Element which`'no items'` 
is wrapped in, we'll have to change the test as well. Using `container.textContent` doesn't care about that and
therefore doesn't break when we wrap `'no items'` in a `<div/>` or a `<span/>`

Matching items in an array is also possible.

```typescript jsx
test('Test the case where there are items in the list', () => {
  const container = document.createElement('div');
  ReactDOM.render(<ItemList items={[ 'apple', 'orange', 'pear' ]}/>, container);
  expect(container.textContent).toMatch('apple');
  expect(container.textContent).toMatch('orange');
  expect(container.textContent).toMatch('pear');
});
```

If DOM structure is relevant, snapshot tests are available (covered later).