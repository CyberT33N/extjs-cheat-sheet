# ExtJs Cheat Sheet
ExtJs Cheat Sheet Cheat Sheet with the most needed stuff..






<br><br>


# Ext.data.Model (https://docs.sencha.com/extjs/6.5.3/classic/Ext.data.Model.html)
- A Model or Entity represents some object that your application manages. For example, one might define a Model for Users, Products, Cars, or other real-world object that we want to model in the system. Models are used by Ext.data.Store, which are in turn used by many of the data-bound components in Ext.
- You can also call it as schema

```javascript
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



<br> <br>
__________________________________________________
__________________________________________________
<br> <br>
