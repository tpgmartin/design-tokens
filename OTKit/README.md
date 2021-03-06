# OTKit tokens

## Available tokens

| Token | Available Formats | Version |
|--------|-------|-------|
| [`otkit-breakpoints`](/OTKit/otkit-breakpoints) | [`scss`, `cssmodules.css`, `common.js`] | [![npm version](https://badge.fury.io/js/otkit-breakpoints.svg)](http://badge.fury.io/js/otkit-breakpoints) |
| [`otkit-colors`](/OTKit/otkit-colors) | [`scss`, `cssmodules.css`, `common.js`] | [![npm version](https://badge.fury.io/js/otkit-colors.svg)](http://badge.fury.io/js/otkit-colors) |
| [`otkit-spacing`](/OTKit/otkit-spacing) | [`scss`, `cssmodules.css`, `common.js`] | [![npm version](https://badge.fury.io/js/otkit-spacing.svg)](http://badge.fury.io/js/otkit-spacing) |
| [`otkit-typography`](/OTKit/otkit-typography) | [`scss`, `cssmodules.css`, `common.js`] | [![npm version](https://badge.fury.io/js/otkit-typography.svg)](http://badge.fury.io/js/otkit-typography) |

***

## Usage

### Install the token

```bash
$ npm install --save-dev <token-name>
```

### Use the token

A Token exposes multiple available formats (listed above). **The format need to be excplicitely referenced upon requiring/importing the token:**

```
require('<token-name>/token.<format>')
```

Examples
```
// cssmodules example:
@value color-primary from 'otkit-colors/token.cssmodules.css';

// common.js require/import examples:
const color = require('otkit-colors/token.common.js');
import color from 'otkit-colors/token.common.js';

// scss example:
@import '../node_modules/ottheme-colors/token.scss';
```

### Preview and debug

Executing `npm run build` will generate the token values in each token's folder, such as `token.scss` or other available formats you specified.

When you publish a token, this step is executed as part of the publishing.

If you are using a token in your project, you can execute `npm link '<token-name>'` in `node_modules` folder to test the token values before publishing.

***

### Publish

A token needs to be published in order for the changes to take effect. To publish a token, navigate to the token's directory, for example `./OTKit/otkit-colors/`, then run `npm publish otkit-colors`.

You need to have an NPM account and be among the "Collaborators" list on the official NPM package page, for example  `https://www.npmjs.com/package/otkit-colors`, to publish. Contact one of the collaborators if you would like to be added.

Note: if you are a developer of OpenTable organization, remember to remove the OpenTable credentials from your `~/.npmrc` file to make sure you are publishing to the public instead of a private registry.



## Contributing a new value

All OTKit design system values are aliased and contained within the [OTKit/aliases.yml](/aliases/yml) file. This file represents the single source of truth for the OTKit design system. The values in aliases.yml are referenced within each token for build purposes.

### I need to add a new value, where do I add it?

1. In the [OTKit/aliases.yml](/aliases/yml) file, add the value and a unique name for it. Follow the existing conventions as much as possible (place it in the right area, if it one exists, and add a helpful comment about how the value is used). 

For example, to add a value named "color-gray-primary", which is used as the text color, you should add the section seen in between the ellipses (...) below:

```yml
aliases:
  ...
  # Primary Gray, used on all text sizes
  # =============================================
  color-gray-primary:
    value: "#333333"
  ...
```
2. Find the directory containing the tokens that are relevant to your new value (otkit-typography for typography, otkit-colors for colors, etc.). Within that directory, find the token.yml file and add the new value in the props section. For example, we would add the color-gray-primary value in otkit-colors/token.yml in the following way:

```yml
props:
  ...
  color-gray-primary:
    value: "!{color-gray-primary}"
  ...  
```
3. Add, commit, and push your changes. Make a PR on `https://github.com/opentable/design-tokens`. Pat yourself on the back as you wait for your PR to be reviewed.

### I need to add a new format, how do I add it?

1. Edit the related build system in the project root scripts (within the `package.json` file). Check the [theo](https://github.com/salesforce-ux/theo#available-formats) and [theo-cli](https://github.com/salesforce-ux/theo/blob/master/CLI.md) documentation for more information.

```json
...
"scripts": {
  ...
  "build-otkit": "lerna exec --scope otkit-* theo cssmodules.css NEWFORMAT",
  ...
}
...
```
