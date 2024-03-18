---
layout: mainLayout
---

<script>
  import { Banner } from 'flowbite-svelte';
</script>

<Banner id="default-banner" dismissable={false} classDiv='p-2'>
  <p class="flex items-center gap-4 text-lg font-normal text-gray-900 dark:text-gray-100">
      To Keep It Going, Please Show Your Love.<a href='https://ko-fi.com/Z8Z2CHALG' target='_blank'><img height='42' style='border:0px;height:42px;' src='https://storage.ko-fi.com/cdn/kofi3.png?v=3' alt='Buy Me a Coffee at ko-fi.com' /></a>
  </p>
</Banner>

# Svelte Feathers

<div class="flex gap-2 my-8">
<a href="https://github.com/sponsors/shinokada" target="_blank"><img src="https://img.shields.io/static/v1?label=Sponsor&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86" alt="sponsor"></a>
<a href="https://www.npmjs.com/package/svelte-feathers" rel="nofollow" target="_blank"><img src="https://img.shields.io/npm/v/svelte-feathers" alt="npm"></a>
<a href="https://twitter.com/shinokada" rel="nofollow" target="_blank"><img src="https://img.shields.io/badge/created%20by-@shinokada-4BBAAB.svg" alt="Created by Shin Okada"></a>
<a href="https://opensource.org/licenses/MIT" rel="nofollow" target="_blank"><img src="https://img.shields.io/github/license/shinokada/svelte-feathers" alt="License"></a>
<a href="https://www.npmjs.com/package/svelte-feathers" rel="nofollow" target="_blank"><img src="https://img.shields.io/npm/dw/svelte-feathers.svg" alt="npm"></a>
</div>

280+ Svelte-Feathers icon components for Svelte. It is a collection of simply beautiful open source icons for Sveltejs. Each icon is designed on a 24x24 grid with an emphasis on simplicity, consistency and readability.

Thank you for considering my open-source package. If you use it in a commercial project, please support me by sponsoring me on GitHub: https://github.com/sponsors/shinokada. Your support helps me maintain and improve this package for the benefit of the community.

## Installation

```sh
pnpm i -D svelte-feathers
```

## Repo

[GitHub Repo](https://github.com/shinokada/svelte-feathers)

## Usage

```html
<script>
  import { ActivityIcon, AirplayIcon } from 'svelte-feathers';
</script>

<ActivityIcon color="#c61515" size="12" />

<AirplayIcon color="#23deff" size="36" />
```

## Faster compiling

If you need only a few icons from this library in your Svelte app, import them directly. This can optimize compilation speed and improve performance by reducing the amount of code processed during compilation.

```html
<script>
  import ActivityIcon from 'svelte-feathers/ActivityIcon.svelte';
</script>

<ActivityIcon />
```

## Props

- size = ctx.size || '24';
- withEvents: boolean = false;
- role = ctx.role || 'img';
- color = ctx.color || 'currentColor';
- ariaLabel = 'file name';

## IDE support

If you are using an LSP-compatible editor, such as VSCode, Atom, Sublime Text, or Neovim, hovering over a component name will display a documentation link, props, and events.

## Size

Use the size prop to change the size of icons.

```html
<UnlockIcon size="24" />
```

If you are using Tailwind CSS, you can add a custom size using Tailwind CSS by including the desired classes in the class prop. For example:

```html
<UnlockIcon class="shrink-0 h-20 w-20" />
```

## Setting Global Icon using setContext

You can establish global icon preferences in your Svelte application using `setContext`. This allows you to configure icon-related properties once and share them across multiple components. Here's how you can do it:

```html
<script>
  import { setContext } from 'svelte';

  // Define your global icon settings
  const iconCtx = {
    size: '100', // Icon size in pixels
    color: '#ff4488', // Icon color in hexadecimal or CSS color name
    role: 'svg icon image' // Accessible role for the icon
  };
  setContext('iconCtx', iconCtx);
</script>
```

The `size`, `color`, and `role` properties are optional, allowing you to fine-tune the appearance and accessibility of your icons as needed.

If you set `size`, icons can be customized with different colors. For example:

```html
<script>
  import { setContext } from 'svelte';
  import { UnlockIcon } from 'svelte-feathers';
  const iconCtx = {
    size: '50'
  };
  setContext('iconCtx', iconCtx);
</script>

<UnlockIcon color="#ff4488" />
```

Remember that you can set only one or two of these properties, allowing you to tailor icon settings to your specific design and accessibility requirements.

Feel free to mix and match these properties as needed to create visually appealing and accessible icons in your Svelte application.

## Creating a Default Icon Setting

You can create a config file, `/src/lib/icon.config.json`.

The `Icon` component serves as a wrapper for svelte:component, allowing you to establish a global default setting or expand the capabilities of a component.

To create a default global icon setting, follow these steps:

### Configuration File

Start by creating a configuration file named `/src/lib/icon.config.json` with the following structure:

```json
{
  "config1": {
    "size": 40,
    "color": "#FF5733"
  },
  "config2": {
    "size": 50,
    "color": "#445533"
  }
}
```

In this JSON file, you can define different configurations (config1 and config2 in this case) for your icons, specifying attributes like size, variation, and color.

### Implementation

In your Svelte page file, make use of the configurations from the JSON file:

```html
<script lang="ts">
  type IconConfig = {
    config1: {
      size: number;
      color: string;
    };
    config2: {
      size: number;
      color: string;
    };
  };
  import config from '$lib/icon.config.json';
  import { Icon, ArrowUp, AlertCircle } from 'svelte-feathers';

  const iconConfig: IconConfig = config;
  const config1 = iconConfig.config1;
  const config2 = iconConfig.config2;
</script>

<Icon {...config1} icon="{ArrowUp}" />
<Icon {...config2} icon="{AlertCircle}" />
```

We import the configurations from the JSON file and assign them to config1 and config2. We then utilize the Icon component with the spread attributes `{...config1}` and `{...config2}` to apply the respective configurations to each icon.

### Custom Default Icon

If you wish to create a custom default icon, you can follow these steps:

Create a Svelte component named `src/lib/MyIcon.svelte`:

```html
<script lang="ts">
  import type { ComponentType } from 'svelte';
  const config = {
    size: 30,
    color: '#FF5733'
  };
  import { Icon } from 'svelte-feathers';
  export let icon: ComponentType;
</script>

<Icon {...config} {icon} />
```

This component, `MyIcon.svelte`, accepts an `icon` prop which you can use to pass in the specific icon component you want to display. The default configuration is also applied to the icon.

### Implementation in a Page

To use your custom default icon in a Svelte page, do the following:

```html
<script>
  import MyIcon from '$lib/MyIcon.svelte';
  import { ArrowUp } from 'svelte-feathers';
</script>

<MyIcon icon="{ArrowUp}" />
```

Here, we import the `MyIcon` component and the `ArrowUp` icon. By passing the `ArrowUp` icon to the `icon` prop of MyIcon, you apply the default configuration to the icon.

## CSS HEX Colors

Use the color prop to change colors with HEX color code.

```html
<UnlockIcon color="#6dff6b" />
```

## CSS frameworks support

You can apply CSS framework color and other attributes directly to the icon component or its parent tag using the class prop.

Tailwind CSS example:

```html
<UnlockIcon class="h-24 w-24 text-blue-700 mr-4" />
```

Bootstrap example:

```html
<UnlockIcon class="position-absolute top-0 px-1" />
```

Dark mode with Tailwind CSS
If you are using the dark mode on your website with Tailwind CSS, add your dark mode class to the class prop.

Let’s use dark for the dark mode class as an example.

```html
<script>
  import { UnlockIcon } from 'svelte-feathers';
</script>

<UnlockIcon class="text-blue-700 dark:text-red-500" />
```

## Focusable icon

Icons are unfocuable as the defalut.
If you want to make an icon focusable, add `tabindex="0"`.

```html
<UnlockIcon tabindex="0" />
```

## Event

All icons have the `withEvents` props. Use it if you want to add the following events:

- on:click
- on:keydown
- on:keyup
- on:focus
- on:blur
- on:mouseenter
- on:mouseleave
- on:mouseover
- on:mouseout

## Passing down other attributes

You can pass other attibutes as well.

```html
<UnlockIcon tabindex="0" />
```

## Using svelte:component

```html
<script>
  import { UnlockIcon } from 'svelte-feathers';
</script>

<svelte:component this="{UnlockIcon}" />
```

## Using onMount

```html
<script>
  import { UnlockIcon } from 'svelte-feathers';
  import { onMount } from 'svelte';
  const props = {
    size: '50',
    color: '#ff0000'
  };
  onMount(() => {
    const icon = new UnlockIcon({ target: document.body, props });
  });
</script>
```

## Import all

You can also include the whole icon pack:

```html
<script>
  import * as Icon from 'svelte-feathers';
</script>

<UnlockIcon color="#6dff6b" size="24" />
```

## Original source

[feathericons/feather](https://github.com/feathericons/feather)

## License

[Svelte-Feathers License](https://github.com/shinokada/svelte-feathers/LICENSE)

[feathericons/feather License](https://github.com/feathericons/feather/blob/master/LICENSE)

## Other icons

[Svelte-Icon-Sets](https://svelte-svg-icons.codewithshin.com/)
