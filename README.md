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

### setReducer
`setReducer(dispatcher)`
Set a reducer (a method that will be called for complex set). The reducer will be called with 2 arguments: the parameters passed to the reducer call & the `set` method of the state manager.

### reduce
`reduce(...params)`
Call the reducer.

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

Statemgr.subscribe(new Observer(
    'foo',
    params => {
        // Do something here
        console.log(params[0]); // bar
    }
));
Statemgr.set('foo', 'bar');
```
Call the reducer:
```js
import Statemgr from "statemgr";
import {Observer} from "obsrvble";

Statemgr.subscribe(new Observer(
    'total',
    params => {
        // Do something here
        console.log(params[0]);
    }
));

Statemgr.set('total', 0);
Statemgr.setReducer((params, set) => {
    if (params[0] === 'add') {
        set('total', Statemgr.get('total') + 1);
    }
    if (params[0] === 'sub') {
        set('total', Statemgr.get('total') - 1);
    }
});

Statemgr.reduce('add'); //1
Statemgr.reduce('add'); //2
Statemgr.reduce('sub'); //1
```