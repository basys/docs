### Application code

#### Front-end app

Basys automatically detects and imports `.vue` files inside `<project-dir>/src` directory. Vue file reprensents a page or UI component depending on whether a page path is provided. Besides a few Basys-specific options Vue components are implemented as usual based on the latest versions of [Vue](https://vuejs.org/v2/api) and [Vue Router](https://router.vuejs.org/api).

JavaScript code in `.vue` and `.js` files fully supports ECMAScript 2017 syntax. In order for Basys to automatically register Vue component the `<script>` section must contain `export default { ... }` and specify the `name` option. Other Basys-specific configuration is optional.

```javascript
export default {
  name: 'component-name', // Required unique component name
  info: {
    // Path passed to Vue Router (for pages only)
    path: '/page-path',
    // A list of apps using this component (optional).
    // By default component is included in all project apps.
    apps: ['basys-app-name'],
  },
  // Passed to vue-meta to customize tags inside <head> (optional).
  // See https://github.com/declandewet/vue-meta#recognized-metainfo-properties .
  head: {
    title: 'Page title',
  },
  // Other component configuration goes here...
};
```

A global `basys = {env, appName, entryType}` is available in all front-end code. Module import supports two shortcuts: `@` for `<project-dir>/assets` and `~` for `<project-dir>/src`.

If you need to include the contents of a file into the front-end js bundle use `require('raw-loader!./file.txt')`. It will be replaced with the file contents by webpack during the compilation.

<a name="front-end-style"></a>

`<style>` section in `.vue` files doesn't support `lang` attribute. Instead, the styles are processed by [PostCSS](https://postcss.org) with the following plugins (see [PostCSS config](https://github.com/basys/basys/blob/master/packages/basys/lib/webpack/postcss.config.js) for details):
* [postcss-import](https://github.com/postcss/postcss-import) for inlining `@import` rules content. Import path supports the `@` shortcut for `<project-dir>/assets` directory and `~` for `<project-dir>/src`.
* [postcss-simple-vars](https://github.com/postcss/postcss-simple-vars) adds support for Sass-like variables (`appName` and `env` are built-in)
* [postcss-conditionals](https://github.com/andyjansson/postcss-conditionals) supports `@if` statements
* [postcss-nested](https://github.com/postcss/postcss-nested) for unwrapping nested rules

<a name="front-end-entry"></a>

Sometimes you may need to customize Vue configuration, install a Vue plugin or import an external library. Front-end entry point should be used then - it's a JavaScript file that will be imported before Vue is initialized. In `basys.json` you will need to add `entry` option - entry point file path relative to `<project-dir>/src`. You will have access to `basys = {env, appName}` and `Vue` objects.

To customize [`render()` method](https://vuejs.org/v2/api/#render) of the root Vue instance the entry point module should export an object with `render()` method. To dig into the inner working of Basys front-end entry point look at the [webpack entry point](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/frontend.js).

#### Backend app

Basys comes with support for a [Express](https://expressjs.com) backend app. To activate the backend app you need to add `backendEntry` option to `basys.json` - the path to entry point JavaScript file relative to `<project-dir>/src`. The backend code supports ECMAScript 2017 and runs inside Node.js.

Basys handles a lot of [boilerplate code](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/backend.js) required to run Express app, so that you can focus on the core functionality. A global `basys` object with the following attributes is available:

* `app` - Express app instance. For more details see [Express documentation](http://expressjs.com/en/4x/api.html#app);
* `server` - [http.Server](https://nodejs.org/api/http.html#http_class_http_server) instance;
* `config` - Basys [configuration object](configuration.md) for the current app;
* `entryType` - if some of your code can be shared between front-end and backend use it to identify the runtime environment (`'backend'` or `'frontend'`);
* `appName` - Basys app name defined in `basys.json`, useful when your project contains several apps;
* `env` - environment in which application is currently running (`'dev'`, `'test'` or `'prod'`);
* `setPageHandler` - method that allows to implement custom page rendering (see below).

For example, to add a new route use
```javascript
basys.app.get('/api', (req, res) => {
  res.json({value: 42});
});
```

Often you will need to customize the page rendering on the backend, say to import an external spreadsheet. To override the [default HTML page](https://github.com/basys/basys/blob/master/packages/basys/lib/templates/index.html) save your custom HTML into `<project-dir>/index.html`. This file is a [Nunjucks](https://mozilla.github.io/nunjucks) template that can access `basys = {appName, env}` variable. In some cases you will need to render this template using request-specific data, such as information about authenticated user or a configuration value. You can pass custom template variables by overriding the page rendering method `setPageHandler` as follows
```javascript
basys.setPageHandler((render, request, response) => {
  // `value` variable is now available in index.html template
  render({value: 'value from backend'});
});
```
Please note that the rendering method should not use page-specific information (such as request url), since the front-end app is a single page application.

#### Static assets

Static files such as images and styles are stored in `<project-dir>/assets` directory and bundled by webpack. To improve the load times image, video and font files smaller than 10 kB are automatically inlined.

Basys supports `.css`, `.scss` and `.less` styles. In order to include a style into the app add its path (relative to `<project-dir>/assets`) to the `styles` option in `basys.json`. `.css` files are processed by PostCSS as described [above](#front-end-style).
