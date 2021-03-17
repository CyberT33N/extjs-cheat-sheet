# ExtJs Cheat Sheet
- Ext JS is a class-based, object-oriented framework. There are many hundreds of classes provided by Ext JS that you can use or extend to create your application. These classes range from non-visual classes that manage data and server communication to user interface components that provide powerful functionality. By creating your own classes based on these components, you can concentrate on making a compelling application







<br><br><br><br>



# Install
- https://docs.sencha.com/extjs/6.5.3/guides/getting_started/getting_started.html
```javascript
# We recommend extracting Ext JS in a fixed location in your "home" directory:
C:\Users\Me\sencha-sdks    # Windows
/Users/Me/sencha-sdks      # Mac OS X
/home/me/sencha-sdks       # Linux


# After unzipping Ext JS in this folder, you should see a sub-folder such as the following (on Windows):
C:\Users\Myname\sencha-sdks\ext-6.5.3

# Now that Sencha Cmd is installed and the Ext JS SDK is extracted, let's configure Sencha Cmd with this location. For example (on Windows):
sencha config --prop sencha.sdk.path=C:\Users\Me\sencha-sdks --save
```


<br><br><br><br>


## Initializing the Application
```javascript
# To create the application, open a terminal or command prompt and create an empty directory and "cd" into it:
md ~/myapp    # On Windows, replace "~" with "C:\Users\Me"
cd ~/myapp

# From this directory, we run "sencha app init" to create the application on disk:
sencha app init --ext@6.5.3 --modern MyApp
```

<br><br>

This will produce a few lines of output as the application code is generated and the necessary pieces of Ext JS are copied into the current directory. The current directory should now contain:
- ext651/
- .gitignore
- app.js
- app.json
- build.xml
- index.html
- workspace.json
















<br><br><br><br>


## Launching the Application
- To build the application (to allow the browser to load it), run the following command from that same directory:
```javascript
sencha app watch
```

<br><br>

You will see a few lines of information as Sencha Cmd builds the application, but there are two to take note of:
```javascript
...
[INF] Application available at http://localhost:1841
…
[INF] Waiting for changes...
```

<br><br>

While app watch is running, a basic web server is serving the application directory. Now we can load http://localhost:1841 in the browser and see the application.

<br><br>

Sencha Cmd is also monitoring your application directory for changes. Should you make changes to the styling or JavaScript code, Sencha Cmd will detect these changes and update the necessary build outputs to keep the application rendering correctly in the browser. As your changes are detected, Sencha Cmd will log a few lines of output and (in typically a couple seconds) end with "Waiting for changes…" to let you know everything is ready.




<br><br><br><br>




## Modifying the Application
- The starting point of an Ext JS application is app.js (as specified in app.json). The generated app.js file looks something like this:
```javascript
Ext.application({
    name: 'MyApp',

    requires: [
        'Ext.MessageBox'
    ],

    launch: function () {
        Ext.Msg.alert('Hello Ext JS', 'Hello! Welcome to Ext JS.');
    }
});
```































































<br><br>
__________________________________________________
__________________________________________________
<br><br>


# Explanations


## MVC
In an MVC architecture, most classes are either Models, Views or Controllers. The user interacts with Views, which display data held in Models. Those interactions are monitored by a Controller, which then responds to the interactions by updating the View and Model, as necessary.

<br><br>

The View and the Model are generally unaware of each other because the Controller has the sole responsibility of directing updates. Generally speaking, Controllers will contain most of the application logic within an MVC application. Views ideally have little (if any) business logic. Models are primarily an interface to data and contain business logic to manage changes to said data.

<br><br>

The goal of MVC is to clearly define the responsibilities for each class in the application. Because every class has clearly defined responsibilities, they implicitly become decoupled from the larger environment. This makes the app easier to test and maintain, and its code more reusable.




<br><br><br><br>



## MVVM
The key difference between MVC and MVVM is that MVVM features an abstraction of a View called the ViewModel. The ViewModel coordinates the changes between a Model’s data and the View's presentation of that data using a technique called “data binding”.

<br><br>

The result is that the Model and framework perform as much work as possible, minimizing or eliminating application logic that directly manipulates the View.









<br><br><br><br>


<br><br>

## View
- The user interacts with Views, which display data held in Models.
- You can easily say stuff that will get rendered.


## ViewModel
- The ViewModel coordinates the changes between a Model’s data and the View's presentation of that data using a technique called “data binding”.









<br><br><br><br>



## Model
- A Model or Entity represents some object that your application manages. For example, one might define a Model for Users, Products, Cars, or other real-world object that we want to model in the system. Models are used by Ext.data.Store, which are in turn used by many of the data-bound components in Ext.
- You can also call it as schema or object structure.









<br><br><br><br>

## Record
- Instances of a Model Class








<br><br><br><br>

## Store
- The Store class encapsulates a client side cache of Ext.data.Model objects. Stores load data via a Ext.data.proxy.Proxy, and also provide functions for sorting, filtering and querying the Ext.data.Model instances contained within it.







<br><br><br><br>

## Alias
- List of short aliases for class names. An alias consists of a namespace and a name concatenated by a period as <namespace>.<name>
  - namespace - The namespace describes what kind of alias this is and must be all lowercase.
  - name - The name of the alias which allows the lazy-instantiation via the alias. The name shouldn't contain any periods.














































<br><br>
__________________________________________________
__________________________________________________
<br><br>

# Ext (https://docs.sencha.com/extjs/6.5.3/modern/Ext.html)
The Ext namespace (global object) encapsulates all classes, singletons, and utility methods provided by Sencha's libraries.

<br><br>

Most user interface Components are at a lower level of nesting in the namespace, but many common utility functions are provided as direct properties of the Ext namespace.

<br><br>

Also many frequently used methods from other classes are provided as shortcuts within the Ext namespace. For example Ext.getCmp aliases Ext.ComponentManager.get.

<br><br>

Many applications are initiated with Ext.application which is called once the DOM is ready. This ensures all scripts have been loaded, preventing dependency issues. For example:
```javascript
Ext.application({
     name: 'MyApp',

     // Once the required classes are loaded and the browser is ready, the launch method is called. This is where the application performs its startup sequence. To get things started, let's define an application class and our main view.Once the required classes are loaded and the browser is ready, the launch method is called. This is where the application performs its startup sequence. To get things started, let's define an application class and our main view.
     launch: function () {
         Ext.Msg.alert(this.name, 'Ready to go!');
     }
 });
```


<br><br><br><br>

## Ext.application (https://docs.sencha.com/extjs/6.5.3/modern/Ext.html#method-application)
- Loads Ext.app.Application class and starts it up with given configuration after the page is ready.
```javascript
Ext.application({
    name: 'MyApp',

    requires: [
        'Ext.MessageBox'
    ],

    launch: function () {
        Ext.Msg.alert('Hello Ext JS', 'Hello! Welcome to Ext JS.');
    }
});
```

<br><br>

#### Include all classes by using wildmark
```javascript
Ext.application({
    name: 'MyApp',
    extend: 'MyApp.Application',  // <<== added

    requires: [
        'MyApp.*'   // tell Cmd to include all app classes
    ]
});
```










































<br><br>
__________________________________________________
__________________________________________________
<br><br>



## Ext.app.ViewModel (https://docs.sencha.com/extjs/6.5.3/modern/Ext.app.ViewModel.html)
- This class manages arbitrary data and its relationship to data models. Instances of ViewModel are associated with some Component and then used by their child items for the purposes of Data Binding.
```javascript
Ext.application({
    name: 'MyApp',

    requires: [
        'Ext.MessageBox'
    ],

    launch: function () {
        Ext.Msg.alert('Hello Ext JS', 'Hello! Welcome to Ext JS.');
    }
});
```



<br><br>
























































<br><br>
__________________________________________________
__________________________________________________
<br><br>



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

<br><br><br><br>


## Create an anonymous class
```javascript
 Ext.define(null, {
     constructor: function () {
         // ...
     }
 });
```



<br><br><br><br>


## extend from .js file
```javascript
./app/Application.js

Ext.define('MyApp.Application', {
    extend: 'Ext.app.Application',

    mainView: 'MyApp.view.main.Main'
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

## requires (https://docs.sencha.com/extjs/6.5.3/modern/Ext.Class.html#cfg-requires)
- The parent class that this class extends. It is the same logic like JS extends for classes. For example:
```javascript
Ext.define('Mother', {
    requires: ['Child'],
    giveBirth: function() {
        // we can be sure that child class is available.
        return new Child();
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


<br><br>


## alias (https://docs.sencha.com/extjs/6.5.3/modern/Ext.Class.html#cfg-alias)
- In short words custom name of your class which you can access later as example with Ext.create
```javascript
Ext.define('MyApp.CoolPanel', {
    extend: 'Ext.panel.Panel',
    alias: ['widget.coolpanel'],
    title: 'Yeah!'
});

// Using Ext.create
Ext.create('widget.coolpanel');

// Using the shorthand for defining widgets by xtype
Ext.widget('panel', {
    items: [
        {xtype: 'coolpanel', html: 'Foo'},
        {xtype: 'coolpanel', html: 'Bar'}
    ]
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



#### Ajax
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



























































<br> <br>
__________________________________________________
__________________________________________________
<br> <br>




<br><br><br><br>



# Ext.form.Panel (https://docs.sencha.com/extjs/6.5.3/classic/Ext.form.Panel.html)
- FormPanel provides a standard container for forms. It is essentially a standard Ext.panel.Panel which automatically creates a Ext.form.Basic for managing any Ext.form.field.Field objects that are added as descendants of the panel. It also includes conveniences for configuring and working with the BasicForm and the collection of Fields.

```javascript
Ext.create('Ext.form.Panel', {
    title: 'Simple Form',
    bodyPadding: 5,
    width: 350,

    // The form will submit an AJAX request to this URL when submitted
    url: 'save-form.php',

    // Fields will be arranged vertically, stretched to full width
    layout: 'anchor',
    defaults: {
        anchor: '100%'
    },

    // The fields
    defaultType: 'textfield',
    items: [{
        fieldLabel: 'First Name',
        name: 'first',
        allowBlank: false
    },{
        fieldLabel: 'Last Name',
        name: 'last',
        allowBlank: false
    }],

    // Reset and Submit buttons
    buttons: [{
        text: 'Reset',
        handler: function() {
            this.up('form').getForm().reset();
        }
    }, {
        text: 'Submit',
        formBind: true, //only enabled once the form is valid
        disabled: true,
        handler: function() {
            var form = this.up('form').getForm();
            if (form.isValid()) {
                form.submit({
                    success: function(form, action) {
                       Ext.Msg.alert('Success', action.result.msg);
                    },
                    failure: function(form, action) {
                        Ext.Msg.alert('Failed', action.result.msg);
                    }
                });
            }
        }
    }],
    renderTo: Ext.getBody()
});
```



























































<br> <br>
__________________________________________________
__________________________________________________
<br> <br>




<br><br><br><br>



# Ext.grid.Panel (https://docs.sencha.com/extjs/6.5.3/classic/Ext.grid.Panel.html)
- Grids are an excellent way of showing large amounts of tabular data on the client side. Essentially a supercharged <table>, GridPanel makes it easy to fetch, sort and filter large amounts of data.

<br><br>

Grids are composed of two main pieces - a Ext.data.Store full of data and a set of columns to render.
```javascript
Ext.create('Ext.data.Store', {
    storeId: 'simpsonsStore',
    fields:[ 'name', 'email', 'phone'],
    data: [
        { name: 'Lisa', email: 'lisa@simpsons.com', phone: '555-111-1224' },
        { name: 'Bart', email: 'bart@simpsons.com', phone: '555-222-1234' },
        { name: 'Homer', email: 'homer@simpsons.com', phone: '555-222-1244' },
        { name: 'Marge', email: 'marge@simpsons.com', phone: '555-222-1254' }
    ]
});

Ext.create('Ext.grid.Panel', {
    title: 'Simpsons',
    store: Ext.data.StoreManager.lookup('simpsonsStore'),
    columns: [
        { text: 'Name', dataIndex: 'name' },
        { text: 'Email', dataIndex: 'email', flex: 1 },
        { text: 'Phone', dataIndex: 'phone' }
    ],
    height: 200,
    width: 400,
    renderTo: Ext.getBody()
});
```













<br><br><br><br>



## Configuring columns
- By default, each column is sortable and will toggle between ASC and DESC sorting when you click on its header. Each column header is also reorderable by default, and each gains a drop-down menu with options to hide and show columns. It's easy to configure each column - here we use the same example as above and just modify the columns config:
```javascript
columns: [
    {
        text: 'Name',
        dataIndex: 'name',
        sortable: false,
        hideable: false,
        flex: 1
    },
    {
        text: 'Email',
        dataIndex: 'email',
        hidden: true
    },
    {
        text: 'Phone',
        dataIndex: 'phone',
        width: 100
    }
]
```




<br><br><br><br>



## Renderes
- As well as customizing columns, it's easy to alter the rendering of individual cells using renderers. A renderer is tied to a particular column and is passed the value that would be rendered into each cell in that column. For example, we could define a renderer function for the email column to turn each email address into a mailto link:
```javascript
columns: [
    {
        text: 'Email',
        dataIndex: 'email',
        renderer: function(value) {
            return Ext.String.format('<a href="mailto:{0}">{1}</a>', value, value);
        }
    }
]
```










<br><br><br><br>



## Sorting & Filtering
- Every grid is attached to a Ext.data.Store, which provides multi-sort and filtering capabilities. It's easy to set up a grid to be sorted from the start:
```javascript
var myGrid = Ext.create('Ext.grid.Panel', {
    store: {
        fields: ['name', 'email', 'phone'],
        sorters: ['name', 'phone']
    },
    columns: [
        { text: 'Name',  dataIndex: 'name' },
        { text: 'Email', dataIndex: 'email' }
    ]
});






// Sorting at run time is easily accomplished by simply clicking each column header. If you need to perform sorting on more than one field at run time it's easy to do so by adding new sorters to the store:
myGrid.store.sort([
    { property: 'name',  direction: 'ASC' },
    { property: 'email', direction: 'DESC' }
]);
```





































<br><br><br><br>



## Listeners (https://docs.sencha.com/extjs/6.5.3/classic/Ext.grid.Panel.html#cfg-listeners)
- A config object containing one or more event handlers to be added to this object during initialization. This should be a valid listeners config object as specified in the addListener example for attaching multiple handlers at once.
```javascript
new Ext.panel.Panel({
    width: 400,
    height: 200,
    dockedItems: [{
        xtype: 'toolbar'
    }],
    listeners: {
        click: {
            element: 'el', //bind to the underlying el property on the panel
            fn: function(){ console.log('click el'); }
        },
        dblclick: {
            element: 'body', //bind to the underlying body property on the panel
            fn: function(){ console.log('dblclick body'); }
        }
    }
});
```


#### Access data
```javascript
// row is this
// record are field from the model
listeners: {
    itemClick: {
        fn: function(row, record){
            Ext.Msg.alert('Details',
                `
                Name: ${record.get('name')}
                Description: ${record.get('description')}
                Image URL: ${record.get('profileImg')}
                `
            )
        }
    }
}
```
