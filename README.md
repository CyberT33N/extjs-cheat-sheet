# ExtJs Cheat Sheet
ExtJs Cheat Sheet Cheat Sheet with the most needed stuff..






<br> <br>


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
```




<br> <br>
__________________________________________________
__________________________________________________
<br> <br>
