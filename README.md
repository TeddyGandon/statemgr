![Logo](https://raw.githubusercontent.com/TeddyGandon/icons/master/st.svg?sanitize=true)
# STATEMGR

Just a simple state manager for small JS projects.

# Usage

`npm i statemgr`

# API doc

## Statemgr

### set
`set(property, value)`
Stores a property into the state manager

### get
`get(property)`
Returns a stored property

# Example

Set & get a value:
```js
import Statemgr from "statemgr";

Statemgr.set('foo', 'bar');
console.log(Statemgr.get('foo')); //bar
```

Subscribe to some changes:
```js
import Statemgr from "statemgr";
import {Observer} from "obsrvble";

const foo = new Foo();
foo.subscribe(new Observer(
    'foo',
    params => {
        // Do something here
        console.log(params[0]); // hello!
    }
));
Statemgr.set('foo', 'bar');
```
