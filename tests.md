### Tests

#### Unit tests

Under the hood Basys uses [Jest](https://facebook.github.io/jest) to run unit tests. It comes with a [default configuration](https://github.com/basys/basys/blob/master/packages/basys/lib/webpack/jest-config.js), but you can provide custom Jest configuration by creating `jest.config.js` file in the project root directory.

Jest automatically finds `*.test.js` and `*.spec.js` test files inside `tests/unit/` directory. All features included in ECMAScript 2017 are supported with the help of [babel-preset-env](https://babeljs.io/docs/plugins/preset-env/).

Here is a sample test to get you started:
```javascript
test('Sample test', () => {
  expect(1 + 2).toBe(3);
});
```
Save it into `tests/unit/index.test.js` and run `basys test:unit`. To learn more about writing tests follow [Jest documentation](https://facebook.github.io/jest/docs/en/using-matchers.html).

If you are using [Basys extension for VS Code](https://marketplace.visualstudio.com/items?itemName=basys.vscode-basys) you will get a convenient way to run and debug tests right from the code editor.

![Jest extension demo](https://raw.githubusercontent.com/jest-community/vscode-jest/master/images/vscode-jest.gif)

#### End-to-end tests

End-to-end tests in Basys are implemented using [TestCafe](https://devexpress.github.io/testcafe). Unlike Selenium there is no need to install browser-specific drivers - TestCafe injects the driver script into the tested page and emulates user actions. That results in a seamless support of [all popular browsers](https://devexpress.github.io/testcafe/documentation/using-testcafe/common-concepts/browsers/browser-support.html) as well as Electron-based desktop apps.

TestCafe automatically finds test files amoung `tests/e2e/*.js` (only files with at least one fixture and a test are executed). Test files support ECMAScript 2017 syntax and have access to a global object
```javascript
basys = {
  env: 'test',
  appName,
  config: {host, port, backendPort, ...customOptions},
}
```

Here is a sample test which checks that web app home page contains a `&lt;div&gt;Hello world!&lt;/div&gt;` element:
```javascript
import {Selector} from 'testcafe';

fixture('Home page').page(`http://${basys.config.host}:${basys.config.port}`);

test('Sample test', async t => {
  await t
    .expect(Selector('div').exists).ok()
    .expect(Selector('div').innerText).contains('Hello world!');
});
```

Use `basys test:e2e [app-name]` command to run the tests (provide app name if your project contains several apps). To learn more about writing end-to-end tests head to [TestCafe documentation](http://devexpress.github.io/testcafe/documentation/test-api/test-code-structure.html).
