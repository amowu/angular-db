angular-db
==========

An AngularJS IndexedDB provider base on [db.js](http://aaronpowell.github.io/db.js/).

Requirement
---

- [db.js](https://github.com/aaronpowell/db.js) v0.8.0

Installation
---

Add a `<script>` to your `index.html`:

```html
<script src="db.js"></script>
<script src="angular-db.js"></script>
```
	
And add `dbService` as a dependency for your app:

```javascript
angular.module('myApp', ['dbService']);
```

Usage
---

Config IndexedDB with `dbProvider`:

```javascript
app.config(['dbProvider', function(dbProvider) {
  dbProvider.config({
    server: 'PREFIX_',
    version: 1,
    schema: {
      phones: {
        key: { keyPath: 'phoneId' }
      }
      // etc...
    }
  });
}]);
```

Use `db` service to CRUD:

```javascript
app.controller('PhoneListCtrl', ['$scope', 'db', function($scope, db) {
  db('phones').getBatch(function(phones) {
  	$scope.phones = phones;
  });
}]);

app.controller('PhoneDetailCtrl', ['$scope', '$routeParams', 'db', 
function($scope, $routeParams, db) {
  db('phones').get('phoneId', parseInt($routeParams.phoneId), function(phones) {
    $scope.mainImageUrl = phones[0].images[0];
  });
}]);
```

Documentation
---

### Adding items

```javascript
db('objectStore').putBatch(array, onSuccess);
```
### Querying all objects

```javascript
db('objectStore').getBatch(onSuccess);
```

### Getting a single object by ID

```javascript
db('objectStore').get('keyPath', value, onSuccess);
```