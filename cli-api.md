### CLI and API commands

Basys CLI can be installed globally using npm

```bash
npm install -g basys-cli
```
or Yarn:
```bash
yarn global add basys-cli
```

The following commands are available:

#### init

Initializes a new Basys project from a starter project and installs npm packages.

```bash
basys init [starter-project]
```

If starter project name is not provided you will be offered to chose one interactively. The command supports two types of starter project argument:

1. Public GitHub repository in a form `<username>/<repo-name>`;
2. Local directory provided by an absolute or relative path.

You can also create a new project via API (see [source code](https://github.com/basys/basys/blob/master/packages/basys-cli/utils.js)
```javascript
const {initProject} = require('basys-cli/utils');
initProject(answers, install);
```

`answers` is an object containing answers to the questions asked interactively in CLI. Its attributes are: `name` - project starter name descrbed above, `dest` - the directory path where project will be generated (must be empty or non-existent). `install` is a boolean that indicates whether npm packages should be installed (defaults to `true`). Returns a promise that is resolved once project initialization is completed.

#### dev

This commands starts the development server, that automatically bundles all your code and serves to the browser with hot module reload.
```bash
basys dev [app-name]
```
The app name is required if project contains several apps.

To start the development server via API use
```javascript
const {dev} = require('basys');
dev(projectDir, appName);
```
`projectDir` is the root directory of a Basys project, `appName` is the app name from `basys.json` file (required if project contains several apps). Returns a promise fulfilled with the app configuration object.

#### build

Generates a production bundle of the app into `build/<app-name>` directory.

```bash
basys build [app-name]
```

```javascript
const {build} = require('basys');
build(projectDir, appName);
```

`projectDir` is the root directory of a Basys project, `appName` is the app name from `basys.json` file (required if project contains several apps). Returns a promise fulfilled with the app configuration object.

#### start

Starts a local server to test the production bundle.

```bash
basys start [app-name]
```

```javascript
const {start} = require('basys');
start(projectDir, appName);
```

#### test:e2e

Builds the production app bundle and launched end-to-end tests for it. [TestCafe test files](https://devexpress.github.io/testcafe/documentation/test-api/test-code-structure.html) are automatically detected inside `tests/e2e/` directory.

```bash
basys test:e2e [app-name]
```

```javascript
const {e2eTest} = require('basys');
e2eTest(projectDir, appName);
```

#### lint

Lints the source code of the project and prints the list of linting errors. The default ESLint config created specifically for Basys projects can be found [here](https://github.com/basys/basys/tree/master/packages/eslint-config-basys). You can customize the rules in `.eslintrc` file.
```bash
basys lint
```

Some linting errors can be automatically fixed (overwriting the original source files).
```bash
basys lint:fix
```

Linting the project via API is done synchronously:
```javascript
const {lint} = require('basys');
lint(projectDir, fix);
```
`projectDir` is the root directory of a Basys project, `fix` is a boolean indicating whether linting errors should be fixed (defaults to `false`).
