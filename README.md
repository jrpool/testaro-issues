# testaro-issues

A classification of about 1300 rules of 10 rule engines into about 300 issues. The rule engines are those in the ensemble of Testaro, which tests web pages for front-end quality (accessibility, usability, and standards conformance).

## Installation

`npm install testaro-issues`

## Usage

```js
const {issues, rules, issueRules} = require('testaro-issues'); // If your application is CommonJS
import {issues, rules, issueRules} from 'testaro-issues'; // If your application is ESM
```

## Customizing

The `issues`, `rules`, and `issueRules` objects exported by this package are locked (technically, “deep-frozen”) to prevent anybody from modifying them. This is because editing one table could corrupt the data. For example, if the name of an issue in the `rules` object were changed to a name that is missing from the `issues` object, the objects would become incompatible. In fact, any change in the `rules` object would necessitate a corresponding simultaneous change in the `issueRules` object.

However, these three objects represent more than a thousand individual decisions, and you may well want to override some of them by revising the objects. You may want to split an issue, combine two issues, or assign a rule to a different issue, or adjust thequality score of a rule. You are welcome to do that in either of two ways:

- Propose a change in this repository by submitting a [pull request](https://github.com/jrpool/testaro-issues/pulls) or [issue](https://github.com/jrpool/testaro-issues/issues).
- Create your own custom version of this repository and revise the objects in your version. To do that, make your application use these data as follows, **not** as shown above under “Usage”:

   ```js
   const {getEditableData} = require('testaro-issues'); // If your application is CommonJS
   import {getEditableData} from 'testaro-issues'; // If your application is ESM
   const {issues, rules, issueRules} = getEditableData();
   ```

## Development

Clone the repository and install the dev dependencies:

`npm install`

Build the CommonJS and ESM bundles plus type declarations into `dist/`:

`npm run build`
