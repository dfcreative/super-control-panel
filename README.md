# settings-panel [![unstable](https://img.shields.io/badge/stability-unstable-green.svg)](http://github.com/badges/stability-badges)

UI for an object.

<!-- TODO: really simple tiny cute image here -->
[![settings-panel](https://raw.githubusercontent.com/dfcreative/settings-panel/gh-pages/images/preview.png "settings-panel")](http://dfcreative.github.io/settings-panel/)

_typer_ theme, for other themes see [demo](http://dfcreative.github.io/settings-panel/).

## Usage

[![npm install settings-panel](https://nodei.co/npm/settings-panel.png?mini=true)](https://npmjs.org/package/settings-panel/)

```js
let createSettings = require('settings-panel')

let settings = createSettings({
  number: 97,
  range: [0, 100],
  checkbox: false,
  text: 'Hello world',
  color: '#aabbcc',
  select: ['Option 1', 'Option 2', 'Option 3'],
  ok: e => alert('click')
})

settings.number = 100
```

### createSettings(fields, options?, onchange?)

Create object with its properties reflected in UI. Changing property values of this object updates UI, and vice versa.

`fields` argument defines property controls. That can be a list:

```js
settings = createSettings([
  {id: 'fieldA', type: 'checkbox', ...},
  {id: 'fieldB', type: 'number', ...},
  ...
])
```

a dict:

```js
settings = createSettings({
  fieldA: {
    order: 0,
    type: 'checkbox',
    label: 'My Checkbox',
    value: true,
    change: value => {}
  },
  fieldB: {
    order: 1,
    type: 'number',
    ...
  },
  ...
})
```

or an object with direct values (eg. some options):

```js
settings = createSettings({
  value: 1,
  center: [2, 3],
  inversed: true,
  ...
})
```

Field param | Default | Meaning
---|---|---
`id` | dashcase `label` | Property key.
`value` | `null` | Property value.
`type` | detected from `value` | Property control type, one of the table below or any `<input>` type.
`order` | incremental | Position of the control in panel.
`label` | camelcase `id` | Label for the control. `false` disables label.
`title` | `label` | Tooltip text.
`hidden` | `false` | Hides control from panel.
`disabled` | `false` | Disables control interactivity.
`min`, `max` | `0..100` | Numeric controls range.
`step`, `steps` | `1` | Numeric control step or stops.
`multi` | detected from `value` | Makes range an interval and select a multiselect.
`options` | `[]` | Choice control options, either an array `['Label1', 'Label2', ...]` or an object `{Label1: value1, Label2: value2}`.
`placeholder` | `null` | Textual controls placeholder.


`options` argument may adjust appearance of the panel:

```js
createSettings(fields, {
  title: 'Settings',
  position: 'left',
  drag: false,
  theme: 'flat',
  colors: ['black', 'white']
})
```

Option | Default | Meaning
---|---|---
`title`, `header` | `false` | Panel title.
`container` | `document.body` | The container element or selector.
`position` | `'top-right'` | One of `top-left`, `top`, `top-right`, `right`, `bottom-right`, `bottom`, `bottom-left`, `left`, `center` or `popup`.
`theme` | `'flat'` | One of `control`, `dat`, `dragon`, `flat`, `typer`. See [`all themes`](https://github.com/dfcreative/settings-panel/tree/master/theme).
`colors` | `['black', 'white']` | Theme palette.
`background` | theme default | Panel background color.
`collapse` | `false` | Collapse to options sign.
`font` | `13` | Customize font and/or font size.
<!-- `labelWidth` | `'9em'` | -->
<!-- `inputHeight` | `'1.6em'` | -->
<!-- `fontFamily` | `'sans-serif'` | -->
<!-- `css` | `''` | additional css, aside from the theme’s one. Useful for custom styling -->
<!-- `className` | `'` | appends additional className to the panel element. -->

`onchange` is fired every time any value changes:

```js
let settings = createSettings({
  cancel: {label: 'Cancel', type: 'button', input: e => alert('cancel')},
  ok: {label: 'Ok', type: 'button', input: e => alert('ok')}
}, e => {
  console.log(e)
})

// read values
let [from, to] = settings.interval

// write values
settings.range = 50
Object.assign(settings, {color: '#aabbcc', textarea: 'Lorem Ipsum'})

// use as options for other components
myComponent.update(settings)

options.c = false // GUI is updated here
```

### settings.get()

Read control value.

### settings.set()

Write control value.

### settings.create()

Create a new control based on options.

### settings.read()

Get control parameters.

### settings.update()

Update control parameters.

### settings.delete()

Delete control from panel.



## Controls

```js
let settings = createSettings({
  switch: { order: 0, label: 'Switch', type: 'switch', value: 'One', options: ['One', 'Two', 'Three']},
  range: { order: 0, label: 'Range', value: 97},
  interval: { order: 1, label: 'Interval', type: 'range', multiple: true, value: [33, 77]},
  checkbox: { order: 2, label: 'Checkbox group', type: 'checkbox', value: ['b', 'c'],
    options: {a: 'Option A', b: 'Option B', c: 'Option C'}
  },
  text: { order: 3, label: 'Text', value: 'my setting'},
  color: { order: 4, label: 'Color', value: 'rgb(100, 200, 100)'},
  select: { order: 5, label: 'Select', value: 'State One', options: ['State One', 'State Two', 'State Three']},
  textarea: { order: 6, label: 'Textarea', type: 'textarea', placeholder: 'long text...'},
  cancel: {label: 'Cancel', type: 'button', input: e => alert('cancel')},
  ok: {label: 'Ok', type: 'button', input: e => alert('ok')}
})
```

[Image here]

<!--
`range`, `interval` |
`checkbox` |
`color` |
`select` |
`switch` |
`textarea` |
`text` |
`number` | -->
<!-- `canvas` | -->
<!-- `pad` | -->
<!-- `angle` | -->
<!-- `toggle` | -->
<!-- `gradient` | -->
<!-- `palette` | -->
<!-- `taglist` | -->
<!-- `file` | -->
<!-- `date` | -->
<!-- `time` | -->
<!-- `vec2`, `vec3`, `vec4` | -->
<!-- `volume` | -->
<!-- `log` | Logs output -->
<!-- `unit` | -->
<!-- `font` | -->
<!-- `ratio` | -->
<!-- `mic` | -->




## Analogs

* [control-panel](https://github.com/freeman-lab/control-panel) — original forked settings panel.<br/>
* [oui](https://github.com/wearekuva/oui) — sci-ish panel.<br/>
* [dat.gui](https://github.com/dataarts/dat.gui) — other oldschool settings panel.<br/>
* [quicksettings](https://github.com/bit101/quicksettings) — an alternative versatile settings panel.<br/>
* [dis-gui](https://github.com/wwwtyro/dis-gui) — remake on dat.gui.<br/>

## License

(c) 2017 Dima Yv. MIT License

