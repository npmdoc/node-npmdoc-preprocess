# api documentation for  [preprocess (v3.1.0)](https://github.com/jsoverson/preprocess)  [![npm package](https://img.shields.io/npm/v/npmdoc-preprocess.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-preprocess) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-preprocess.svg)](https://travis-ci.org/npmdoc/node-npmdoc-preprocess)
#### Preprocess directives in HTML, JavaScript, etc directives based off variable context

[![NPM](https://nodei.co/npm/preprocess.png?downloads=true)](https://www.npmjs.com/package/preprocess)

[![apidoc](https://npmdoc.github.io/node-npmdoc-preprocess/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-preprocess_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-preprocess/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-preprocess/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-preprocess/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Jarrod Overson",
        "email": "jsoverson@gmail.com",
        "url": "http://jarrodoverson.com/"
    },
    "bugs": {
        "url": "https://github.com/jsoverson/preprocess/issues"
    },
    "dependencies": {
        "xregexp": "3.1.0"
    },
    "description": "Preprocess directives in HTML, JavaScript, etc directives based off variable context",
    "devDependencies": {
        "chai": "^3.5.0",
        "chai-spies": "^0.7.0",
        "grunt": "^0.4.5",
        "grunt-benchmark": "^0.3.0",
        "grunt-cli": "^0.1.13",
        "grunt-contrib-clean": "^1.0.0",
        "grunt-contrib-copy": "^0.8.0",
        "grunt-contrib-jshint": "^1.0.0",
        "grunt-contrib-watch": "^0.6.1",
        "grunt-coveralls": "^1.0.0",
        "grunt-deps-ok": "^0.9.0",
        "grunt-mocha-istanbul": "^3.0.1",
        "grunt-mocha-test": "^0.12.7",
        "istanbul": "^0.4.2",
        "load-grunt-tasks": "^3.4.0",
        "mocha": "^2.4.5",
        "time-grunt": "^1.3.0",
        "travis-cov": "^0.2.5"
    },
    "directories": {},
    "dist": {
        "shasum": "a44e5cdd5bbb5a54f0ad289aaeed80995d7d938a",
        "tarball": "https://registry.npmjs.org/preprocess/-/preprocess-3.1.0.tgz"
    },
    "engines": {
        "node": ">= 0.10.0"
    },
    "gitHead": "a5ddda7fa80917ce04076616bfafe5837f3cf11c",
    "homepage": "https://github.com/jsoverson/preprocess",
    "keywords": [
        "directive",
        "ENV",
        "environment",
        "ifdef",
        "ifndef",
        "echo",
        "include",
        "exclude",
        "process",
        "preprocess",
        "pragma"
    ],
    "licenses": [
        {
            "type": "Apache 2.0",
            "url": "https://github.com/jsoverson/preprocess/blob/master/LICENSE"
        }
    ],
    "main": "lib/preprocess.js",
    "maintainers": [
        {
            "name": "jsoverson",
            "email": "jsoverson@gmail.com"
        },
        {
            "name": "bendingbender",
            "email": "semtexx@web.de"
        }
    ],
    "name": "preprocess",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/jsoverson/preprocess.git"
    },
    "scripts": {
        "ci": "grunt ci",
        "test": "grunt test"
    },
    "version": "3.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module preprocess](#apidoc.module.preprocess)
1.  [function <span class="apidocSignatureSpan"></span>preprocess (src, context, typeOrOptions)](#apidoc.element.preprocess.preprocess)
1.  [function <span class="apidocSignatureSpan">preprocess.</span>preprocessFile (srcFile, destFile, context, callback, options)](#apidoc.element.preprocess.preprocessFile)
1.  [function <span class="apidocSignatureSpan">preprocess.</span>preprocessFileSync (srcFile, destFile, context, options)](#apidoc.element.preprocess.preprocessFileSync)
1.  object <span class="apidocSignatureSpan">preprocess.</span>gruntMochaTestPreprocess

#### [module preprocess.gruntMochaTestPreprocess](#apidoc.module.preprocess.gruntMochaTestPreprocess)
1.  boolean <span class="apidocSignatureSpan">preprocess.gruntMochaTestPreprocess.</span>defer
1.  [function <span class="apidocSignatureSpan">preprocess.gruntMochaTestPreprocess.</span>fn (deferred)](#apidoc.element.preprocess.gruntMochaTestPreprocess.fn)
1.  number <span class="apidocSignatureSpan">preprocess.gruntMochaTestPreprocess.</span>maxTime
1.  string <span class="apidocSignatureSpan">preprocess.gruntMochaTestPreprocess.</span>name



# <a name="apidoc.module.preprocess"></a>[module preprocess](#apidoc.module.preprocess)

#### <a name="apidoc.element.preprocess.preprocess"></a>[function <span class="apidocSignatureSpan"></span>preprocess (src, context, typeOrOptions)](#apidoc.element.preprocess.preprocess)
- description and source-code
```javascript
function preprocess(src, context, typeOrOptions) {
  src = src.toString();
  context = context || process.env;

  // default values
  var options = {
    fileNotFoundSilentFail: false,
    srcDir: process.cwd(),
    srcEol: getEolType(src),
    type: delim['html']
  };

  // needed for backward compatibility with 2.x.x series
  if (typeof typeOrOptions === 'string') {
    typeOrOptions = {
      type: typeOrOptions
    };
  }

  // needed for backward compatibility with 2.x.x series
  if (typeof context.srcDir === "string") {
    typeOrOptions = typeOrOptions || {};
    typeOrOptions.srcDir = context.srcDir;
  }

  if (typeOrOptions && typeof typeOrOptions === 'object') {
    options.srcDir = typeOrOptions.srcDir || options.srcDir;
    options.fileNotFoundSilentFail = typeOrOptions.fileNotFoundSilentFail || options.fileNotFoundSilentFail;
    options.srcEol = typeOrOptions.srcEol || options.srcEol;
    options.type = delim[typeOrOptions.type] || options.type;
  }

  context = copy(context);

  return preprocessor(src, context, options);
}
```
- example usage
```shell
...
## Usage Examples

'''js
var pp = require('preprocess');

var text = 'Hi, I am <!-- @echo USERNAME -->';

pp.preprocess(text);
// -> Hi, I am jsoverson

pp.preprocess(text, {USERNAME : "Bob"});
// -> Hi, I am Bob

// specify the format to use for the directives as the third parameter
pp.preprocess(text, {USERNAME : "Bob"}, {type: 'html'});
...
```

#### <a name="apidoc.element.preprocess.preprocessFile"></a>[function <span class="apidocSignatureSpan">preprocess.</span>preprocessFile (srcFile, destFile, context, callback, options)](#apidoc.element.preprocess.preprocessFile)
- description and source-code
```javascript
function preprocessFile(srcFile, destFile, context, callback, options) {
  options = getOptionsForFile(srcFile, options);
  context.src = srcFile;

  fs.readFile(srcFile, function (err, data) {
    if (err) return callback(err, data);
    var parsed = preprocess(data, context, options);
    fs.writeFile(destFile, parsed, callback);
  });
}
```
- example usage
```shell
...
// -> Hi, I am Bob

// specify the format to use for the directives as the third parameter
pp.preprocess(text, {USERNAME : "Bob"}, {type: 'html'});
// -> Hi, I am Bob

// Preprocess files asynchronously
pp.preprocessFile(src, dest, context, callback, options);

// Preprocess files synchronously
pp.preprocessFileSync(src, dest, context, options);
'''

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or
...
```

#### <a name="apidoc.element.preprocess.preprocessFileSync"></a>[function <span class="apidocSignatureSpan">preprocess.</span>preprocessFileSync (srcFile, destFile, context, options)](#apidoc.element.preprocess.preprocessFileSync)
- description and source-code
```javascript
function preprocessFileSync(srcFile, destFile, context, options) {
  options = getOptionsForFile(srcFile, options);
  context.src = srcFile;

  var data = fs.readFileSync(srcFile);
  var parsed = preprocess(data, context, options);
  return fs.writeFileSync(destFile, parsed);
}
```
- example usage
```shell
...
pp.preprocess(text, {USERNAME : "Bob"}, {type: 'html'});
// -> Hi, I am Bob

// Preprocess files asynchronously
pp.preprocessFile(src, dest, context, callback, options);

// Preprocess files synchronously
pp.preprocessFileSync(src, dest, context, options);
'''

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or
changed functionality. Lint and test your code using jshint

## Release History
...
```



# <a name="apidoc.module.preprocess.gruntMochaTestPreprocess"></a>[module preprocess.gruntMochaTestPreprocess](#apidoc.module.preprocess.gruntMochaTestPreprocess)

#### <a name="apidoc.element.preprocess.gruntMochaTestPreprocess.fn"></a>[function <span class="apidocSignatureSpan">preprocess.gruntMochaTestPreprocess.</span>fn (deferred)](#apidoc.element.preprocess.gruntMochaTestPreprocess.fn)
- description and source-code
```javascript
fn = function (deferred) {
  var spawnGrunt = spawn(process.argv[0], [process.argv[1], 'mochaTest:preprocess']);

  spawnGrunt.stderr.on('data', function(data) {
    deferred.resolve();
    throw new Error(data);
  });

  spawnGrunt.on('exit', function() {
    deferred.resolve();
  });
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
