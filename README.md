# redux-form-validate-rules

A rule set of redux-form validation with custom message.
Work with redux-form validation v7.

see http://redux-form.com/7.0.3/examples/syncValidation/
for redux-form validate

## Example

```javascript
import { Field, reduxForm } from 'redux-form'
import rules from './rules'

// ....

const titleRequired = rules.required(`Post title is required.`)
const titleMaxLength128 = rules.maxLength(`Post title length must atmost :arg1 characters`)(128)
const titleMinLength5 = rules.minLength()(5)
const titleSame = rules.same()('title')

// ...

<Field 
	component={renderField} 
	type="text" 
	name="title" 
	id="title" 
	placeholder="Title here"
	validate={[titleRequired, titleMaxLength128, titleMinLength5]} />

<Field 
	component={renderField} 
	type="text" 
	name="title_recheck" 
	id="title_recheck" 
	placeholder="Title here too"
	validate={[titleSame]} />


```

![Image of Validate](https://i.imgur.com/7T85WiR.jpg)

---
## Custom Message
You can provide custom error message when setting rules.
example 
```javascript
const titleRequired = required('This title is required')
```
This library is provide a way to make message more dynamic with
- `:arg1` will be replace with validate rule argument with specific index
- `:args` will be replace with validate rule arguments join with comma(,)
- `:name` will be replace with field name
- `:value` will be replace with current field value


---
## Available Rules

Rule | Params | Example
------------ | ------------- | -------------
required | none | `required('This field is required')`
maxLength | max-length : int | `maxLength('Must have length at most :arg1')(100)`
minLength | min-length : int | `minLength('Must have length at least :arg1')(5)`
alpha | none | `alpha('Must contain only alphabet character')`
alphaNumeric | none | `alphaNumeric('Must contain only alphabet character or digit')`
alpheDash | none | `alphaNumeric('Must contain only alphabet character or dash')`
number | none | `number('This field must be a number')`
number | none | `number('This field must be a number')`
email | none | `email('Invalid email pattern')`
minValue | minimum-value : number | `minValue('Must have value at least :arg1')(10)`
maxValue | maximum-value : number | `maxValue('Must have value at most :arg1')(10)`
same | field-name : string | `same('This field value must match with :arg1, found :value')('email')`
difference | field-name : string | `difference('This field value must contain value difference from :arg1, found :value')('email')`
accepted | none | `accepted('Must accept this term of use')`


---

## Default Message 
```
const _def = {
	required: 'Required',
	maxLength: `Must be :arg1 characters or less`,
	minLength: `Must be :arg1 characters or more`,
	alpha: 'Only alphabet characters',
	alphaNumeric: 'Only alphanumeric characters',
	alphaDash: 'Only alphabet or dash characters',
	number: 'Must be a number',
	email: 'Invalid email address',
	minValue: `Must be at least :arg1`,
	maxValue: `Must be at most :arg1`,
	same: `This must have same value as :arg1`,
	difference: `This must have difference value as :arg1`,
	accepted: `Must accept this first`
}

```