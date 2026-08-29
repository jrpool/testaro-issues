# testaro-issues

A classification of about 1300 rules of 10 rule engines into about 350 issues. The rule engines are those in the ensemble of [Testaro](https://github.com/YRA-tech/testaro), which tests web pages for front-end quality (accessibility, usability, and standards conformance).

A _rule engine_ is an application, such as HTML CodeSniffer, that tests software.

An _issue_ is a problem, such as a link that does not tell the user what it links to.

A `rule` is a requirement defined by a rule engine.

When multiple rule engines define rules that require approximately the same thing, the rule engines may test differently and therefore report different results, so [it is advantageous to run an ensemble of rule engines](https://arxiv.org/abs/2304.07591) instead of only one, but it is also helpful to group their reports on similar rules so you can examine their results efficiently. This repository provides such grouping.

## Data

The data exported by this repository consist of three objects, defined in `index.ts`:

- `issues`: An object that describes the issues.
- `rules`: An object that describes the rules and maps them to issues.
- `issueRules`: An object that describes the issues and maps them to rules.

The data underlying the `issues` and `rules` objects are statically defined. Those objects are deep-frozen copies of the data. In other words, `issues` and `rules` and every object within them are protected from modification. The `issueRules` object (not frozen) is generated from the `issues` and `rules` objects by the `makeIssueRules` function.

## Installation

`npm install testaro-issues`

## Usage

### As is

To use the data as-is, import the three exported objects:

```js
const {issues, rules, issueRules} = require('testaro-issues'); // If your application is CommonJS
import {issues, rules, issueRules} from 'testaro-issues'; // If your application is ESM
```

### Customized

The `issues` and `rules` objects represent more than a thousand individual decisions, and you may well want to override some of them by revising the objects. You may want to split an issue, combine two issues, assign a rule to a different issue, or adjust the quality score of a rule. You are welcome to work on that purpose in any of three ways:

- Propose a change in this repository by submitting an [issue](https://github.com/jrpool/testaro-issues/issues).
- Fork this repository, perform the installation and build steps described under “Development” below, revise the `issuesData` and/or `rulesData` objects, and submit a [pull request](https://github.com/jrpool/testaro-issues/pulls).
- Customize the data in your own application as follows, **not** as shown above under “As is”:

   ```js
   const {getEditableData, makeIssueRules} = require('testaro-issues'); // If your application is CommonJS
   import {getEditableData, makeIssueRules} from 'testaro-issues'; // If your application is ESM
   const {issues, rules} = getEditableData();
   // Modify issues and/or rules. Then:
   const issueRules = makeIssueRules(rules, issues);
   // If you introduced any inconsistency, you will get an error message
   ```

## Development

- Clone the repository.
- Install the dev dependencies: `npm install`.
- Build the CommonJS and ESM bundles plus type declarations into `dist/`: `npm run build`
