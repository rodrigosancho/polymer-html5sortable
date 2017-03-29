# \<html5-sortable\>

[Polymer](https://www.polymer-project.org/) wrapper for [html5sortable](https://github.com/lukasoppermann/html5sortable) library.

## Using the element

This element must be placed always as a `parentNode` of a `dom-repeat` template.
```
<html5-sortable>
    <template is="dom-repeat"
              items="[[ items ]]">
        
    </template>
</html5-sortable>
```


### Basic list

```
<ul>  
    <html5-sortable>
        <template is="dom-repeat"
                  items="[[ items ]]">
            <li>[[ item ]]</li>        
        </template>
    </html5-sortable>
</ul>
```

### Linked lists

```
<!-- var listItems = ['Item 1', 'Item 2', 'Item 3'] -->
<ul id="list">  
    <html5-sortable connect-with="connectedlist">
        <template is="dom-repeat"
                  items="[[ listItems ]]">
            <li>[[ item ]]</li>        
        </template>
    </html5-sortable>
</ul>


<!-- var gridItems = ['1', '2', '3'] -->
<div id="grid">
    <html5-sortable connect-with="connectedlist">
        <template is="dom-repeat" 
                  items="[[ gridItems ]]">
            <li>[[ item ]]</li>
        </template>
    </html5-sortable>
</div>
```

Note: Under the hood, the `<html5-sortable>` element will move the value from the original 
array to the new one every time you drag an element. After that, `dom-repeat` elements will
notice the splices and rerender the lists. This functionality allows you to have your application 
model synchronized and ready to be used. 

### Infinite sortable tree (nested lists)


```

<!-- Defining the tree node element -->

<dom-module id="sortable-tree">
    <template>
        [[ rootNode.label ]]
        <ul>
            <html5-sortable connect-with="sortable-tree" 
                            style="min-height: 10px;">
                <template is="dom-repeat"
                          items="[[ rootNode.children ]]">
                    <li>
                        <sortable-tree root-node="[[ item ]]">
                    </li>
                </template>
            </html5-sortable>
        </ul>
    </template>
    <script>
        Polymer({
            is: 'tree',
            properties : {
                rootNode: Object
            }
        });
    </script>
</dom-module>
```
Note: In order to be able to drag elements into an empty children array, 
the `html5-sortable` element that surrounds the array's dom-repeat, 
must have a minimum height.

```
<!-- Defining the tree model -->
var tree = {
    label : 'node 1',
    children: [
        {
            label: 'node 1.1',
            children: []
        },
        {
            label: 'node 1.2',
            children: [
                {
                    label: 'node 1.2.1',
                    children: []
                },
                {
                    label: 'node 1.2.2',
                    children: []
                },
            ]
        },
        {
            label: 'node 1.3',
            children: []
        },
    ]
};
```

Showing the tree

```
<sortable-tree root-node="[[ tree ]]"></sortable-tree>

```

## Running in local

### Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your application locally.

### Viewing Your Application

```
$ polymer serve
```

### Building Your Application

```
$ polymer build
```

This will create a `build/` folder with `bundled/` and `unbundled/` sub-folders
containing a bundled (Vulcanized) and unbundled builds, both run through HTML,
CSS, and JS optimizers.

You can serve the built versions by giving `polymer serve` a folder to serve
from:

```
$ polymer serve build/bundled
```

### Running Tests

```
$ polymer test
```

Your application is already set up to be tested via [web-component-tester](https://github.com/Polymer/web-component-tester). Run `polymer test` to run your application's test suite locally.
