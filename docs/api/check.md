### `.check(propValue[, options]) => Page`

Check a checkbox

**Default Checked Props:** `id` and `name`

#### Arguments
The `propValue` and `options` arguments are passed to
[`.findWrapperForCheck`][find-wrapper-method] to find a
[`ReactWrapper`][react-wrapper]. The [`ReactWrapper`][react-wrapper] will be
used to simulate events.

1. `propValue` (`String`): Value is compared with the values of the checked
   props to assert a match.
2. `options` (`Object`): Optional.
  * `propToCheck` (`String`): Name of prop to check against instead of the default checked props.

#### Returns

`Page` object which invoked the method. This allow the method to be chained
with another `Page` object method.

#### Simulated Events
If a [`ReactWrapper`][react-wrapper] is found by
[`.findWrapperForCheck`][find-wrapper-method], then the following events will
be simulated on the [`ReactWrapper`][react-wrapper]'s React element:

1. `blur` event on the React element which is focused. This will occur if there
   is a focused React element and it is not the same as the
   [`ReactWrapper`][react-wrapper]'s React element.
2. `focus` event on the [`ReactWrapper`][react-wrapper]'s React element unless
   it is already in focus.
3. `change` event on the [`ReactWrapper`][react-wrapper]'s React element.

If no [`ReactWrapper`][react-wrapper] is found, then an error is thrown.

#### Related Methods

- [`.findWrapperForCheck(propValue[, options]) => ReactWrapper`][find-wrapper-method]
- [`.uncheck(propValue[, options]) => ReactWrapper`](uncheck.md)

[react-wrapper]: https://github.com/airbnb/enzyme/blob/master/docs/api/mount.md#reactwrapper-api
[find-wrapper-method]: findWrapperForCheck.md

#### Example in Jest

```js
import React, { Component } from 'react'
import Page from 'react-page-object'

class App extends Component {
  state = { checked: false }

  onChange = event => this.setState({ checked: event.target.checked })

  render() {
    return (
      <div>
        {this.state.checked ? 'is checked' : 'is not checked'}
        <input
          id="input-id"
          type="checkbox"
          onChange={this.onChange}
          checked={this.state.checked}
        />
        <input
          name="input-name"
          type="checkbox"
          onChange={this.onChange}
          checked={this.state.checked}
        />
        <input
          className="input-class"
          type="checkbox"
          onChange={this.onChange}
          checked={this.state.checked}
        />
      </div>
    )
  }
}

describe('check', () => {
  let page

  beforeEach(() => {
    page = new Page(<App />)
  })

  afterEach(() => {
    page.destroy()
  })

  it('checks the input - targeting id', () => {
    expect(page.content()).toMatch(/is not checked/)
    page.check('input-id')
    expect(page.content()).toMatch(/is checked/)
  })

  it('checks the input - targeting name', () => {
    expect(page.content()).toMatch(/is not checked/)
    page.check('input-name')
    expect(page.content()).toMatch(/is checked/)
  })

  it('checks the input - targeting non-default prop', () => {
    expect(page.content()).toMatch(/is not checked/)
    page.check('input-class', { propToCheck: 'className' })
    expect(page.content()).toMatch(/is checked/)
  })
})
```
