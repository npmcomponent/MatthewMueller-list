
# list

Generic list component, based on the [menu component](https://github.com/component/menu).
  
## Installation

    $ component install matthewmueller/list

## Features

* Custom templating support, using [minstache](https://github.com/visionmedia/minstache).
* Events for composition
* Structural CSS
* Fluent API

## Events

* `add` (item) when an item is added
* `remove` (item) when an item is removed
* `select` (item) when an item is selected

Also, list item slugs are emitted when clicked.

    list.add('First Item')
    list.on('select:0', fn)

## Example

### Message Template:

    <script type="text/template" id="message">
      <a href='#'>
        <span class='from'>{from}</span>
        <span class='subject'>{subject}</span>
        <span class='message'>{message}</span>
      </a>
    </script>

### Usage:

    var List = require('list'),
        inbox = new List;

    inbox.template(document.getElementById('message').text)

    var messages = [
      { from : 'jim', subject : 'hey', message : 'blah'},
      { from : 'matt', subject : 'sup', message : 'cool'},
      { from : 'drew', subject : 'howdy', message : 'yah'},
    ]

    inbox.add(messages, function(message) {
      console.log('invoked fn', message);
    })

    inbox.el.appendTo('body');

    inbox.on('add', function(message) {
      console.log('message added:', message);
    });

    inbox.on('remove', function(message) {
      console.log('message removed:', message);
    })

    inbox.on('select', function(message) {
      console.log('message selected:', message);
    });

    inbox.add({
      from : 'zak',
      subject : 'no way',
      message : 'crazy'
    });

    inbox.remove(3);

## API 

### List()

Create a new `List`:

var List = require('list');
var list = new List();
var list = List();

### List#template(str)

Add a template string to be used when adding items. The internal templating engine is [minstache](https://github.com/visionmedia/minstache).

    list.template('<li><a href={url}>{text}</a></li>')

### List#add(arr|obj, [fn])

Add a new list item(s). Pass each `obj` into the templating function. When `selected` the optional callback `fn` will be invoked.

    list.add({ name : 'apple' }, function(item) {
      console.log('You selected:', item.name);
    })

You can also use text and the default template:

    list.add('apple'); // <li><a href="#">apple</a></li>

### List#remove(i)

Remove an item by it's place in the list

    list.remove(0);

### List.has(i)

Checks to see if an item exists.

    list.has(1);

## License

  MIT