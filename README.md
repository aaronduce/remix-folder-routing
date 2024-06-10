# Remix Folder Routing (adapted from V1 Route Convention)

Original source: [@remix-run/v1-route-convention](https://www.npmjs.com/package/@remix-run/v1-route-convention)

v1-route-convention is used to return to classic style nested folder routing for Remix v2 - a feature that was removed in the transition from Remix v1 to Remix v2 as they moved to flat file routing - which is unfeasible and unappropriate for monolith applications. The original package, though, comes with significant performance issues to `remix dev`, and with vite being an unfeasible option in this particular situation, optimisations must be introduced by other means. 

Some functions have been changed to asynchronous functions, and thats all I have changed for now.

* Tests have not yet been adapted from vitest to jest.

---

Enables the [v1 route file convention](https://remix.run/docs/en/v1/file-conventions/routes-files) in Remix v2.

```sh
npm install --save remix-folder-routing
```

```js
// remix.config.js
const { createRoutesFromFolders } = require("remix-folder-routing");

/** @type {import('@remix-run/dev').AppConfig} */
module.exports = {
  // Tell Remix to ignore everything in the routes directory.
  // We'll let `createRoutesFromFolders` take care of that.
  ignoredRouteFiles: ["**/*"],
  routes: (defineRoutes) => {
    // `createRoutesFromFolders` will create routes for all files in the
    // routes directory using the same default conventions as Remix v1.
    return createRoutesFromFolders(defineRoutes, {
      // If you're already using `ignoredRouteFiles` in your Remix config,
      // you can move them to `ignoredFilePatterns` in the plugin's options.
      ignoredFilePatterns: ["**/.*", "**/*.css"],
    });
  },
};
```
