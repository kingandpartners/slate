# Slate is Dead, Long Live Slate (April 2021)

This repo fork is solely intended to support legacy projects already using Slate, since Slate itself is deprecated by Shopify (See Legacy Info section below).

## Primary Updates

### Upgraded Themekit = Vastly Faster Deploys

To take advantage of file checksums, so only changed files are uploaded/downloaded on deploy/start etc

### Removed analytics calls from CLI commands

To avoid axios errors clogging the logs

## Installation

Releases will be accessible only from tarballs on the [release page](https://github.com/kingandpartners/slate/releases/)

Go to the release page for the latest release and note the individual packages attached to the release.

Copy the links to each of the tarballs (.tgz files) and then install as normal via URL.

Since we're not changing the Shopify namespace and we're installing the updated packages from outside the NPM registry, we have to install each updated package individually.
```
npm i --save-dev [package url] [package url]

 e.g.
npm i --save-dev https://github.com/kingandpartners/slate/releases/download/v1.0.1/shopify-slate-sync-1.0.1.tgz https://github.com/kingandpartners/slate/releases/download/v1.0.1/shopify-slate-tools-1.0.1.tgz

...
```

The resulting package.json will look like
```
...

  "devDependencies": {
    "@shopify/slate-sync": "https://github.com/kingandpartners/slate/releases/download/v1.0.1-beta.0/slate-sync-1.0.1-beta.0.tgz",
    "@shopify/slate-tools": "https://github.com/kingandpartners/slate/releases/download/v1.0.1-beta.0/slate-tools-1.0.1-beta.0.tgz",

    ...
```

## Usage Notes
- Due to the way Themekit is calculating checksums, you'll note that certain files are always uploaded despite no obvious changes (e.g. `locales/en.default.json`)
  - This is because Shopify is minifying the JSON after upload, so the file on Shopify will have a different checksum than our repo version.

## Release creation

### 1. Merge necessary PR's to `develop`

### 2. Create a release PR from `develop` to `master` and merge

### 3. Checkout and pull master

### 4. `npm run release`
This uses Lerna lib to bump all the necessary versions (you'll be prompted to choose the next version) and creates the release tag on the repo releases page.

If necessary bump the version in each package's README.md (e.g. `## Last update (1.0.1-beta.2)`) to force Lerna to change the version for that package.

```
$ npm run release

> slate@ release /Users/johnroyall/slate-mine
> lerna version --exact && git push --follow-tags

lerna notice cli v3.11.0
lerna info current version 1.0.1-beta.1
lerna info Looking for changed packages since v1.0.0-beta.19
? Select a new version (currently 1.0.1-beta.1) Custom Version
? Enter a custom version 1.0.1-beta.2

Changes:
 - @shopify/slate-sync: 1.0.1-beta.1 => 1.0.1-beta.2
 - @shopify/slate-tools: 1.0.1-beta.1 => 1.0.1-beta.2

? Are you sure you want to create these versions? Yes
lerna info execute Skipping GitHub releases
lerna info git Pushing tags...
lerna success version finished
Everything up-to-date
```

### 5. Package the individual tarballs with `npm pack` (for any updated packages)
.eg.
```
$ pwd
/Users/johnroyall/slate-mine
$ cd packages/slate-sync
$ npm pack
npm notice
npm notice 📦  @shopify/slate-sync@1.0.1-beta.1
npm notice === Tarball Contents ===
npm notice 5.3kB index.js
npm notice 115B  slate-sync.schema.js
npm notice 751B  package.json
npm notice === Tarball Details ===
npm notice name:          @shopify/slate-sync
npm notice version:       1.0.1-beta.1
npm notice filename:      shopify-slate-sync-1.0.1-beta.1.tgz
npm notice package size:  2.2 kB
npm notice unpacked size: 6.1 kB
npm notice shasum:        9a8a7d5aca0304141fb1d0ab1039d3800618b763
npm notice integrity:     sha512-gAt2HyJa7NQ6a[...]5m7THw6mMXzzg==
npm notice total files:   3
npm notice
shopify-slate-sync-1.0.1-beta.1.tgz
```

### 6. Attach all the updated packages to the tag
Don't forget to delete the tarballs once done.

### More info
See CONTRIBUTING.MD, but note that most of this is *not* followed

## Dev Setup (tbd)

# Legacy Info - Slate is Deprecated

[![Build Status](https://travis-ci.org/Shopify/slate.svg?branch=master)](https://travis-ci.org/Shopify/slate) [![npm version](https://badge.fury.io/js/%40shopify%2Fslate-tools.svg)](https://badge.fury.io/js/%40shopify%2Fslate-tools)

![slate animated banner](https://user-images.githubusercontent.com/4837696/47506317-cbe22400-d83d-11e8-9867-1dc874943833.gif)

## ⚠ Slate - End of Support (January 2020)

After re-evaluating Slate and its current state, Shopify has decided to officially end support for Slate.

### Why?

With the launch of our new [section theme architecture](https://help.shopify.com/en/themes/development/sections-architecture) we're taking a step back to examine our current tooling and how we can deliver the best theming experience to our theme developers.

Slate is not in line with our vision for themes moving forward and it does not solve two of the larger asks our theme developers have made:

* Local development of a Shopify theme
* Support for code versioning within themes

### I’m a theme developer that is using Slate. What should I do now?

Slate was built upon [Theme Kit](https://github.com/Shopify/themekit) as an opinionated way to setup up a Shopify theme build. Shopify will continue to actively maintain and support the growth of Theme Kit through the open-source community.

You can continue using Slate the way you have been. While we will not be maintaining it any longer, you can still fork the repo to suit your own needs.

<hr />

> **Slate v1.0 is currently in beta.** Expect more bugs than a final release. If you are migrating from using the previous version of Slate, please review the [new documentation](https://shopify.github.io/slate/docs/about) as there are breaking changes. Slate v1.0 has not yet been tested on Windows.
>
> To view the previous version of Slate, visit the [0.x branch](https://github.com/Shopify/slate/tree/0.x).

Slate empowers developers of all skill levels to build quality Shopify themes. Slate guides developers by providing a tested workflow and opinionated development toolkit, while also accommodating more established developers through advanced configuration.

🚀 [Get started with a new Slate project](https://shopify.github.io/slate/docs/system-requirements)

## Documentation

Visit the [official Slate documentation website](https://shopify.github.io/slate/docs/about) for complete documentation Slate's concepts and technical details, as well as helpful guides!

## Contributing

For help on setting up the repo locally, building, testing, and contributing
please see [CONTRIBUTING.md](https://github.com/Shopify/slate/blob/master/CONTRIBUTING.md).

## Code of Conduct

All developers who wish to contribute through code or issues, take a look at the
[Code of Conduct](https://github.com/Shopify/slate/blob/master/CODE_OF_CONDUCT.md).

## License

Copyright (c) 2018 Shopify. See [LICENSE](https://github.com/Shopify/slate/blob/master/LICENSE) for further details.

## Thanks

We would like to specifically thank the following projects, for the inspiration and help in regards to the creation of Slate:

* [create-react-app](https://github.com/facebookincubator/create-react-app)
* [Dynamo's Shopify Pipeline](https://github.com/DynamoMTL/shopify-pipeline)
