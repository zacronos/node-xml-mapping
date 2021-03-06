# xml2json and json2xml for NodeJS

It's native javascript implementation of a bidirectional converter between XML and JS data structure (aka JSON).
You can convert any type of XML documents in an Javascript data structure.
You can also do the reverse, converting a Javascript data structure in XML String. XML is still valid.

This is a fork of https://github.com/lindory-project/node-xml-mapping with improvements made to allow optional
throwing of parser errors rather than the default of tossing them away.

# Installation

With [npm](http://npmjs.org) do:

    $ npm install git+https://github.com/zacronos/node-xml-mapping.git


# Usage
```javascript
var xm = require('xml-mapping');

// will not throw errors -- ignores them instead
var json = xm.load('<key>value</key>');
var xml  = xm.dump(json);

console.log(xml);
console.log(json);

try {
    // throws parsing errors with line and column numbers
    json = xm.load('<key>value', {throwErrors: true});
} catch (err) {
    console.log(err.toString())
}
```

Output:

    <key>value</key>
    { key: { '$t': 'value' } }
    Error: Unexpected end of input
    Line: 0
    Column: 10
    Char: null


# Convention

The rules for converting XML to JSON are those used by Google in its GData protocol. More information here : http://code.google.com/apis/gdata/docs/json.html

# Tests

Use [nodeunit](https://github.com/caolan/nodeunit) to run the tests.

    $ npm install nodeunit
    $ nodeunit test

# API Documentation

## load(String xml)
Transform a string with XML in Javascript data structure (JSON). 
**Return Object.**

## dump(Object json)
Transform a Javascript data structure (JSON) in XML string. **Return String.**

## tojson(String xml)
Alias of load.

## toxml(Object json)
Alias of dump.

# Also

* https://github.com/estheban/node-json2xml
* https://github.com/buglabs/node-xml2json

# License

[MIT/X11](https://github.com/zacronos/node-xml-mapping/LICENSE)

# TODO:

* It would be nice allow passthrough of other options to SAX and XMLWriter.
* The code could be more efficient by instantiating a single parser/writer and allowing it to be reused, rather than always starting from scratch.
* It would be nice to expose SAX's incremental parsing / data buffering mechanism.
* The existing code is not reversible for html-escaped characters; this should be fixed, though the issue may lie in the underlying XMLWriter code.
