[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/dark-mode-toggle)

# `<dark-mode-toggle>` Element

A custom element that allows you to easily put a *Dark Mode 🌒* toggle
or switch on your site and that adds
[`prefers-color-scheme`](https://drafts.csswg.org/mediaqueries-5/#prefers-color-scheme)
support even to browsers that don't support the media feature natively.

## Installation

From npm:

```bash
npm install --save dark-mode-toggle
```

In the browser:

```js
import * as DarkModeToggle from 'https://cdn.pika.dev/dark-mode-toggle';
```
or 

```js
import * as DarkModeToggle from 'https://unpkg.com/dark-mode-toggle';
```



## Usage

⚠️ The custom element assumes that you have organized your CSS in different files
that you load conditionally based on the **`media`** attribute in the stylesheet's
corresponding `link` element. This is a great performance pattern,
as you don't force people to download CSS that they don't need
based on their current theme preference, yet non-matching stylesheets still get loaded,
but don't compete for bandwidth in the critical rendering path.
You can also have more than one file per theme.
The example below illustrates the principle.

<!--
```
<custom-element-demo>
  <template>
    <link rel="stylesheet" href="https://googlechromelabs.github.io/dark-mode-toggle/demo/common.css">
    <link rel="stylesheet" href="https://googlechromelabs.github.io/dark-mode-toggle/demo/light.css" media="(prefers-color-scheme: light), (prefers-color-scheme: no-preference)">
    <link rel="stylesheet" href="https://googlechromelabs.github.io/dark-mode-toggle/demo/dark.css" media="(prefers-color-scheme: dark)">
    <script type="module" src="https://googlechromelabs.github.io/dark-mode-toggle/src/dark-mode-toggle.mjs"></script>
    <style>
      #dark-mode-toggle-1 {
        --dark-mode-toggle-dark-icon: url("https://googlechromelabs.github.io/dark-mode-toggle/demo/moon.png");
        --dark-mode-toggle-light-icon: url("https://googlechromelabs.github.io/dark-mode-toggle/demo/sun.png");
        --dark-mode-toggle-remember-icon-checked: url("https://googlechromelabs.github.io/dark-mode-toggle/demo/checked.svg");
        --dark-mode-toggle-remember-icon-unchecked: url("https://googlechromelabs.github.io/dark-mode-toggle/demo/unchecked.svg");
        --dark-mode-toggle-remember-font: 0.75rem 'Helvetica';
        --dark-mode-toggle-legend-font: bold 0.85rem 'Helvetica';
        --dark-mode-toggle-label-font: 0.85rem 'Helvetica';
        --dark-mode-toggle-color: var(--text-color);
        --dark-mode-toggle-background-color: none;
        --dark-mode-toggle-active-mode-background-color: var(--accent-color);
        --dark-mode-toggle-remember-filter: invert(100%);
      }
    </style>
    <next-code-block></next-code-block>
  </template>
</custom-element-demo>
```
-->
```html
<main>
  <h1>Hi there</h1>
  <img src="https://googlechromelabs.github.io/dark-mode-toggle/demo/cat.jpg"
       alt="Sitting cat in front of a tree" width="320" height="195"
       intrinsicsize="640x390">
  <p>Check out the dark mode toggle in the upper right corner!</p>
</main>
<aside>
  <dark-mode-toggle
      id="dark-mode-toggle-1"
      legend="Theme Switcher"
      appearance="switch"
      dark="Dark"
      light="Light"
      remember="Remember this"
  ></dark-mode-toggle>
</aside>
```

## Demo

See the custom element in action in the
[interactive demo](https://googlechromelabs.github.io/dark-mode-toggle/demo/index.html).
It shows four different kinds of synchronized `<dark-mode-toggle>`s.
If you use Chrome on an Android device, pay attention to the address bar's
theme color, and also note how the favicon changes.

<img src="https://user-images.githubusercontent.com/145676/59537453-ec5b0d80-8ef6-11e9-9efb-c44ed9db24b6.png" width="400" alt="Dark"> <img src="https://user-images.githubusercontent.com/145676/59537454-ec5b0d80-8ef6-11e9-8a89-5e3fbda9c15c.png" width="400" alt="Light">

## Properties

Properties can be set directly on the custom element at creation time, or
dynamically via JavaScript.

👉 Note that the dark and light **icons** are set via CSS variables, see
[Style Customization](#style-customization) below.

| Name | Required | Values | Default | Description |
| ---- | -------- | ------ | ------- | ----------- |
| `mode` | No | Any of `"dark"` or `"light"` | Defaults to whatever the user's preferred color scheme is according to `prefers-color-scheme`, or `"light"` if the user's browser doesn't support the media query. | If set overrides the user's preferred color scheme. |
| `appearance` | No | Any of `"toggle"` or `"switch"` | Defaults to `"toggle"`. | The `"switch"` appearance conveys the idea of a theme switcher (light/dark), whereas `"toggle"` conveys the idea of a dark mode toggle (on/off). |
| `permanent` | No | `true` if present | Defaults to not remember the last choice. | If present remembers the last selected mode (`"dark"` or `"light"`), which allows the user to permanently override their usual preferred color scheme. |
| `legend` | No | Any string | Defaults to no legend. | Any string value that represents the legend for the toggle or switch. |
| `light` | No | Any string | Defaults to no label. | Any string value that represents the label for the `"light"` mode. |
| `dark` | No | Any string | Defaults to no label. | Any string value that represents the label for the `"dark"` mode. |
| `remember` | No | Any string | Defaults to no label. | Any string value that represents the label for the "remember the last selected mode" functionality. |

## Events

- `colorschemechange`: Fired when the color scheme gets changed.
- `permanentcolorscheme`: Fired when the color scheme should be permanently remembered or not.

## Complete Example

Interacting with the custom element:

```js
/* On the page */
const darkModeToggle = document.querySelector('dark-mode-toggle');

// Set the mode to dark
darkModeToggle.mode = 'dark';
// Set the mode to light
darkModeToggle.mode = 'light';

// Set the legend to "Dark Mode"
darkModeToggle.legend = 'Dark Mode';
// Set the light label to "off"
darkModeToggle.light = 'off';
// Set the dark label to "on"
darkModeToggle.dark = 'on';

// Set the appearance to resemble a switch (theme: light/dark)
darkModeToggle.appearance = 'switch';
// Set the appearance to resemble a toggle (dark mode: on/off)
darkModeToggle.appearance = 'toggle';

// Set a "remember the last selected mode" label
darkModeToggle.remember = 'Remember this';

// Remember the user's last color scheme choice
darkModeToggle.setAttribute('permanent', '');
// Forget the user's last color scheme choice
darkModeToggle.removeAttribute('permanent');
```

Reacting on color scheme changes:

```js
  /* On the page */
  document.addEventListener('colorschemechange', (e) => {
    console.log(`Color scheme changed to ${e.detail.colorScheme}.`);
  });
```

Reacting on "remember the last selected mode" functionality changes:

```js
  /* On the page */
  document.addEventListener('permanentcolorscheme', (e) => {
    console.log(`${e.detail.permanent ? 'R' : 'Not r'
        }emembering the last selected mode.`);
  });
```

## Style Customization

See the demo source code for some concrete examples.

| CSS Variable Name | Default | Description |
| ----------------- | ------- | ----------- |
| `--dark-mode-toggle-light-icon` | No icon | The icon for the light state in `background-image:` notation. |
| `--dark-mode-toggle-dark-icon` | No icon | The icon for the dark state in `background-image:` notation. |
| `--dark-mode-toggle-remember-icon-checked` | No icon | The icon for the checked "remember the last selected mode" functionality in `background-image:` notation. |
| `--dark-mode-toggle-remember-icon-unchecked` | No icon | The icon for the unchecked "remember the last selected mode" functionality in `background-image:` notation. |
| `--dark-mode-toggle-color` | User-Agent stylesheet text color | The main text color in `color:` notation. |
| `--dark-mode-toggle-background-color` | User-Agent stylesheet background color | The main background color in `background-color:` notation. |
| `--dark-mode-toggle-legend-font` | User-Agent `<legend>` font | The font of the legend in shorthand `font:` notation. |
| `--dark-mode-toggle-label-font` | User-Agent `<label>` font | The font of the labels in shorthand `font:` notation. |
| `--dark-mode-toggle-remember-font` | User-Agent `<label>` font | The font of the "remember the last selected mode" functionality label in shorthand `font:` notation. |
| `--dark-mode-toggle-icon-filter` | No filter | The filter for the dark icon (so you can use all black or all white icons and just invert one of them) in `filter:` notation. |
| `--dark-mode-toggle-remember-filter` | No filter | The filter for the "remember the last selected mode" functionality icon (so you can use all black or all white icons and just invert one of them) in `filter:` notation. |
| `--dark-mode-toggle-active-mode-background-color` | No background color | The background color for the currently active mode in `background-color:` notation. |

## Notes

This is not an official Google product.

## License

Copyright 2019 Google LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
