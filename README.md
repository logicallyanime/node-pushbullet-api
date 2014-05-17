# PushBullet API

A Node.js module for using the [PushBullet REST API](https://www.pushbullet.com/api).

## Usage

This module is very simple to use.  All you need is your PushBullet API key and you can begin pushing.

```javascript
var PushBullet = require('pushbullet');
var pusher = new PushBullet('YOUR-API-KEY');

pusher.devices(function(error, response) {
	// response is the JSON response from the API
});

pusher.note(deviceIden, noteTitle, noteBody, function(error, response) {
	// response is the JSON response from the API
});
```

Both device IDENs and device IDs can be used.  If the `deviceIden` parameter is passed as a number it is treated as a device ID.

## Callbacks

Each callback receives two arguments.  For a successful request the first argument will be `null` or `undefined`
and the second argument will be the parsed JSON response from the API.

If an error occurs at any part of the request the first argument will be an Error object.

## API

### PushBullet.me(callback);

Get the current user's information.

```javascript
pusher.me(function(err, response) {});
```

### PushBullet.devices(callback)

Retrieves a list of pushable devices.

```javascript
pusher.devices(function(error, response) {});
```

### PushBullet.deleteDevice(deviceIden, callback)

Delete a device.

```javascript
pusher.deleteDevice('u1qSJddxeKwOGuGW', function(error, response) {});
```

### PushBullet.contacts(callback)

Retrieves a list of pushable contacts.

```javascript
pusher.contacts(function(error, response) {});
```

### PushBullet.deleteContact(contactIden, callback)

Delete a contact.

```javascript
pusher.deleteContact('ubdcjAfszs0Smi', function(error, response) {});
```

### PushBullet.note(deviceIden, noteTitle, noteBody, callback)

Push a note to the specified device.

```javascript
pusher.note('u1qSJddxeKwOGuGW', 'New Note', 'Note body text', function(error, response) {});
```

### PushBullet.address(deviceIden, name, address, callback)

Push an address to the specified device.

```javascript
pusher.address('u1qSJddxeKwOGuGW', 'Fake Address', '10 Fake Street, Fakesville', function(error, response) {});
```

### PushBullet.list(deviceIden, name, listItems, callback)

Push a list to the specified device.

```javascript
var shoppingList = [
	'steaks',
	'sausages',
	'burgers',
	'buns',
	'beer'
];
pusher.list('u1qSJddxeKwOGuGW', 'BBQ', shoppingList, function(error, response) {});
```

### PushBullet.link(deviceIden, name, url, callback)

Push a link to the specified device.

```javascript
pusher.link('u1qSJddxeKwOGuGW', 'GitHub', 'https://github.com/', function(error, response) {});
```

### PushBullet.file(deviceIden, filePath, message, callback)

Push a file to the specified device.

```javascript
pusher.file('u1qSJddxeKwOGuGW', '/path/to/file', 'Important file!', function(error, response) {});
```

### PushBullet.deletePush(pushIden, callback)

Delete a push.

```javascript
pusher.deletePush('udhrSpjAewzdwpCC', function(error, response) {});
```

### PushBullet.history(options, callback)

Get the push history.

The `options` parameter can use two attributes `modified_after` and `cursor`
to control the data returned.

- `modified_after` should be a timestamp.
- `cursor` is used to select the page if the results have been paginated.

```javascript
var options = {
	modified_after: 1400000000.00000
}

pusher.history(options, function(error, response) {})
```

## Releases

### 0.5.0

- Set request defaults locally so multiple instances can be used.

### 0.4.0

- Support and prefer using device IDENs over device IDs.

### 0.3.0

- Use JSON post body rather than form encoding. Fixes empty lists.

### 0.2.0

- Update API URL

### 0.1.0

- Initial release
