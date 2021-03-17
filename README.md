# ExtJs Cheat Sheet
ExtJs Cheat Sheet Cheat Sheet with the most needed stuff..

<br> <br>




# Ext.define (https://docs.sencha.com/extjs/6.5.3/modern/Ext.html#method-define)
- Defines a class or override. A basic class is defined like this:
```javascript
 Ext.define('My.awesome.Class', {
     someProperty: 'something',

     someMethod: function(s) {
         alert(s + this.someProperty);
     }

     ...
 });

 var obj = new My.awesome.Class();

 obj.someMethod('Say '); // alerts 'Say something'
```

<br> <br>


## Create an anonymous class
```javascript
 Ext.define(null, {
     constructor: function () {
         // ...
     }
 });
```


































<br><br>
__________________________________________________
__________________________________________________
<br><br>





# Ext.create (https://docs.sencha.com/extjs/6.5.3/modern/Ext.html#method-create)
- Instantiate a class by either full name, alias or alternate name.
- 
<br><br>

If Ext.Loader is enabled and the class has not been defined yet, it will attempt to load the class via synchronous loading.

<br><br>

For example, all these three lines return the same result:
```javascript
 // xtype
 var window = Ext.create({
     xtype: 'window',
     width: 600,
     height: 800,
     ...
 });

 // alias
 var window = Ext.create('widget.window', {
     width: 600,
     height: 800,
     ...
 });

 // alternate name
 var window = Ext.create('Ext.Window', {
     width: 600,
     height: 800,
     ...
 });

 // full class name
 var window = Ext.create('Ext.window.Window', {
     width: 600,
     height: 800,
     ...
 });

 // single object with xclass property:
 var window = Ext.create({
     xclass: 'Ext.window.Window', // any valid value for 'name' (above)
     width: 600,
     height: 800,
     ...
 });
```



















































<br><br>
__________________________________________________
__________________________________________________
<br><br>





# Ext.Class (https://docs.sencha.com/extjs/6.5.3/modern/Ext.Class.html)
- This is a low level factory that is used by Ext.define and should not be used directly in application code. The configs of this class are intended to be used in Ext.define calls to describe the class you are declaring. For example:
```javascript
Ext.define('App.util.Thing', {
    extend: 'App.util.Other',

    alias: 'util.thing',

    config: {
        foo: 42
    }
});
```


<br><br>



## extend
- The parent class that this class extends. It is the same logic like JS extends for classes. For example:
```javascript
Ext.define('Person', {
    say: function(text) { alert(text); }
});

Ext.define('Developer', {
    extend: 'Person',
    say: function(text) { this.callParent(["print "+text]); }
});
```

















<br> <br>
__________________________________________________
__________________________________________________
<br> <br>


# Ext.data.Model (https://docs.sencha.com/extjs/6.5.3/classic/Ext.data.Model.html)
- A Model or Entity represents some object that your application manages. For example, one might define a Model for Users, Products, Cars, or other real-world object that we want to model in the system. Models are used by Ext.data.Store, which are in turn used by many of the data-bound components in Ext.
- You can also call it as schema

```javascript
// User in this case is the Class we will create.
Ext.define('User', {
    extend: 'Ext.data.Model',
    fields: [
        {name: 'name',  type: 'string'},
        {name: 'age',   type: 'int', convert: null},
        {name: 'phone', type: 'string'},
        {name: 'alive', type: 'boolean', defaultValue: true, convert: null}
    ],

    changeName: function() {
        var oldName = this.get('name'),
            newName = oldName + " The Barbarian";

        this.set('name', newName);
    }
});

const user = Ext.create('User', {
    id   : 'ABCD12345',
    name : 'Conan',
    age  : 24,
    phone: '555-555-5555'
});

user.changeName();
user.get('name'); //returns "Conan The Barbarian"
```



<br><br><br><br>


## The "id" Field and idProperty
- A Model definition always has an identifying field which should yield a unique key for each instance. By default, a field named "id" will be created with a mapping of "id". This happens because of the default idProperty provided in Model definitions.
-  
<br><br>

To alter which field is the identifying field, use the idProperty config.



<br><br><br><br>



## Validators
 Models have built-in support for field validators. Validators are added to models as in the follow example:
```javascript
Ext.define('User', {
    extend: 'Ext.data.Model',
    fields: [
        { name: 'name',     type: 'string' },
        { name: 'age',      type: 'int' },
        { name: 'phone',    type: 'string' },
        { name: 'gender',   type: 'string' },
        { name: 'username', type: 'string' },
        { name: 'alive',    type: 'boolean', defaultValue: true }
    ],

    validators: {
        age: 'presence',
        name: { type: 'length', min: 2 },
        gender: { type: 'inclusion', list: ['Male', 'Female'] },
        username: [
            { type: 'exclusion', list: ['Admin', 'Operator'] },
            { type: 'format', matcher: /([a-z]+)[0-9]{2,3}/i }
        ]
    }
});
```
















<br><br><br><br>



## Validation
- The results of the validators can be retrieved via the "associated" validation record:
```javascript
var instance = Ext.create('User', {
    name: 'Ed',
    gender: 'Male',
    username: 'edspencer'
});

var validation = instance.getValidation();
```

<br><br>

The returned object is an instance of Ext.data.Validation and has as its fields the result of the field validators. The validation object is "dirty" if there are one or more validation errors present.


































<br><br><br><br>



## Using a Proxy
- Models are great for representing types of data and relationships, but sooner or later we're going to want to load or save that data somewhere. All loading and saving of data is handled via a Ext.data.proxy.Proxy, which can be set directly on the Model:
```javascript
Ext.define('User', {
    extend: 'Ext.data.Model',
    fields: ['id', 'name', 'email'],

    proxy: {
        type: 'rest',
        url : '/users'
    }
});


var user = Ext.create('User', {name: 'Ed Spencer', email: 'ed@sencha.com'});
user.save(); //POST /users



// Loading data via the Proxy is accomplished with the static load method:
// Uses the configured RestProxy to make a GET request to /users/123
User.load(123, {
    success: function(user) {
        console.log(user.getId()); //logs 123
    }
});
```




























<br><br><br><br>



#### Update and destroy
```javascript
//the user Model we loaded in the last snippet:
user.set('name', 'Edward Spencer');

//tells the Proxy to save the Model. In this case it will perform a PUT request to /users/123 as this Model already has an id
user.save({
    success: function() {
        console.log('The User was updated');
    }
});

//tells the Proxy to destroy the Model. Performs a DELETE request to /users/123
user.erase({
    success: function() {
        console.log('The User was destroyed!');
    }
});
```






































<br> <br>
__________________________________________________
__________________________________________________
<br> <br>




<br><br><br><br>



# Ext.data.Store (https://docs.sencha.com/extjs/6.5.3/classic/Ext.data.Store.html)
- The Store class encapsulates a client side cache of Ext.data.Model objects. Stores load data via a Ext.data.proxy.Proxy, and also provide functions for sorting, filtering and querying the Ext.data.Model instances contained within it.

<br><br>

Creating a Store is easy - we just tell it the Model and the Proxy to use for loading and saving its data:
```javascript
// Set up a model to use in our Store
 Ext.define('User', {
     extend: 'Ext.data.Model',
     fields: [
         {name: 'firstName', type: 'string'},
         {name: 'lastName',  type: 'string'},
         {name: 'age',       type: 'int'},
         {name: 'eyeColor',  type: 'string'}
     ]
 });

 var myStore = Ext.create('Ext.data.Store', {
     model: 'User',
     proxy: {
         type: 'ajax',
         url: '/users.json',
         reader: {
             type: 'json',
             rootProperty: 'users'
         }
     },
     autoLoad: true
 });
```













<br><br><br><br>



## Inline data
- Stores can also load data inline. Internally, Store converts each of the objects we pass in as cfg-data into Model instances:
```javascript
 Ext.create('Ext.data.Store', {
     model: 'User',
     data : [
         {firstName: 'Peter',   lastName: 'Venkman'},
         {firstName: 'Egon',    lastName: 'Spengler'},
         {firstName: 'Ray',     lastName: 'Stantz'},
         {firstName: 'Winston', lastName: 'Zeddemore'}
     ]
 });
```















<br><br><br><br>



## Dynamic Loading
- Stores can be dynamically updated by calling the method-load method:
```javascript
store.load({
    params: {
        group: 3,
        type: 'user'
    },
    callback: function(records, operation, success) {
        // do something after the load finishes
    },
    scope: this
});
```











<br><br><br><br>



## Filtering and Sorting
- Stores can be sorted and filtered - in both cases either remotely or locally. The cfg-sorters and cfg-filters are held inside Ext.util.Collection instances to make them easy to manage. Usually it is sufficient to either just specify sorters and filters in the Store configuration or call method-sort or filter:
```javascript
var store = Ext.create('Ext.data.Store', {
     model: 'User',
     sorters: [{
         property: 'age',
         direction: 'DESC'
     }, {
         property: 'firstName',
         direction: 'ASC'
     }],

     filters: [{
         property: 'firstName',
         value: /Peter/
     }]
 });
 
 
 
 store.filter('eyeColor', 'Brown');
 store.sort('height', 'ASC');
```














<br><br><br><br>



## Loading Nested Data
- Applications often need to load sets of associated data - for example a CRM system might load a User and her Orders. Instead of issuing an AJAX request for the User and a series of additional AJAX requests for each Order, we can load a nested dataset and allow the Reader to automatically populate the associated models. Below is a brief example, see the Ext.data.reader.Reader intro docs for a full explanation:
```javascript
 var store = Ext.create('Ext.data.Store', {
     autoLoad: true,
     model: "User",
     proxy: {
         type: 'ajax',
         url: 'users.json',
         reader: {
             type: 'json',
             rootProperty: 'users'
         }
     }
 });
 
 
 /*
 {
     "users": [{
         "id": 1,
         "name": "Peter",
         "orders": [{
             "id": 10,
             "total": 10.76,
             "status": "invoiced"
        },{
             "id": 11,
             "total": 13.45,
             "status": "shipped"
        }]
     }]
 }
 */
```
