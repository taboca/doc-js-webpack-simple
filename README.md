# Webpack via command line 

* https://leanpub.com/doc-js
* If you want to contribute to the book or join me as a coauthor pool, please get in contact mgalli at mgalli dot com subject "doc-js book"

# Bundlers and HTML app start points

* npm install webpack --save-dev
* npm install webpack-cli -save-dev

Create a directory for your unbundled sources, and another for the distribution HTML that will attempt to load a bundle.js (generated output of webpack):

* ./src/index.js
* ./public/dist/ (target will will receive the bundle.js)
* ./public/page.html (HTML file that will load the ./public/dist/bundle.js)

Let's write a JS file with almost nothing in it:

(./src/index.js)
```
alert(1);
```

Now setup your config to help web pack to load your js file and generate the bundle.

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'public', 'dist'),
    filename: 'bundle.js'
  }
};
```

Le't run:

```
./node_modules/webpack-cli/bin/cli.js --config ./webpack.config.js
```

Now make a simple page.html:

```
<!doctype html>
<html>
  <head>
    ...
  </head>
  <body>
    ...
    <script src="dist/bundle.js"></script>
  </body>
</html>
```

And load it from the file system in your browser. Expect the simple alert box.

Now let's evolve your webpack-based example so your initial JS executes a code from a module:

(./src/index.js)
```
import moduleTest from './moduleTest'
moduleTest();
```

And make your 'moduleTest.js':

```
export default function something() {

  alert(1)

}
```

Again, execute the webpack to generate your bundle:

```
./node_modules/webpack-cli/bin/cli.js --config ./webpack.config.js
```

And expect, again an alert box.


## References

* [Webpack @ npm](https://www.npmjs.com/package/webpack)

* [Getting Started with Webpack](https://webpack.js.org/guides/getting-started/)

* [Configuration of Webpack](https://webpack.js.org/configuration/)
