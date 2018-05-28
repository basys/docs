### Linting

Basys toolbox comes with a pre-configured linting for code and styles, which
* finds issues in your code and help to follow the best practices,
* detects and fixes formatting issues.

Linting is integrated into Basys IDE and works out of the box. If you are using Basys CLI use `basys lint` to print all linting errors and `basys lint:fix` to fix formatting issues.

#### Code linting

JavaScript linting, performed by [ESLint](https://eslint.org) and [Prettier](https://prettier.io), is applied to `.js` and `.vue` files. By default [eslint-config-basys](https://github.com/basys/basys/tree/master/packages/eslint-config-basys) is used, but you can customize ESLint rules by adding `.eslintrc.*` file to the project root directory. For more information see the documentation on [configuring ESLint](https://eslint.org/docs/user-guide/configuring). For example, to add more rules add the following `.eslintrc.js` file:
```javascript
module.exports = {
  extends: 'basys',
  rules: {
    // Your custom ESLint rules
  },
};
```
To exclude some code from being linted create [`.eslintignore` file](https://eslint.org/docs/user-guide/configuring#ignoring-files-and-directories).

#### Style linting

Style linting, based on [stylelint](https://stylelint.io) and [Prettier], is applied to `.css`/`.less`/`.scss`/`.vue` files.

By default the stylelint rules from [stylelint-config-basys](https://github.com/basys/basys/tree/master/packages/stylelint-config-basys) are used. You can customize them by adding `.stylelintrc` file to the project root directory (see [how to configure stylelint rules](https://stylelint.io/user-guide/configuration/#the-configuration-object)). For example,
```javascript
{
  "extends": "stylelint-config-basys",
  "rules": {
    // Your custom stylelint rules
  }
}
```

To exclude some styles from being linted (say a CSS file from a 3rd party library) use [`.stylelintignore` file](https://stylelint.io/user-guide/configuration/#stylelintignore).
