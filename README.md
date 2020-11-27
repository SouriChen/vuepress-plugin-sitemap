# vuepress-plugin-sitemap-tranhom

Sitemap generator plugin for vuepress.

## Install

- Yarn

  ```sh
  yarn add vuepress-plugin-sitemap-tranhom --registry=http://npm.inner.tranhom.com
  ```

- NPM

  ```sh
  npm install vuepress-plugin-sitemap-tranhom --registry=http://npm.inner.tranhom.com
  ```

> in v2.0.0, dependencies except `sitemap` are moved to peerDependencies so we need to install `esm` module manually (`chalk` and `commander` are already installed by `vuepress`) when we use this plugin with _cli method_.

## Usage

### Vuepress v1.x

```js
// .vuepress/config.js
module.exports = {
  plugins: {
    sitemap: {
      hostname: "https://pake.web.id"
    }
  }
}
```

### Vuepress v0.x

There's no plugin supported with Vuepress v0.x so we need to run it after the build process manually (or with npm `postbuild` script).

1. Manual

   ```sh
   ./node_modules/.bin/vuepress -d "dist"
   ./node_modules/.bin/vuepress-sitemap-tarnhom -H "https://pake.web.id" -d "dist"
   ```

2. NPM Script

   ```ts
   {
     scripts: {
       build: "vuepress build docs -d dist",
       postbuild: "vuepress-sitemap-tarnhom -H https://pake.web.id -d dist"
     }
   }
   ```

## Options

```yml
hostname:
  type: string
  required: true
  default: null
  description: website root url
  example: https://pake.web.id

outFile:
  type: string
  required: false
  default: sitemap.xml
  description: sitemap file name
  example: sitemap.txt

urls:
  type: array
  required: false
  default: [],
  description: custom urls to append
  example: [
    { url: '/place', changefreq: 'monthly' }
  ]

exclude:
  type: array
  required: false
  default: [],
  description: pages path to exclude
  example: ['/404.html']

dateFormatter:
  type: function
  required: false
  description: change the date format
  default: time => new Date(time).toISOString()
```

## Frontmatter Options

To override global option for a specific page, we can use `sitemap` key on the frontmatter,
currently we just have 2 options, they are `exclude` and `changefreq` and `priority`.

### Example

```yml
---
sitemap:
  exclude: false
  changefreq: hourly
  priority: 1.0
---
# Content Updated Frequently
```

**Note:**
Other options of [sitemap](https://npm.im/sitemap) can be used, all options passed except `urls`, `hostname`, `cacheTime`, `xslUrl`, `xmlNs` and `outFile` will be passed to `sitemap.createSitemap` constructor.


