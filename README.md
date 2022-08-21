# Not exporting types in esm

## Desc

- Rollup Plugin Name: @rollup/pluginutils
- Rollup Plugin Version: 4.2.1
- Rollup Version: 2.77.3
- Operating System (or Browser): macOS 12.5.1
- Node Version: v18.7.0

## Reproduction

```bash
npm run build

test.ts:1:31 - error TS7016: Could not find a declaration file for module '@rollup/pluginutils'. '/Users/ding/Projects/rollup-esm-issue/node_modules/@rollup/pluginutils/dist/es/index.js' implicitly has an 'any' type.
  Try `npm i --save-dev @types/rollup__pluginutils` if it exists or add a new declaration (.d.ts) file containing `declare module '@rollup/pluginutils';`

1 import { normalizePath } from "@rollup/pluginutils"
```

But when I changed `moduleResolution` to `node`, it worked fine.

## Solution

Add `exports.types` to `package.json` could fix it.


```
diff --git a/package.json b/package.json
index 6c9a2851e043cb86d15ad234d2aea5bbff319f81..68ef585105c1ba97dcd1367e5d219906069a1b30 100644
--- a/package.json
+++ b/package.json
@@ -20,7 +20,8 @@
   "type": "commonjs",
   "exports": {
     "require": "./dist/cjs/index.js",
-    "import": "./dist/es/index.js"
+    "import": "./dist/es/index.js",
+    "types": "./types/index.d.ts"
   },
   "engines": {
     "node": ">= 8.0.0"

```