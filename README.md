# rheactor-value-objects

[![Build Status](https://travis-ci.org/ResourcefulHumans/rheactor-value-objects.svg?branch=master)](https://travis-ci.org/ResourcefulHumans/rheactor-value-objects)
[![monitored by greenkeeper.io](https://img.shields.io/badge/greenkeeper.io-monitored-brightgreen.svg)](http://greenkeeper.io/) 
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)
[![semantic-release](https://img.shields.io/badge/semver-semantic%20release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![Test Coverage](https://codeclimate.com/github/ResourcefulHumans/rheactor-value-objects/badges/coverage.svg)](https://codeclimate.com/github/ResourcefulHumans/rheactor-value-objects/coverage)
[![Code Climate](https://codeclimate.com/github/ResourcefulHumans/rheactor-value-objects/badges/gpa.svg)](https://codeclimate.com/github/ResourcefulHumans/rheactor-value-objects)

[![NPM](https://nodei.co/npm/rheactor-value-objects.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/rheactor-value-objects/)

A collection of value objects

## Common API

### ValueType()

This method exposes a [tcomb](https://github.com/gcanti/tcomb) type validation base on `instanceof` or the **name of the type** and it's properties.

Note that instanceof can't be used always because having this check will return false, because the application using
the value-objects package will create an instance that Node.js thinks to be from a different location that the
one referenced in this package's `uri.js`

    # app.js
    const URIValue = require('rheactor-value-objects/uri')
    let u = new URIValue(…)
    URIValue.Type(u) // will fail
    
    # uri.js
    URIValue.Type = t.irreducible('URIValue', (x) => x instanceof URIValue)
  
## .equals()

You can compare two value objects with the `.equals()` method:

```javascript
const ex = new URIValue('https://example.com') 
ex.equals(new URIValue('https://example.com')) // -> true
ex.equals(new URIValue('https://acme.com'))    // -> false
```
## .is()

You can check if a given value *is* of this value object:

```javascript
const ex = new URIValue('https://example.com') 
URIValue.is(ex)    // -> true
DomainValue.is(ex) // -> false
```
