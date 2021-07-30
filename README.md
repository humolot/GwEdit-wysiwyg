# GwEdit Editor
An excellent WYSIWYG editor written in pure TypeScript without the use of additional libraries. Its file editor and image editor.

## Get Started
## How use
Download gwedit.min.js gwedit.min.css connector.zip

### Include just two files

ES5 Version
```html
<link type="text/css" rel="stylesheet" href="build/gwedit.min.css"/>
<script type="text/javascript" src="build/gwedit.min.js"></script>
```

### USAGE

And some `<textarea>` element

```html
<textarea id="editor" name="editor"></textarea>
```
After this, you can init Gwedit plugin

```javascript
var editor = new Gwedit('#editor');
editor.value = '<p>start</p>';
```
```

With jQuery
```javascript
$('textarea').each(function () {
    var editor = new Gwedit(this);
    editor.value = '<p>start</p>';
});
```


and set options for Gwedit:
```javascript
var editor = new Gwedit('#editor', {
    uploader: {
        url: 'http://localhost:8080/connector/index.php?action=fileUpload'
    },
    filebrowser: {
        ajax: {
            url: 'http://localhost:8080/connector/index.php'
        }
    },
    toolbarButtonSize: 'small', //tiny, xsmall, small, large
    language: 'es',
    autofocus: true,
    iframe: true,
    defaultMode: '2', //1,2,3
    enter: 'P', // P,DIV,BR
    direction: 'rtl', //rtl, ltr
    buttons: 'source,bold,italic,underline,strikethrough,eraser,superscript,subscript,ul,ol,indent,outdent,left,font,fontsize,paragraph,classSpan',
    saveHeightInStorage: true,
    saveModeInStorage: true,
    readonly: true,
    height:150, // Remove to Auto
    minHeight: 450,
    maxHeight: 600,
    width: 800, // Remove to Auto
    minWidth: 450,
    maxWidth: 600,
    disablePlugins: 'about,focus,class-span,delete,bold,clean-html,wrap-text-nodes,copy-format,clipboard,paste,paste-storage,color,drag-and-drop,drag-and-drop-element,enter,error-messages,font,format-block,fullsize,hotkeys,iframe,indent,hr,inline-popup,justify,limit,link,mobile,ordered-list,placeholder,redo-undo,resizer,search,select,size,resize-handler,source,stat,sticky,symbols,tooltip,xpath,image-properties,image-processor,image,media,video,file,resize-cells,table-keyboard-navigation,select-cells,table,preview,print'
    
});
```

### Create plugin

```javascript
Gwedit.plugins.yourplugin = function (editor) {
    editor.events.on('afterInit', function () {
        editor.s.insertHTMl('Text');
    });
}
```

### Add custom button
```javascript
var editor = new Gwedit('.someselector', {
    extraButtons: [
        {
            name: 'insertDate',
            iconURL: 'http://example.com/logo.png',
            exec: function (editor) {
                editor.s.insertHTML((new Date).toDateString());
            }
        }
    ]
})
```
or

```javascript
var editor = new Gwedit('.someselector', {
	buttons: ['bold', 'insertDate'],
    controls: {
        insertDate: {
            name: 'insertDate',
            iconURL: 'http://example.com/logo.png',
            exec: function (editor) {
                editor.s.insertHTML((new Date).toDateString());
            }
        }
    }
})
```

button with plugin

```javascript
Gwedit.plugins.add('insertText', function (editor) {
    editor.events.on('someEvent', function (text) {
        editor.s.insertHTMl('Hello ' + text);
    });
});

// or

Gwedit.plugins.add('textLength', {
	init(editor) {
		const div = editor.create.div('jodit_div');
		editor.container.appendChild(div);
		editor.events.on('change.textLength', () => {
			div.innerText = editor.value.length;
		});
	},
	destruct(editor) {
		editor.events.off('change.textLength')
	}
});

// or use class

Gwedit.plugins.add('textLength', class textLength {
	init(editor) {
		const div = editor.create.div('jodit_div');
		editor.container.appendChild(div);
		editor.events.on('change.textLength', () => {
			div.innerText = editor.value.length;
		});
	}
	destruct(editor) {
		editor.events.off('change.textLength')
	}
});

var editor = new Gwedit('.someselector', {
	buttons: ['bold', 'insertText'],
    controls: {
        insertText: {
            iconURL: 'http://example.com/logo.png',
            exec: function (editor) {
                editor.events.fire('someEvent', 'world!!!');
            }
        }
    }
})
```

## Browser Support
______________________
* Internet Explorer 11
* Latest Chrome
* Latest Firefox
* Latest Safari
* Microsoft Edge


## Contributing

GOODBITS TECH 
goodbits.tech

## License

MIT


