<h1>Link</h1>

[![CI/CD Status][github-action-badge]][github-action-link] [![Codecov][codecov-badge]][codecov-project] [![MIT License][license-image]][license-url]  
[![NPM version][npm-version-image]][npm-package] [![Library size][file-size-badge]][raw-distribution-js]

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Installation](#installation)
  - [Packages that need to be installed](#packages-that-need-to-be-installed)
  - [Modules that need to be in NgModule](#modules-that-need-to-be-in-ngmodule)
  - [CSS imports](#css-imports)
  - [CSS resources](#css-resources)
- [Usage](#usage)
  - [External links](#external-links)
  - [Tab index](#tab-index)
  - [Local URL fragments](#local-url-fragments)
    - [Router changes to support local links](#router-changes-to-support-local-links)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Installation

### Packages that need to be installed

- `@angular/material`
- `@terminus/design-tokens`
- `@terminus/fe-utilities`
- `@terminus/ui-link`
- `@terminus/ui-styles`
- `@terminus/ui-utilities`

Use the `ng add` command to quickly install all the needed dependencies:

```bash
ng add @terminus/ui-link
```

### Modules that need to be in NgModule

- `TsLinkModule`
- `RouterModule.forRoot(MY_ROUTES)`

### CSS imports

In your top level stylesheet, add these imports:

```css
@import '~@terminus/design-tokens/css/library-design-tokens.css';
@import '~@terminus/ui-styles/terminus-ui.css';
```  

### CSS resources

Load the needed font families by adding this link to the `<head>` of your application:

```css
<link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,500;0,700;1,400&display=swap" rel="stylesheet">
```

## Usage

Wrap your link text and define a destination:

```html
<ts-link [destination]="['your', 'path']">My link</ts-link>
```

### External links

To signify a link will leave the current app or site, set `external` to true.
When the destination is a string and contains either `mailto` or `tel`, the external icon would not show.

```html
<ts-link
  [destination]="http://google.com"
  [external]="true"
>My link</ts-link>
```

> NOTE: When external is set to true, the link should be a standard link in string form.

### Tab index

A custom tabindex can also be set:

```html
<ts-link
  [destination]="http://google.com"
  [tabIndex]="2"
>My link</ts-link>
```

### Local URL fragments

Local fragments are supported for deep linking within a page:

```html
<ts-link
  [destination]="['your', 'path']"
  fragment="myFragment"
  [tabIndex]="2"
>My link</ts-link>
<!-- This would route to: `/your/path#myFragment -->
```

If no destination is defined, it will fallback to the local page: `['.']`:

```html
<ts-link
  fragment="myFragment"
  [tabIndex]="2"
>My link</ts-link>
<!-- If used on the route `/my/home`, this would route to: `/my/home#myFragment` -->
```

#### Router changes to support local links

There are a couple needed Router configuration changes to support local links:

```typescript
import { NgModule } from '@angular/core';
import {
  ExtraOptions,
  RouterModule,
  Routes,
} from '@angular/router';

const myRoutes: Routes = [...];
const routerOptions: ExtraOptions = {
  anchorScrolling: 'enabled',
  scrollPositionRestoration: 'enabled',
};

@NgModule({
  ...
  imports: [RouterModule.forRoot(myRoutes, routerOptions)],
  ...
})
```

> Learn more about Angular's `ExtraOptions` here: <https://angular.io/api/router/ExtraOptions>

<!-- Links -->
[license-url]:         https://github.com/GetTerminus/terminus-oss/blob/release/LICENSE
[license-image]:       http://img.shields.io/badge/license-MIT-blue.svg
[codecov-project]:     https://codecov.io/gh/GetTerminus/terminus-oss
[codecov-badge]:       https://codecov.io/gh/GetTerminus/terminus-oss/branch/release/graph/badge.svg
[npm-version-image]:   http://img.shields.io/npm/v/@terminus/ui-link.svg
[npm-package]:         https://www.npmjs.com/package/@terminus/ui-link
[github-action-badge]: https://github.com/GetTerminus/terminus-oss/workflows/Release%20CI/badge.svg
[github-action-link]:  https://github.com/GetTerminus/terminus-oss/actions?query=workflow%3A%22CI+Release%22
[file-size-badge]:     http://img.badgesize.io/https://unpkg.com/@terminus/ui-link/bundles/terminus-ui-link.umd.min.js?compression=gzip
[raw-distribution-js]: https://unpkg.com/@terminus/ui-link/bundles/terminus-ui-link.umd.js
