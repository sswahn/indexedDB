# Database
Easily interact with the IndexedDB API with a simplified, promise-based approach.

## Features
  · Simplified promise-based API  
  · Singleton pattern ensures one instance of the database is active  
  · Default setup pre-configured  
  · Bulk addition of items  

## Usage  

```javascript
import database from '@sswahn/indexedDB'

// Initialize with custom configuration (optional)
const db = database([
  {
    storeName: 'customStore',
    keyPath: 'customID',
    indexes: [
      {
        name: 'indexName',
        keyPath: 'indexKeyPath',
        unique: false
      }
    ]
  }
])

// Add item
db.add({ customID: 1, name: 'John Doe' }, 'customStore')

// Get item
db.get(1, 'customStore')

// Get all items
db.getAll('customStore')

// Get count
db.count('customStore')

// Update item
db.put({ customID: 1, name: 'Jane Doe' }, 'customStore')

// Delete item
db.remove(1, 'customStore')

// Bulk addition
db.addAll([{ customID: 2, name: 'Alice' }, { customID: 3, name: 'Bob' }], 'customStore')

// Close the connection (optional, if needed)
db.close()

```

## API  

**database(storeConfigs)**  
Initializes the database with the provided store configurations.  

**.get(key, storeName)**  
Retrieves an item by key from the specified store.

**.getAll(storeName)**  
Retrieves all items from the specified store.

**.count(storeName)**  
Retrieves count of all items in the specified store.

**.add(data, storeName)**  
Adds an item to the specified store.

**.put(data, storeName)**  
Updates an item in the specified store.

**.remove(key, storeName)**  
Deletes an item by key from the specified store.

**.addAll(items, storeName)**  
Adds multiple items to the specified store.

**.destroy(databaseName)**  
Deletes the specified database.

**.close()**  
Closes the connection to the database.

## Example  
```javascript
const db = database()

const storeLocally = async () => {
  try {
    await db.add({ id: 1, name: 'John Doe' })
    const record = await db.get(1)
    return record
  } catch (error) {
    console.error(`Error: ${error}`)
  }
}

storeLocally()
```

## Licence
Database is [MIT Licensed](https://github.com/sswahn/database/blob/main/LICENSE)
