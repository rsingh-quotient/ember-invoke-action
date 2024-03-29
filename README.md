# ember-invoke-action
[![NPM Version](https://badge.fury.io/js/ember-invoke-action.svg)](http://badge.fury.io/js/ember-invoke-action)
[![Build Status](https://travis-ci.org/martndemus/ember-invoke-action.svg?branch=master)](https://travis-ci.org/martndemus/ember-invoke-action)
[![Ember Observer Score](http://emberobserver.com/badges/ember-invoke-action.svg)](http://emberobserver.com/addons/ember-invoke-action)

A slightly more idiomatic way to invoke actions in your Ember components.

## Compatibility

* Ember.js v4.4 or above
* Ember CLI v4.4 or above
* Node.js v14 or above


## Installation

```
ember install ember-invoke-action
```

## How To

You can either use `ember-invoke-action` as a helper function or a mixin.
## Usage

### Mixin usage

```javascript
import Ember from 'ember';
import { InvokeActionMixin } from 'ember-invoke-action';

export default Ember.Component.extend(InvokeActionMixin, {
  click(...args) {
    this.invokeAction('click', ...args);
  }
});
```

### Helper usage

```javascript
import Ember from 'ember';
import { invokeAction } from 'ember-invoke-action';

export default Ember.Component.extend({
  click(...args) {
    invokeAction(this, 'click', ...args);
  }
});
```

### `strictInvokeAction`

As alternative to `invokeAction` you can call `strictInvokeAction`.
`strictInvokeAction` is functionally the same as `invokeAction` except for when
the given action could not be found, then `strictInvokeAction` will raise an
`AssertionError`.

### `invoke`

With the `invoke` helper you can call other actions from the `actions` object as
if it is a closure action.

```javascript
import Ember from 'ember';
import { invoke } from 'ember-invoke-action';

export default Ember.Component.extend({
  actions: {
    saveModel() {
      return get(this, 'model').save();
    },

    closeModal() {
      set(this, 'modalVisible', false);
    },

    saveModelAndClose(...args) {
      invoke(this, 'closeModal');
      return invoke(this, 'saveModel');
    }
  }
});
```

### Linting

* `npm run lint:js`
* `npm run lint:js -- --fix`

### Running tests

* `ember test` – Runs the test suite on the current Ember version
* `ember test --server` – Runs the test suite in "watch mode"
* `ember try:each` – Runs the test suite against multiple Ember versions

## Credits

This code was inspired by @miguelcobain, I just made an addon out of it.

License
------------------------------------------------------------------------------
## Contributing

See the [Contributing](CONTRIBUTING.md) guide for details.


## License

This project is licensed under the [MIT License](LICENSE.md).
