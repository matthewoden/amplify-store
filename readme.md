# Amplify-Store
A very, very basic node wrapper around the amplify.js store module, to set and fetch data from cookies in a commonjs style.

## Installation
```
npm install amplify-store
```
or
```
bower install amplify-store
```


## Usage

Most of this can be found on the official [amplify docs](http://amplifyjs.com/api/store/). But, as this is built around the node API, so the methods below assume you've required the file as per the following:
```
var store = require('amplify-store');
```

### Methods

If you've never used amplify.store before, it's really just one method. The arguments provided determines the functionality (fetching, setting, clearing, etc).

```
store( string key, mixed value [, hash options ] )
```
Stores a value for a given key using the default storage type.

- **key**: Identifier for the value being stored.
- **value**: The value to store. The value can be anything that can be serialized as JSON.
- **[options]**: A set of key/value pairs that relate to settings for storing the value.


```
store( string key );
```
Gets a stored value based on the key.


```
store();
```
Gets a hash of all stored values.


```
store( string key, null );
```
Clears key/value pair from the store.


```
store.storageType( string key, mixed value [, hash options ] );
```
Stores a value for a given key using an explicit storage type, where storageType is one of the available storage types through amplify.store. The storage types available by default are listed below.


```
store.storageType( string key )
```
Gets a stored value based upon key for the explicit storage type.


```
store.storageType()
```
Gets a hash of all stored values which were stored through amplify.store.


### Options

**expires**: Duration in milliseconds that the value should be cached.

#### Storage Types
Support for the following storage types are built into amplify.store and are detected in the order listed. The first available storage type will become the default storage type when using amplify.store().

**localStorage**

- IE 8+
- Firefox 3.5+
- Safari 4+
- Chrome
- Opera 10.5+
- Phone 2+
- Android 2+

**sessionStorage**

- IE 8+
- Firefox 2+
- Safari 4+
- Chrome
- Opera 10.5+
- iPhone 2+
- Android 2+

**globalStorage**

- Firefox 2+

**userData**

- IE 5 - 7
(userData exists in newer versions of IE as well, but due to quirks in IE 9's implementation, we don't register userData if localStorage is supported.)

**memory**
- An in-memory store is provided as a fallback if none of the other storage types are available.

## Examples
Store data with amplify storage picking the default storage technology:
```javascript
var store = require('amplify-store');
store( "storeExample1", { foo: "bar" } );
store( "storeExample2", "baz" );

// retrieve the data later via the key
var myStoredValue = store( "storeExample1" ),
    myStoredValue2 = store( "storeExample2" ),
    myStoredValues = store();

myStoredValue.foo; // bar
myStoredValue2; // baz
myStoredValues.storeExample1.foo; // bar
myStoredValues.storeExample2; // baz
```


Store data explicitly with session storage

```javascript
var store = require('amplify-store');
store.sessionStorage( "explicitExample", { foo2: "baz" } );
// retrieve the data later via the key
var myStoredValue2 = store.sessionStorage( "explicitExample" );
myStoredValue2.foo2; // baz
```
