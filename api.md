### API

```javascript
const basys = require('basys');
```

#### basys.initProject( options [, install = true] )

Initializes a new Basys project from a starter template and installs npm packages.

`options` is an object with the following attributes:
* `name` - starter template name, that supports two formats:
  1. Public GitHub repository in a form `<username>/<repo-name>` (with an optional `#branch`);
  2. Local directory provided by an absolute or relative path.
* `dest` - the directory path where project will be generated (must be empty or non-existent).
* `vscode` - boolean indicating whether Visual Studio Code workspace settings should be generated.

If some of these options are missing an interactive CLI will be launched in the terminal.

`install` is a boolean that indicates whether npm packages should be installed.

Returns a promise that is resolved once project initialization is complete.

#### basys.dev( projectDir [, appName [, appBuilder = true] ])

This command starts the development server, that automatically bundles all your code and opens web app in the browser with hot module reload. By default the server starts at `localhost:8080` (can be customized in `basys.json` [configuration file](configuration.md) using `host` and `port` options). If the port is occupied it will search for the nearest empty port.

`projectDir` is a Basys project directory, `appName` is an app name defined in `basys.json` (required if project consists of several apps).

By default the development server launches Basys visual app builder (at `localhost:8090` or the nearest empty port). To disable it pass `appBuilder = false`.

Returns a promise fulfilled with the app configuration object.

#### basys.build( projectDir [, appName] )

Generates a production bundle of the app into `<project-dir>/build/<app-name>` directory. Returns a promise fulfilled with the app configuration object.

#### basys.start( projectDir [, appName] )

Starts a local server to test a previously generated production bundle. Returns the app configuration object.

#### basys.unitTest( projectDir )

Runs project unit tests. [Jest test files](https://facebook.github.io/jest/docs/en/using-matchers.html) are automatically detected inside `<project-dir>/tests/unit/` directory.

#### basys.e2eTest( projectDir [, appName [, options] ] )

Builds the production app bundle and launches end-to-end tests for it. [TestCafe test files](https://devexpress.github.io/testcafe/documentation/test-api/test-code-structure.html) are automatically detected inside `<project-dir>/tests/e2e/` directory.

`options` is an optional TestCafe test runner [configuration object](http://devexpress.github.io/testcafe/documentation/using-testcafe/programming-interface/runner.html#run).

#### basys.lint( projectDir [, fix] )

Lints the source code of the project and prints the list of linting errors. The default ESLint config created specifically for Basys projects can be found [here](https://github.com/basys/basys/tree/master/packages/eslint-config-basys). You can customize the rules in `<project-dir>/.eslintrc` file.

If `fix = true` some linting errors can be automatically fixed (overwriting the original source files).
