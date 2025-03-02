---
title: Getting Started | Workbox
---

# Getting Started

**Workbox** is a huge package with a lot of modules to just make service worker development not to be a hassle and avoid 
dealing with low level service worker api.

In this document we focus only on 
[workbox-build](https://developers.google.com/web/tools/workbox/reference-docs/latest/module-workbox-build) <outbound-link /> 
module from **Workbox**.

## workbox-build module

This module is for build process purpose (it is a `node` module), that is, `Vite Plugin PWA` will use it to build your 
service worker.

We focus on 2 methods of this module:

<ul aria-labelledby="workbox-build-module">
<md-list-anchor href="/workbox/generate-sw.html">
  <template #link>generateSW</template>
  <template #trailing>: for generating the service worker.</template>
</md-list-anchor>
<md-list-anchor href="/workbox/inject-manifest.html">
  <template #link>injectManifest</template>
  <template #trailing>: to build your own service worker.</template>
</md-list-anchor>
</ul>

You must read [Which Mode to Use](https://developers.google.com/web/tools/workbox/modules/workbox-build#which_mode_to_use) <outbound-link />
before decide what strategy to use.

`generateSW` method will abstract you from using service worker api when building the service worker. 
This method can be configured using plugins instead writing your own service worker code (`generateSW` will generate 
the code for you).

`injectManifest` method will get your custom service worker and build/compile it.

## How is `workbox-build` related to `vite-plugin-pwa`?

`vite-plugin-pwa` will use internally `generateSW` and `injectManifest` `workbox` methods when `strategies` 
option is `generateSW` and `injectManifest` respectively.

When you configure `strategies: 'generateSW'` option (it is the default value) on your `vite.config.ts` file, then the 
plugin invoke the workbox `generateSW` method: the options passed to the `workbox-build` method will be the provided on 
`workbox` option of the plugin configuration.

When you configure `strategies: 'injectManifest'` plugin option on your `vite.config.ts` file, the plugin will first 
build your custom service worker via `rollup` and then, with previous build result will call to workbox `injectManifest` 
method: the options passed to the `workbox-build` method will be the provided on `injectManifest` option of the plugin configuration.
