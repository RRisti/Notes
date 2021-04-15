```javascript
// Get the registry
const registry = require('uiRegistry');
```

```javascript
// Example callback
const cb = (...rest) => console.log(...rest);

// Example single query
const query = 'customer';

// Example multiple queries
const queries = [
    'customer',
    'personalData'
];

// Search, by key-value object pairs
const search = 'a = 3, b = 25';
```

### Get data
#### Synchronous
```javascript
// Single entry. Potentailly trying to access data before being initialized
cb(registry.get(query));
```

```javascript
// Get first entry matching "key = value" pairs. 
cb(registry.get(search));
```

```javascript
// Get array of entries matching "key = value" pairs.
cb(registry.filter(search));
```

#### Asynchronous
##### Callback
```javascript
// Single entry
registry.get(query, cb);
```

```javascript
// Multiple entries
registry.get(queries, cb);
```

##### $.Deferred
```javascript
// Single entry
registry.promise(query).then(cb);
```

```javascript
// Multiple entries
registry.promise(queries).then(cb);
```


### Set data
```javascript
registry.set('id', {
    a: 'foo',
    b: 'bar',
});
```

### Remove data
```javascript
registry.remove('id');
```

### Iterate through the defined entries
```javascript
const iterator = (entry, name, currentRegistry) => cb(entry, name, currentRegistry);

registry.get(iterator);
```

### Create a new instance of registy
```javascript
const newRegistry = registry.create();
```

### Async method hooking, even before the entry is initialized
```javascript
const id = 'customEntry';
const action = registry.async(id);

// Register actions, and call once if it's initialized, in the same order
action('update', 'param:1:1', 'param:1:2');
action('update', 'param:2:1', 'param:2:2');

// Set entry, trigger action if it hasn't been already
registry.set(id, { update: cb });
```

## Check if registry contains an item, by query
```javascript
registry.has(query); // !!registry.get(query)
```

## Check if registry contains an item, by reference
```javascript
const item = registry.get(entry);

registry.contains(item); // Boolean
```

## Get index by reference
```javascript
const item = registry.get(entry);

registry.indexOf(item);
```

