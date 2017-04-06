# api documentation for  [encoding (v0.1.12)](https://github.com/andris9/encoding#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-encoding.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-encoding) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-encoding.svg)](https://travis-ci.org/npmdoc/node-npmdoc-encoding)
#### Convert encodings, uses iconv by default and fallbacks to iconv-lite if needed

[![NPM](https://nodei.co/npm/encoding.png?downloads=true)](https://www.npmjs.com/package/encoding)

[![apidoc](https://npmdoc.github.io/node-npmdoc-encoding/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-encoding_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-encoding/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-encoding/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-encoding/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Andris Reinman"
    },
    "bugs": {
        "url": "https://github.com/andris9/encoding/issues"
    },
    "dependencies": {
        "iconv-lite": "~0.4.13"
    },
    "description": "Convert encodings, uses iconv by default and fallbacks to iconv-lite if needed",
    "devDependencies": {
        "iconv": "~2.1.11",
        "nodeunit": "~0.9.1"
    },
    "directories": {},
    "dist": {
        "shasum": "538b66f3ee62cd1ab51ec323829d1f9480c74beb",
        "tarball": "https://registry.npmjs.org/encoding/-/encoding-0.1.12.tgz"
    },
    "gitHead": "91ae950aaa854a119122c27cdbabd8c5585106f7",
    "homepage": "https://github.com/andris9/encoding#readme",
    "license": "MIT",
    "main": "lib/encoding.js",
    "maintainers": [
        {
            "name": "andris",
            "email": "andris@node.ee"
        }
    ],
    "name": "encoding",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/andris9/encoding.git"
    },
    "scripts": {
        "test": "nodeunit test"
    },
    "version": "0.1.12"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module encoding](#apidoc.module.encoding)
1.  [function <span class="apidocSignatureSpan">encoding.</span>convert (str, to, from, useLite)](#apidoc.element.encoding.convert)



# <a name="apidoc.module.encoding"></a>[module encoding](#apidoc.module.encoding)

#### <a name="apidoc.element.encoding.convert"></a>[function <span class="apidocSignatureSpan">encoding.</span>convert (str, to, from, useLite)](#apidoc.element.encoding.convert)
- description and source-code
```javascript
function convert(str, to, from, useLite) {
    from = checkEncoding(from || 'UTF-8');
    to = checkEncoding(to || 'UTF-8');
    str = str || '';

    var result;

    if (from !== 'UTF-8' && typeof str === 'string') {
        str = new Buffer(str, 'binary');
    }

    if (from === to) {
        if (typeof str === 'string') {
            result = new Buffer(str);
        } else {
            result = str;
        }
    } else if (Iconv && !useLite) {
        try {
            result = convertIconv(str, to, from);
        } catch (E) {
            console.error(E);
            try {
                result = convertIconvLite(str, to, from);
            } catch (E) {
                console.error(E);
                result = str;
            }
        }
    } else {
        try {
            result = convertIconvLite(str, to, from);
        } catch (E) {
            console.error(E);
            result = str;
        }
    }


    if (typeof result === 'string') {
        result = new Buffer(result, 'utf-8');
    }

    return result;
}
```
- example usage
```shell
...

## Usage

Require the module

  var encoding = require("encoding");

Convert with encoding.convert()

  var resultBuffer = encoding.convert(text, toCharset, fromCharset);

Where

* **text** is either a Buffer or a String to be converted
* **toCharset** is the characterset to convert the string
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
