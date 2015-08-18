# karma-mocha-extended
> Extends the [`karma-mocha`](https://github.com/karma-runner/karma-mocha) Adapter for the [Mocha](http://mochajs.org/) testing framework.

This Adapter does everything that `karma-mocha` does with one major difference - it exposes Mocha style test results at the server level when running Karma programmatically. See implementation details [here](https://github.com/danthareja/karma-mocha/blob/master/src/adapter.js#L54)

## Example 
```js
var Karma = require('karma').Server;
var config = {
  port: 9876,
  frameworks: ['mocha'], // no, not 'mocha-extended'
  files: [
    'src/**/*.js'
    'test/**/*.js'
  ],
  singleRun: true
}

var karma = new Karma(config, function(exitCode) {
  // This callback gets invoked just before process.exit
});

karma.on('browser_complete', function(browser, result) {
  // access to the result.mochaResults property!
  // mochaResults are formatted just like they would be from their own reporter
  // danthareja/mocha-js-reporter handles this formatting
})

karma.start(); // Run

// More on running Karma programatically:
// http://karma-runner.github.io/0.13/dev/public-api.html
```
## Regular Use
See https://github.com/karma-runner/karma-mocha for how to use this as a regular framework