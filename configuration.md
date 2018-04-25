### Configuration

Basys project consists of one or more apps, which may have shared assets or code. The configuration file `basys.json` uses [JSON5](https://json5.org) format (an unofficial extension of JSON) that supports comments, optional quotes and trailing commas. It has the following structure:

```javascript
{
  "apps": {
    "your-app-name": {
      "type": "web",
      // Optional app configuration options go here...
    },
  },
}
```

| Option | Default  | Description |
| ------ | -------- | ----------- |
| type   | Required | App type. Available options: `"web"` (`"mobile"` and `"desktop"` coming soon). |
| entry  | `null`   | Optional entry for UI Vue application (relative to src/ directory), e.g. `"frontend.js"`. The full front-end code can be found [here](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/frontend.js). |
| backendEntry | `null` | Optional entry to customize Express application (relative to src/ directory), e.g. `"backend.js"`. The full backend code can be found [here](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/backend.js). For web apps only. |
| styles | `[]`    | A list of paths to stylesheet files, that are preprocessed, bundled and loaded on all pages. CSS, LESS and SASS files are supported. Two types of paths can be provided: 1) Project files using a path relative to assets/ directory (e.g. `"theme.scss"`); 2) Files from NPM modules using a path relative to project's node_modules directory (e.g. `"bootstrap/dist/css/bootstrap.min.css"`). |
| overrides | `{}` | Allows to override javascript modules with custom code. Useful when a 3rd-party library bundled into the frontend code imports a large module, that is not actually needed. The key is a [minimatch](https://github.com/isaacs/minimatch)-like path (e.g. `"**/node_modules/acorn-jsx/inject.js"`) and the value is a path to override module relative to the project root directory (e.g. `"src/acorn-jsx-inject.js"`). |
| caseSensitive | `false` | Defines whether to use case sensitive route matching. |
| favicon | `null` | Optional path to favicon file relative to the project root. |
| browsers | `["> 0.5%", "last 2 versions", "Firefox ESR", "not dead"]` | A list of browsers that will be supported by the web app. This option is used when bundling JavaScript and CSS and replaces all unsupported features with polyfills. It uses the [browserlist format](https://github.com/ai/browserslist#queries). If you only support newer browsers this option allows to reduce the bundle size. For web apps only. |
| cssSourceMap | `env==='test'` | Defines whether CSS source maps should be generated (only in end-to-end tests by default). |
| jsSourceMap | `env==='test'` | Defines whether JavaScript source maps should be generated (only in end-to-end tests by default). |
| nodeVersion | `8.9` | A minimum version of Node.js supported by the backend code. For web and desktop apps only. |
| host | `"localhost"` | Host used for serving web app and dev server. |
| port | `8080` | Port used for serving web app. If this port is occupied an empty port will be automatically detected and used. |
| backendPort | `3000` | Port used by dev server for web app backend. If this port is occupied an empty port will be automatically detected and used. |
| testBrowsers | `[]` | A list of browsers that are used for end-to-end testing. Available options: `"chromium"`, `"chrome"`, `"chrome:headless"`, `"chrome-canary"`, `"ie"`, `"edge"`, `"firefox"`, `"firefox:headless"`, `"opera"`, `"safari"`. |
| custom | `{}` | A JSON object that contains custom app-specific configuration, that can be accessed in the backend code using the global `basys.config` object. Attribute names must not overlap with any built-in option names. |
| dev | `{}` | Allows to override option values when running the dev server. |
| test | `{}` | Allows to override option values when running end-to-end tests. |
| prod | `{}` | Allows to override option values when building the app for production. |
