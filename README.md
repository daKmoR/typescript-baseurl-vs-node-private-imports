# Typescript BaseUrl vs Node Private imports

We have 3 files:

👉 `control.js`

basically to show that it actually works. Using the "cumbersome" long file path.

```js
import { one } from "../../src/one.js";

console.log(one);
```

👉 `baseUrl.js`

we now use the `baseUrl` typescript compilerOptions and import with it

```js
import { one } from "one.js";

console.log(one);
```

👉 `importMap.js`

we now use a private node import we defined in the package.json

```js
import { one } from "#one";

console.log(one);
```

We now execute/bundle those files with various tools and see the output.

## Results

| File         |  TSC   | TSC@next | Node | Webpack | Rollup |
| :----------- | :----: | :------: | :--: | :-----: | :----: |
| control.js   |   ✅   |    ✅    |  ✅  |   ✅    |   ✅   |
| baseUrl.js   |   ✅   |    ✅    |  ❌  |   ❌    |   ❌   |
| importMap.js | ⚠️ [1] |    ✅    |  ✅  |   ✅    | ✅ [2] |

[1]: typescript < 4.6 will not get the type info from an import map <br>
[2]: Requires the `@rollup/plugin-node-resolve` plugin

## Run it yourself

```bash
npm run tsc
npm run tsc:base
npm run tsc:map
npm run node
npm run node:base
npm run node:map
npm run rollup
npm run rollup:base
npm run rollup:map
npm run webpack
npm run webpack:base
npm run webpack:map
```
