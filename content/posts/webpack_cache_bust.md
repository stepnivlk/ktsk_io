+++
title = "Hey Webpack, can you bust my cache?"
date = 2017-07-02

[taxonomies]
categories = ["programming"]
+++

Most JavaScript developers are familiar with this problem. You have a bug in your system; you fix it, ship it… and your error monitoring still spams you with the problem, which was apparently fixed. How come? Your responses have cache headers set, and the client's browser caches static assets. But web development is very dynamic nowadays; we deploy multiple times per day. So how can we continue with aggressive deployment and still cache static assets?

You can use query string to version your assets:

```html
<script src=”/bundles/app.bundle.js?v=23” type=”text/javascript”></script>
```

Unfortunately, some CDNs and proxies don't cache assets with query strings at all. Moreover, versioning here is a very manual process, thus doomed to be forgotten.

What else? Of course, you can include your version in a path or in a file name:

```html
<script src=”/bundles/v23/app.bundle.js” type=”text/javascript”></script>
```

...

```html
<script src=”/bundles/app.bundle.v23.js” type=”text/javascript”></script>
```

Better and valid for CDNs and proxies. But still too manual, we need something automatic and more sophisticated. So whenever someone builds an asset, the version will be automatically busted. Only then will the feature be handy (even managers will be able to invalidate a cache).

Let's try to automate it! Since the title of this post starts with Hey Webpack, we will focus on Webpack based solutions. We will build a very tiny example React application because React is cool. But it doesn't matter; you can use this solution with whatever library (or framework) you want as long as it will be built using Webpack.

We start with initializing the project and adding some libraries:

```bash
➜ mkdir cache-busters && cd cache-busters

➜ cache-busters yarn init

➜ cache-busters yarn add react react-dom

➜ cache-busters yarn add --dev webpack webpack-dev-server babel-core babel-loader babel-preset-react css-loader
```

Now let's create some basic directory structure:

```bash
➜ cache-busters mkdir config

➜ cache-busters mkdir config/webpack

➜ cache-busters mkdir src

➜ cache-busters touch src/index.jsx

➜ cache-busters mkdir src

➜ cache-busters mkdir src/components

➜ cache-busters mkdir src/assets

➜ cache-busters touch src/assets/style.css

➜ cache-busters mkdir public

➜ cache-busters touch public/index.html

➜ cache-busters mkdir public/bundles

➜ cache-busters touch .babelrc
```

Add Babel preset to .babelrc:

```js
{

  "presets": ["react"]

}
```

Ok, time to get our hands dirty; now we start to configure the Webpack. We want to have one basic configuration file with just an entry point definition and some rules. Then we'll add two separate configurations for development and production environments, which would enhance basic configuration. Using this setup, we can define plugins for each environment separately:

```bash
➜ cache-busters touch config/webpack/config.js

➜ cache-busters touch config/webpack/config.production.js

➜ cache-busters touch config/webpack/config.development.js
```

```js
// config/webpack/config.js

const path = require('path')
const ExtractTextPlugin = require('extract-text-webpack-plugin')

module.exports = {
  entry: {
    app: [
      path.resolve(__dirname, '../../src/index.jsx'),
    ],
  },
  module: {
    rules: [
      {
        test: /.jsx?$/,
        use: ['babel-loader'],
        exclude: /node_modules/,
      },
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          use: 'css-loader',
        }),
      },
    ],
  },
  resolve: {
    modules: [
      'node_modules',
      path.resolve(__dirname, '../../src'),
    ],
    extensions: ['.js', '.jsx'],
    alias: {
      react: path.resolve(__dirname, '../../node_modules', 'react'),
    },
  },
  plugins: [],
}
```

Webpack now knows our entry point and is instructed to use babel-loader for js/jsx and css-loader for CSS files.

Now it's time to add basic development configuration, so we'll be able to actually build our application and run webpack-dev-server:

```js
// config/webpack.development.js

const webpack = require('webpack')
const config = require('./config')

config.output = {
  path: path.resolve(__dirname, '../../public/bundles'),
  filename: '[name].bundle.js',
  chunkFilename: "[name].js",
  publicPath: '/bundles/',
}

module.exports = config
```

Here we told Webpack where it should store output files and defined file names.

We're almost ready for our first development build! We need to just add index.html file, React component, and some basic styling:


```html
// public/index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Cache Busters</title>
    <link rel="stylesheet" href="/bundles/app.bundle.css">
  </head>
  <body>
    <div id="app"></div>
    <script src="/bundles/app.bundle.js" type="text/javascript"></script>
  </body>
</html>
```

```js
// src/index.jsx

import React from 'react'
import { render } from 'react-dom'

const CacheBusters = () =>
  <div>Stays Puft, Even When Toasted</div>

render(
  <CacheBusters />,
  document.getElementById('app'),
)
```

```css
// src/assets/style.css

body {
  background-color: purple;
}
```

And finally, we can add the start script to package.json:

```js
{

  // …

  "scripts": {

    "start": "webpack-dev-server — config config/webpack/config.development.js — content-base public/",

  },

  // …

}
```

Now lets try to build & start webpack-dev-server:

```bash
➜ cache-busters yarn start

yarn start v0.22.0

$ webpack-dev-server — config config/webpack/config.development.js — content-base public/ — history-api-fallback

...

Version: webpack 3.0.0

Time: 1681ms

Asset Size Chunks Chunk Names

app.bundle.js 1.06 MB 0 [emitted] [big] app

app.bundle.css  40 bytes       0  [emitted] app

...

+ 252 hidden modules

webpack: Compiled successfully.
```

Nice 1MB hello world, our setup works, we can check webpack-dev-server running at a given URL: `http://localhost:8080/`.

Time to move on to production configuration!

Let's repeat our goal once more. Upon each production build, we want our static assets to contain a hash (which would be different than the previous one only if the code was changed) and our index.html to be dynamically generated with correct assets names (containing a hash), e.g.:

```html
<script src=”/bundles/app.bundle.9f61f58dd1cc3bb82182.js” type=”text/javascript”></script>
```

Adding a hash is easy, Webpack gives us two options:

**[hash]** — calculated for build and **[chunkhash]** — calculated for entry file. For our use case, chunkhash will be a better option. Since we can selectively bust only, e.g., *app.bundle.js* and no *app.bundle.css* if we changed code just in the javascript part of our application:


```js
// config/webpack/config.production.js

const ExtractTextPlugin = require('extract-text-webpack-plugin')
const path = require('path')
const config = require('./config')

config.plugins.push(
  new ExtractTextPlugin({
    filename: 'app.bundle.[chunkhash].css',
    allChunks: true
  })
)

config.output = {
  path: path.resolve(__dirname, '../../public/bundles'),
  filename: '[name].bundle.[chunkhash].js',
  chunkFilename: "[name].[chunkhash].js",
  publicPath: '/bundles/',
}

module.exports = config
```

Let's add a build option to our package.json:

```js
{

  ...

  "scripts": {

    ...

    "build": "webpack --bail -p --config config/webpack/config.production.js",

    ...

  },

  ...

}
```

And trigger a build:

```bash
➜ cache-busters yarn build

yarn build v0.22.0

$ webpack — bail -p — config config/webpack/config.production.js

Hash: 01788dcc6a43c1f47e5c

Version: webpack 3.0.0

Time: 1786ms

Asset Size Chunks Chunk Names

app.bundle.9f61f58dd1cc3bb82182.js 688 kB 0 [emitted] [big] app

app.bundle.9f61f58dd1cc3bb82182.css 29 bytes 0 [emitted] app
```

We are getting there! Now our bundles have unique hashes. But we have a new problem now; our index.html contains old links to */bundles/app.bundle.js* and */bundles/app.bundle.css*.

We will use [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) to generate our *index.html* on demand from a template. You can use *html-webpack-plugin* with various templating engines, so it should cover most of the use cases.

```bash
➜ cache-busters yarn add --dev html-webpack-plugin

➜ cache-busters mv public/index.html ./src/assets/index.template.html
```

Remove bundle links from index.template.html:

```html
// src/assets/index.template.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Cache Busters</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

Add *html-webpack-plugin* to Webpack's *config.production.js*:

```js
const path = require('path')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const config = require('./config')

config.output = {
  path: path.resolve(__dirname, '../../public/bundles'),
  filename: '[name].bundle.[chunkhash].js',
  chunkFilename: "[name].[chunkhash].js",
  publicPath: '/bundles/',
}

config.plugins.push(
  new ExtractTextPlugin({
    filename: 'app.bundle.[chunkhash].css',
    allChunks: true
  }),
  new HtmlWebpackPlugin({
    filename: '../../public/index.html',
    template: 'src/assets/index.template.html'
  })
)

module.exports = config
```

And build:

```bash
➜ cache-busters yarn build

yarn build v0.22.0

...

Asset Size Chunks Chunk Names

app.bundle.9f61f58dd1cc3bb82182.js 688 kB 0 [emitted] [big] app

app.bundle.9f61f58dd1cc3bb82182.css 29 bytes 0 [emitted] app

public/index.html 462 bytes [emitted]

...

➜ cache-busters cat public/index.html

<!DOCTYPE html>

<html lang=”en”>

  <head>

    ...

    <link href="/bundles/app.bundle.9f61f58dd1cc3bb82182.css" rel=" stylesheet">

  </head>

  <body>

    <div id=”app”></div>

    <script type=”text/javascript” src=”/bundles/app.bundle.9f61f58dd1cc3bb82182.js”></script>

  </body>

</html>
```

Bingo! Our *index.html* now contains a dynamic chunk hash for both asset files.

It's a good idea to add those folders with dynamically generated files to *.gitignore* so that no one will commit it to git.

Now we have a new problem; our development build is broken. There's no *index.html* with our entry point anymore, and we don't want to use chunk hash during development since it's slower. One way to solve this issue would be to create a second public folder for development only with *index.html* referencing to static app.bundle.js/css assets, but it means we'd have to keep two versions of *index.html* with the same content.

But what if we'd use html-webpack-plugin to generate index.html from the template with chunk hash-free assets? I'd work except for one small issue — using webpack-dev-server, our *index.html* is not being written to a hard drive. What now? Of course, there is a webpack plugin to solve it: [html-webpack-harddisk-plugin](https://github.com/jantimon/html-webpack-harddisk-plugin)!

Now we can add it to our development config:

```bash
➜ cache-busters yarn add --dev html-webpack-harddisk-plugin
```

```js
// config.development.js

const path = require('path')
const ExtractTextPlugin = require('extract-text-webpack-plugin')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const HtmlWebpackHarddiskPlugin = require('html-webpack-harddisk-plugin')
const config = require('./config')

config.output = {
  path: path.resolve(__dirname, '../../public/bundles'),
  filename: '[name].bundle.js',
  chunkFilename: "[name].js",
  publicPath: '/bundles/',
}

config.plugins.push(
  new ExtractTextPlugin({
    filename: 'app.bundle.css',
    allChunks: true
  }),
  new HtmlWebpackPlugin({
    filename: '../../public/index.html',
    template: 'src/assets/index.template.html',
    alwaysWriteToDisk: true, // this option was added by html-webpack-harddisk-plugin
  }),
  new HtmlWebpackHarddiskPlugin()
)

module.exports = config
```

Try to run webpack-dev-server:

```bash
➜ cache-busters yarn start

...

Asset Size Chunks Chunk Names

app.bundle.js 1.06 MB 0 [emitted] [big] app

app.bundle.css 37 bytes 0 [emitted] app

../../public/index.html 420 bytes [emitted]
```

That's it! Bundles don't have a hash, and index.html is being emitted.

Now we have working cache-busting as well as a solid Webpack setup ready to be extended.

I hope you enjoyed this tutorial & see you next time.
