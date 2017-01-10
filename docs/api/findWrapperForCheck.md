### `.findWrapperForCheck(propValue[, options]) => ReactWrapper`

Find a checkbox

#### Arguments

1. `propValue` (`String`): Value is compared with the values of the checked props to assert a match.
2. `options` (`Object`): Optional.
  * `propToCheck` (`String`): Name of prop to check against instead of the default checked props.

#### Returns

[`ReactWrapper`][react-wrapper] for an `input` React element whose:
  1. `id` or `name` prop value equals `propValue`
  2. `type` prop equals `'checkbox'`

If `options.propToCheck` is specified, then the method returns a
[`ReactWrapper`][react-wrapper] for an `input` React element whose:
  1. value for the prop specified by `options.propToCheck` equals `propValue`
  2. `type` prop equals `'checkbox'`

#### Related Methods

- [`.check(propValue[, options]) => ReactWrapper`](check.md)
- [`.uncheck(propValue[, options]) => ReactWrapper`](uncheck.md)

[react-wrapper]: https://github.com/airbnb/enzyme/blob/master/docs/api/mount.md#reactwrapper-api