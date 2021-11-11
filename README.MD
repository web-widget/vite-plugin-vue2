# vite-plugin-vue2

[![NPM version](https://img.shields.io/npm/v/vite-plugin-vue2?color=a1b858&label=)](https://www.npmjs.com/package/vite-plugin-vue2)

## Install

```bash
npm install vite-plugin-vue2 -D
```

```js
// vite.config.js
import { createVuePlugin } from 'vite-plugin-vue2'

export default {
  plugins: [
    createVuePlugin(/* options */)
  ],
}
```

## [Options](https://github.com/underfin/vite-plugin-vue2/blob/master/src/index.ts#L26)

### `vueTemplateOptions`

Type: `Object`<br>

Default: `{ compilerOptions :{ whitespace: 'condense' }   }`

**Note {  whitespace: 'condense' } behavior**

* A whitespace-only text node between element tags is removed if it contains new lines. Otherwise, it is condensed into a single space.

* Consecutive whitespaces inside a non-whitespace-only text node are condensed into a single space.


Using condense mode will result in smaller compiled code size and slightly improved performance. However, it will produce minor visual layout differences compared to plain HTML in certain cases,if you want to keep whitespace  behavior, please set `{ whitespace: 'preserve' }`

The options for `@vue/component-compiler-utils`.

### `jsx`

Type: `Boolean`<br>
Default: `false`

The options for jsx transform.

### `jsxOptions`

Type: `Object`<br>

The options for `@vue/babel-preset-jsx`.

### `target`

Type: `String`<br>

The options for esbuild to transform script code

### `customElement`

Type: `boolean | string | RegExp | (string | RegExp)[]`<br>

Transform Vue SFCs into custom elements

## Using Vue SFCs as Custom Elements

```js
import Example from './Example.vue'

console.log(Example.styles) // ['/* css content */']

// register
customElements.define('my-example', defineCustomElement(Example))
```

Note in custom elements mode there is no need to use `<style scoped>` since the CSS is already scoped inside the shadow DOM.

The `customElement` plugin option can be used to configure the behavior:

- `{ customElement: true }` will import all `*.vue` files in custom element mode.
- Use a string or regex pattern to change how files should be loaded as Custom Elements (this check is applied after `include` and `exclude` matches).

## Todo

- SSR Build
- Sourcemap
