---
title: v-font
---

# {{title}}

The directive `v-font` is used to integrate the fonts defined in the [module options](/options#fonts) into the website.

To do this, the respective font must be retrieved via the `$getFont` method contained in the component scope (e.g. `this`).

Fonts are specified by `family`, `weight` and `style` and can be limited to elements and viewports via the options (`media`, `selector`).

Normally the directive activates the fonts only when the viewport is reached.
It is recommended to use the property `critical` for components that are already initially contained in the viewport.

With critical component the fonts are preloaded and are initially active.  
More information on critical components can be found [here](/usage#critical-prop-for-critical-components).

For multiple fonts, a list (`Array`) can be passed.

````html

<!-- single definition -->
<element v-font="$getFont(…)">

<!-- multiple definitions -->
<element v-font="[
  $getFont(…),
  $getFont(…)
]">
````

::alert{type="danger"}
Currently it is not possible to use v-font in combination with v-html/v-text directives. The reason is a bug in Vue SSR, the directive is not applied. As long as this error exists, you can look [**here**](/directives/v-font#workarounds) for workarounds.<br>Read more: [vue-server-renderer: directive not applied to imported component](https://github.com/vuejs/vue/issues/10733).
::

## `$getFont(family, [weight, style, options])`

`$getFont` is included as a plugin and can be accessed via any component scope.  
Use `$getFont` in the `v-font` directive and create the relevant font definition.

| Key       | Type               | Requried | Description                                                     | Default  |
| --------- | ------------------ | -------- | --------------------------------------------------------------- | -------- |
| `family`  | `String`           | yes      | Font-Family e.g. `Custom Font`                                  |          |
| `weight`  | `String`, `Number` |          | Font-Style e.g. `normal`, `italic`                              | `400`    |
| `style`   | `String`           |          | Font-Weight e.g. `400`, `normal`                                | `normal` |
| `options` | `Object`           |          | Media & Selector Options [see more](/directives/v-font#options) |          |

### options

Each definition can be modified in its behaviour via the options.  
With the property `media`, the call of the font definition can be made dependent on the viewport.
The property `selector` can be used to limit the font to elements (e.g. `span`, `.class`).

````js
{
  media: '(min-width: 768px)',
  selector: 'element, .elm, .elm:before'
}
````

| Key        | Type     | Requried | Description                                    | Default |
| ---------- | -------- | -------- | ---------------------------------------------- | ------- |
| `media`    | `String` |          | CSS Media Query e.g. `(min-width: 768px)`      |         |
| `selector` | `String` |          | CSS Selector e.g. `element, .elm, .elm:before` |         |

## Examples

### Basic Usage

````html
<element v-font="$getFont('Font Family', 700)">Text…</element>
````

### Advanced Usage

````js
[
  
  // Font wird auf alles angewendet
  $getFont('Font Family A'),

  // Font wird auf `b` und `strong` Tags angwendet
  $getFont('Font Family B', 700, 'normal', { selector: 'b, strong' }),

  // Font erscheint erst ab Viewport `>768px`
  $getFont('Font Family B', 400, 'normal', { media: '(min-width: 768px)' }),

  // Font wird auf `b` und `strong` Tags angwendet und erscheint erst ab Viewport `>768px`
  $getFont('Font Family B', 700, 'normal', { selector: 'b, strong', media: '(min-width: 768px)' })

]
````

## Workarounds

Workarounds to prevent bugs with default nuxt components and directives, read more in [Usage](/directives/v-font#usage).

### Use component

**<span style="color: red;">Bad</span>**

````html
<template>
  <nuxt-link to="/" v-font="$getFont(…)">Back</nuxt-link>
</template>
````

**<span style="color: green;">Good</span>**

````html
<template>
  <nuxt-link to="/">
    <span v-font="$getFont(…)">Back</span>
  </nuxt-link>
</template>
````

### Use v-html/v-text

**<span style="color: red;">Bad</span>**

````html
<template>
  <div>
    <div v-font="$getFont(…)" v-html="…" />
  </div>
</template>
````

**<span style="color: green;">Good</span>**

````html
<template>
  <div v-font="$getFont(…)">
    <div v-html="…" />
  </div>
</template>
````
