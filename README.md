# MySQLWrapper
An NodeJS mysql wrapper to convert objects to the full query String! Nice to simplify the work with MySQL in a Node Enviroment

## Features

  * Handling Database connection
  * Create Tables with all around like PK or FK
  * Create Database Entrys
  * Update Database Entrys
  * Delete Database Entrys

## Usage

### Establish a connection & Create a Table 

```javascript
const { Database } = require('@jodu555/mysqlapi');

const database = Database.createDatabase('host', 'username', 'password', 'database');
database.connect();

database.createTable('tablename', {
    options: {
        PK: 'UUID'
    },
    'columName': {
        type: 'columType',
        null: false,
    },
});
```

### Create a Table with Foreign Keys
#### This Means that to the colum user_UUID will created an FK to the table users in the colum UUID

```javascript
database.createTable('services', {
    options: {
        PK: 'UUID',
        FK: {
            'user_UUID': 'users/UUID',
        },
    },
    'UUID': {
        type: 'varchar(64)',
        null: false,
    },
    'user_UUID': {
        type: 'varchar(64)',
        null: false,
    },
    'name': 'varchar(64)',
});
```

### Work with the database in other classes | PUT this before you all over before you acces the database

```javascript
const { Database } = require('@jodu555/mysqlapi');
const database = Database.getDatabase();
database. //some other function like get('tablename')
```

### Create an Entry in a Table 

```javascript
database.get('tablename').create({
    columName: 'columValue',
});
```

### Get one or more Entry/s from a Table 

```javascript
//Returns one row
database.get('tablename').getOne({
    searchColumName: 'searchColumValue',
});

//Returns an Array of rows
database.get('tablename').get({
    searchColumName: 'searchColumValue',
});
```

### Update or Delete an Entry from a Table 

```javascript
//Returns the updated row
const update = await database.get('tablename').update({
        searchColumName: 'searchColumValue'
    }, {
        updateColumName: 'updateColumValue',
    });

await database.get('tablename').delete({
        searchColumName: 'searchColumValue'
    });
```

## Projects using this API

* [Monitoring-System](https://github.com/Jodu555/MonitoringSystem-Core)

## Todos

* [ ] Add possibility to createTable to auto implement the timestamps created_AT / updated_AT
* [ ] Add the possibility to activate softdelete and add in the timestamps
* [ ] Validate if the Validation works just fine
* [ ] Add the Validation to the documentation



### This Package is not finished yet. Please dont use in production environments