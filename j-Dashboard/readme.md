## j-Dashboard

- Works only with `+v18`
- Supports mobile devices
- Supports touches
- Movable
- Draggable
- Resizable

The component expects `Array` of objects.

__Configuration__:

- `axisX` {Number} a size of grid of X axis (default: `12`)
- `axisY` {Number} a size of grid of Y axis (default: `144`)
- `padding` {Number} a padding between widgets (default: `10`)
- `delay` {Number} init delay (default: `200`)
- `serviceinterval` {Number} a service interval (default: `5000`)
- `ondrop` {String} a path to method `function(meta) {}`, is executed if someone drops some element into area
	- `meta.x` X grid position
	- `meta.y` Y grid position
	- `meta.el` dragged element
	- `meta.pageX`
	- `meta.pageY`
	- `meta.offsetX`
	- `meta.offsetY`
	- `meta.target`
	- `meta.d` a display mode `xs`, `sm`, `md` or `lg`
- `noemitresize` disables executing of `resize` method in all nested component (default: `false`)
- `parent` {String} a parent container which sets a minimal height (default: `null`)

```javascript
// Component declaration
var component = {

	// Component ID
	id: 'COMPONENT_ID',

	// Positioning
	// You can define specific display size and if the display size is not specified then the component tries to find a size for larger display
	offset: {
		xs: { x: 1, y: 1, width: 6, height: 6 }, // Number means the position in the grid, so e.g. width "2" takes "2" columns in X axis
		lg: { x: 1, y: 1, width: 6, height: 6 }
	},

	html: 'THE CONTENT OF COMPONENT', // or can be raw HTMLElement

	// Default settings
	actions: { move: true, remove: true, resize: true, settings: true },

	// Can disable header (default: true)
	header: true,

	// Can delay displaying (in "ms", default: config.delay)
	delay: 0,

	// A component title
	title: 'Title for the component',

	// Custom properties which will be assigned to the instance
	template: Object,
	config: Object,

	// Handlers (optional):
	destroy: function() {
		// @el {jQuery} a content of the component
		// @this {Instance}

		// is executed when the component is destroyed
	},

	make: function(meta, el) {

		// @el {jQuery} a content of the component
		// @this {Instance}

		// this.meta {Object} a reference to component object
		// this.element {jQuery} a content element of the component
		// this.container {jQuery} a main content element of the component
		// this.main {Object} a reference to Dashboard component
		// this.width {Number} a width of "this.element"
		// this.height {Number} a height of "this.element"
		// this.display {String} a current display size "xs", "sm", "md" or "lg"

		// is executed when the component is making
	},

	data: function(type, data, el) {

		// @type {String}
		// @data {Object}
		// @this {Instance}
		// @el {jQuery} a content element of the component

		// is executed when data are sent via SETTER('dashboard', 'send', 'TYPE', 'DATA')
	},

	settings: function(config, el) {

		// @config {Object}
		// @el {jQuery} a content element of the component

		// is executed when the users clicks on the settings icon
	},

	resize: function(width, height, el, display) {

		// @width {Number}
		// @height {Number}
		// @el {jQuery} a content of the component
		// @display {String} a current display size "xs", "sm", "md" or "lg"
		// @this {Instance}

		// is executed when the component is resized
		// @this {Instance}
	},

	service: function(counter, el) {

		// @counter {Number} count of calls
		// @el {jQuery} a content of the component
		// @this {Instance}

		// dashboard will execute this handler each 5 seconds
	}
};

PUSH('components', component);
```

__Methods__:

- `SETTER('dashboard/send', type, body)` sends data to all widgets which contain `data` delegate

__Good to know__:

- each component (in the Dashboard) contains `d-COMPONENTNAME` class
- component adds classes to component's body:
	- `d_colNUMBER` determins count of taken columns e.g. `d_col2`
	- `d_rowNUMBER` determins count of taken rows e.g. `d_row3`
	- `d_square` the component has same width/height
	- `d_vertical` the component has only 1 step of width and more than 1 steps of height
	- `d_horizontal` the component has only 1 step of height and more than 1 steps of width

### Author

- Peter Širka <petersirka@gmail.com>
- [License](https://www.totaljs.com/license/)