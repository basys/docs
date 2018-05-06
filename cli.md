### CLI

Basys CLI can be installed globally using npm

```bash
npm install -g basys-cli
```
or Yarn:
```bash
yarn global add basys-cli
```

The following commands are available:

#### basys init [starter-template]

Initializes a new Basys project from a starter template and installs npm packages.

If starter template argument is not provided it will be requested interactively. Starter template argument supports two formats:

1. Public GitHub repository in a form `<username>/<repo-name>` (with an optional `#branch`);
2. Local directory provided by an absolute or relative path.

#### basys dev [app-name]

This commands starts the development server (at http://localhost:8080 by default if the port is not occupied), that automatically bundles all your code and opens web app in the browser with hot module reload. The `app-name` argument is required if project consists of several apps.

By default the development server launches Basys visual app builder (at `localhost:8090` or the nearest empty port). To disable it pass `-b` argument.

#### basys build [app-name]

Generates a production bundle of the app into `<project-dir>/build/<app-name>` directory.

#### basys start [app-name]

Starts a local server to test a previously generated production bundle.

#### basys test:unit

Runs project unit tests. [Jest test files](https://facebook.github.io/jest/docs/en/using-matchers.html) are automatically detected inside `<project-dir>/tests/unit/` directory.

#### basys test:e2e [app-name]

Builds the production app bundle and launches end-to-end tests for it. [TestCafe test files](https://devexpress.github.io/testcafe/documentation/test-api/test-code-structure.html) are automatically detected inside `<project-dir>/tests/e2e/` directory.

#### basys lint

Lints the source code of the project and prints the list of linting errors. The default ESLint config created specifically for Basys projects can be found [here](https://github.com/basys/basys/tree/master/packages/eslint-config-basys). You can customize the rules in `<project-dir>/.eslintrc` file.

#### basys lint:fix

Performs code linting and automatically fixes linting errors when possible (overwriting the original source files).
