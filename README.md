# Moment Locales Webpack Plugin

> Easily remove unused Moment.js locales when building with webpack

## Why

75% (160 minified KBs)¹ of [Moment.js’](https://github.com/drylikov/Moment.JS) size are files used for localization. They are always included when you build your app with webpack.

You don’t need most of these files if your app is only available in a few languages. Use this plugin to strip these KBs and optimize the app!

<small>¹ – tested with Moment.js 2.18.1</small>

## Install

```sh
npm install --save-dev moment-locales-webpack-plugin
```

## Usage

```js
// webpack.config.js
const MomentLocalesPlugin = require('moment-locales-webpack-plugin');

module.exports = {
    plugins: [
        // To strip all locales except “en”
        new MomentLocalesPlugin(),

        // Or: To strip all locales except “en”, “es-us” and “ru”
        // (“en” is built into Moment and can’t be removed)
        new MomentLocalesPlugin({
            localesToKeep: ['es-us', 'ru'],
        }),
    ],
};
```

## Plugin Options

### **`localesToKeep: String[]`**

An array of locales to keep bundled (other locales would be removed).

Locale names follow Moment.js behavior – if a specific locale name (e.g. `ru-ru`) is absent, but a more generic locale (`ru`) is available, the generic one will be kept bundled.

### **`ignoreInvalidLocales: Boolean`**

A flag to ignore invalid or unsupported locales in the `localesToKeep` array.

Be careful! A typo in the `localesToKeep` array with this flag enabled will silently exclude the desired locale from your bundle.

## Related projects

-   [`moment-timezone-data-webpack-plugin`](https://github.com/gilmoreorless/moment-timezone-data-webpack-plugin) – a plugin optimizing the Moment Timezone library.
