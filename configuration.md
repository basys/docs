### Configuration

Basys project configuration is stored in `basys.json` file. It uses [JSON5](https://json5.org) format (an unofficial extension of JSON) that supports comments, optional quotes and trailing commas. Most these configuration options are optional. It has the following structure:

<!-- BUG: explain that project may contain several apps, sharing code for cross-platform apps + use cases -->
<!-- BUG: cssSourceMap, jsSourceMap, dev/test/prod - to override for specific environment -->
<!-- BUG: mention that names of custom config options shouldn't overlap with built-in -->
```javascript
{
  "apps": {
    "your-app-name": {
      "type": "web",
      // App configuration options go here...
    },
  },
}
```

| Option | Default  | Description |
| ------ | -------- | ----------- |
| type   | Required | App type. Available options: `"web"`, `"mobile"`, `"desktop"`. |
| entry  | `null`   | Optional entry for UI Vue application (relative to src/ directory), e.g. `"frontend.js"`. The full front-end code can be found [here](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/frontend.js). |
| backendEntry | `null` | Optional entry to customize Express application (relative to src/ directory), e.g. `"backend.js"`. The full backend code can be found [here](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/backend.js). For web apps only. |
| styles | `[]`    | A list of paths to stylesheet files, that are preprocessed, bundled and loaded on all pages. CSS, LESS and SASS files are supported. Two types of paths can be provided: 1) Project files using a path relative to assets/ directory (e.g. `"theme.scss"`); 2) Files from NPM modules using a path relative to project's node_modules directory (e.g. `"bootstrap/dist/css/bootstrap.min.css"`). |
| overrides | `{}` | Allows to override javascript modules with custom code. Useful when a 3rd-party library bundled into the frontend code imports a large module, that is not actually needed. The key is a [minimatch](https://github.com/isaacs/minimatch)-like path (e.g. `"**/node_modules/acorn-jsx/inject.js"`) and the value is a path to override module relative to the project root directory (e.g. `"src/acorn-jsx-inject.js"`). |
| favicon | `null` | Optional path to favicon file relative to the project root. |
| browsers | `["> 0.5%", "last 2 versions", "Firefox ESR", "not dead"]` | A list of browsers that will be supported by the web app. This option is used when bundling JavaScript and CSS and replaces all unsupported features with polyfills. It uses the [browserlist format](https://github.com/ai/browserslist#queries). If you only support newer browsers this option allows to reduce the bundle size. For web apps only. |
| nodeVersion | `8.9` | A minimum version of Node.js supported by the backend code. For web and desktop apps only. |
| host | `"localhost"` | Host used for serving web app and dev server. |
| port | `8080` | Port used for serving web app. If this port is occupied an empty port will be automatically detected and used. |
| backendPort | `3000` | Port used by dev server for web app backend. If this port is occupied an empty port will be automatically detected and used. |
| testBrowsers | `[]` | A list of browsers that are used for end-to-end testing. Available options: `"chromium"`, `"chrome"`, `"chrome:headless"`, `"chrome-canary"`, `"ie"`, `"edge"`, `"firefox"`, `"firefox:headless"`, `"opera"`, `"safari"`. |
| custom | `{}` | A JSON object that contains custom app-specific configuration, that can be accessed in the backend code using the global `basys.config` object. |
