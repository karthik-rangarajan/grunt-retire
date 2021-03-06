# grunt-retire

Grunt task for [retire.js](https://github.com/bekk/retire.js). Scanner detecting the use of JavaScript libraries with known vulnerabilities.



## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-retire --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-retire');
```




## Retire task
_Run this task with the `grunt retire` command._

This task primarily delegates to [Retire][], so please consider the [Retire documentation][] as required reading for advanced configuration.

[Retire]: https://github.com/bekk/retire.js
[Retire documentation]: https://github.com/bekk/retire.js

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

### Available options
Example configuration below shows default option values and the correct syntax to use if you want to override any of them. If no options are provided, the default values as shown below are used.

```js
    retire: {
      js: ['app/src/*.js'], /** Which js-files to scan. **/
      node: ['node'], /** Which node directories to scan (containing package.json). **/
      options: {
         proxy: 'http://something.something:8080',
         verbose: true,
         packageOnly: true, /* Note! package:false is not yet implemented in grunt plugin, only in node version of retire. */
         jsRepository: 'https://raw.github.com/bekk/retire.js/master/repository/jsrepository.json',
         nodeRepository: 'https://raw.github.com/bekk/retire.js/master/repository/npmrepository.json',
         ignore: 'documents,java'
      }
    }
```

`proxy: url`, proxy (supports basic auth).

`verbose: true/false`, default is `true`. More verbose output (grunt -d may also be used for even more debug output).

`packageOnly: true/false`, default is `true`. Only scan only dependencies in package.json, skip dependencies to dependencies.

`jsRepository: String`, default is `https://raw.github.com/bekk/retire.js/master/repository/jsrepository.json`. JSON file which specifies where to retrieve Javascript vulnerability database.

`nodeRepository: String`, default is `https://raw.github.com/bekk/retire.js/master/repository/npmrepository.json`. JSON file which specifies where to retrieve Node vulnerability database.

`ignore: String`, default is empty. Paths to ignore when scanning for JavaScript files.


## Scan javascript files only
```js
    retire: {
      js: ['app/src/*'], /** Scan js-files in app/src/ directory and subdirectories. **/
      options: {
      }
    }
```

Running ```grunt retire``` will scan files in app/src/ for vulnerable libraries. If file sources for both node and js are specified, scanning js only is possible using `retire:js`

## Scan node dependencies example
```js
    retire: {
      node: ['module/'], /** Scan node project in directory module/. Should be ['.'] for normal projects **/
      options: {
      }
    }
```
Running ```grunt retire``` will scan all dependencies specified under `dependencies` in `package.json` for vulnerable libraries. If file sources for both node and js are specified, scanning node only is possible using `retire:node`


## Example output with one vulnerability found in jquery-1.6.js:

```
➜  grunt-retire git:(master) ✗ grunt retire
Running "retire:jsPath" (retire) task
JS repository loaded from: https://raw.github.com/bekk/retire.js/master/repository/jsrepository.json
>> test-files/jquery-1.6.js
>> ↳ jquery 1.6 has known vulnerabilities: http://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2011-4969
Node repository loaded from: https://raw.github.com/bekk/retire.js/master/repository/npmrepository.json
```



## Example output when no vulnerabilities is found
```
➜  grunt-retire git:(master) ✗ grunt retire
Running "retire:jsPath" (retire) task
JS repository loaded from: https://raw.github.com/bekk/retire.js/master/repository/jsrepository.json
Node repository loaded from: https://raw.github.com/bekk/retire.js/master/repository/npmrepository.json
No vulnerabilities found.

Done, without errors.
```


## Release History

 * 2013-11-12   v0.1.15  Upgrading dependencies. Proxy support
 * 2013-10-30   v0.1.12  Upgrade to retire v0.1.12. js and node defined as targets.
 * 2013-10-30   v0.1.0   First version.
