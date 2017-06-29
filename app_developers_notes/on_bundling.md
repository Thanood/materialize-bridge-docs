# Bundling the Materialize bridge
<br>
<br>
The general process of bundling an Aurelia app is explained in [the Aurelia documentation on bundlung](http://aurelia.io/hub.html#/doc/article/aurelia/framework/latest/bundling-jspm).
It may seem like for a complete bundle configuration it would be sufficient to just add the bridge to a bundle:

```json
"dist/aurelia-bundle": {
  "includes": [
    "aurelia-framework",
    ...
    "aurelia-materialize-bridge"
  ]
}
```

A problem with this approach is that the bridge does not export its components directly and thus these components
are not directly visible to Aurelia bundler.

Instead, the bridge's `index.js` file uses `config-builder` to fill Aurelia's
`globalResources` (just like [Aurelia features are configured](http://aurelia.io/docs.html#/aurelia/framework/1.0.0-beta.1.2.2/doc/article/app-configuration-and-startup/6)).

A sufficient bundle configuration needs to include the sub-directories of the
bridge as well as its html and css files. Such a configuration would look like this:

```json
"dist/aurelia-bundle": {
  "includes": [
    "aurelia-framework",
    ...
    "aurelia-materialize-bridge",
    "aurelia-materialize-bridge/**/*.js",
    "aurelia-materialize-bridge/**/*.html!text",
    "aurelia-materialize-bridge/**/*.css!text"
  ]
}
```

An even better solution is to only include the bridge (without its own dependencies)
in a separate bundle.
 
```json
"dist/aurelia-bundle": {
  "includes": [
	"[aurelia-materialize-bridge]",
	"[aurelia-materialize-bridge/**/*.js]",
	"aurelia-materialize-bridge/**/*.css!text",
	"aurelia-materialize-bridge/**/*.html!text",
	"materialize-css"
  ]
}
```

[Have a look here](https://github.com/aurelia-ui-toolkits/demo-materialize/blob/master/build/bundles.js)
for a complete bundle using three bundles for this catalog app, the Aurelia framework
and used plugins (including Materialize bridge).


### A note on jQuery

Since *jquery* is a dependency of *materialize-css*, you should add it explicitly to the bundle or make sure to import it first.

```javascript
import 'jquery';
import 'materialize-css';
```

### Troubleshooting

If you get the error

```
Uncaught (in promise) Error: (SystemJS) Cannot set property 'Picker' of undefined
	TypeError: Cannot set property 'Picker' of undefined
```
This is probably a bug in SystemJS, where ``use strict`` at the beginning of the bundle breaks the import.

The following solutions exists:

- Just remove ``"use strict";`` from the bundle
- Don't add *materialize-css* to the bundle
- This issue is probably gone with SystemJS 0.20/JSPM 0.17

Reference: https://github.com/aurelia-ui-toolkits/aurelia-materialize-bridge/issues/444