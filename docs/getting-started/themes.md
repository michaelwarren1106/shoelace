# Themes

Shoelace ships with a dark theme that complements the default light theme. You can even take things a step further by designing your own custom theme.

The default theme is included as part of `shoelace.css` and should always be loaded first, even if you want to use another theme exclusively. The default theme contains important base tokens and utilities that many components rely on.

## Dark Mode

To install the dark theme, add the following to your page.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@%VERSION%/themes/dark.css">

<body class="sl-theme-dark">
  ...
</body>
```

**Themes must be activated after importing!** You can do this by adding the theme's class name to the element you want the theme to apply to. This is usually `<body>`, but themes can also be applied to container elements, making it possible to use more than one theme on the same page.

```html
<sl-button>Light Mode</sl-button>

<div class="sl-theme-dark">
  <sl-button>Dark Mode</sl-button>
</div>
```

### Detecting the User's Color Scheme Preference

Shoelace doesn't try to auto-detect the user's light/dark mode preference. This should be done at the application level. As a best practice, to provide a dark theme in your app, you should:

- Check for [`prefers-color-scheme`](https://stackoverflow.com/a/57795495/567486) and use its value by default
- Allow the user to override the setting in your app
- Remember the user's preference and restore it on subsequent logins

Shoelace avoids using the `prefers-color-scheme` media query because not all apps support dark mode, and it would break things for the ones that don't.

## Creating a Theme

A theme is nothing more than a stylesheet that uses the Shoelace API to customize design tokens and/or components. To create a theme, you will need a decent understanding of CSS, including [CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*) and the [`::part` selector](https://developer.mozilla.org/en-US/docs/Web/CSS/::part).

The recommended way to create a theme is to piggyback on top of the default theme, adjusting design tokens and styling components as necessary to achieve the look you want. This makes your theme lightweight and "future proof", as later versions of Shoelace may introduce new components that your theme won't support. The default theme will account for these so components won't appear to be broken.

Technically, you can roll your own theme from scratch without using the default theme as a baseline, but that approach isn't recommended.

### Theme Classes

All theme classes should use the `sl-theme-name` convention, where `name` is a lowercase, hyphen-delimited value representing the name of your theme. For example, a theme called "Purple Power" would use the `sl-theme-purple-power` class.

Every selector in a theme must be scoped to the theme's class to ensure interoperability with other themes.

### Design Tokens

[Design tokens](http://localhost:4000/#/getting-started/customizing?id=design-tokens) give you a high-level way to customize Shoelace components. You can customize them in your theme as shown below.

```css
.sl-theme-purple-power { 
  --sl-color-primary-hue: 290;
  --sl-color-primary-saturation: 80%;

  /* more design token customizations here */
}
```

?> Avoid scoping design tokens to `:root`. The default theme does this to provide base styles that will apply to the page even when no `sl-theme-` class is applied.

### Components

To customize individual components, use the following syntax.

```css
.sl-theme-purple-power sl-button::part(base) {
  /* your custom button styles here */
}
```

?> Pay special attention to each component's CSS Parts API. You usually need to use a `::part` selector when targeting components!

## Using a Custom Theme

If a theme adheres to the guidelines above, you can use it by importing the stylesheet and activating it with the theme's class name.

```html
<head>
  ...
  <link rel="stylesheet" href="path/to/purple-power.css">
</head>

<body class="sl-theme-purple-power">
  ...
</body>
```

In fact, you can apply a theme's class to any container on the page, not just the body. This lets you use more than one theme on the same page.

## Submitting a Theme

**I am very interested in showcasing well-designed themes that complement this library.** To submit a theme for review, please [open an issue](https://github.com/shoelace-style/shoelace/issues/new) on GitHub with the theme linked or attached. Once approved, your theme will be showcased on this page.

Please note the following requirements before submitting a theme.

- Themes must be complete and of high quality
- Themes must be available under an open source license
- Derivative works must be properly credited