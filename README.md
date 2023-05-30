# opentelemetry-babel-require-in-the-middle-repro
Reproduction repo for https://github.com/elastic/require-in-the-middle/issues/72

Run `dev` script to see the following error:

```
<path_to_repo>\node_modules\@babel\core\lib\parser\index.js:74
    throw err;
    ^

AssertionError [ERR_ASSERTION]: unexpected that there is no Module entry for "<path_to_repo>\node_modules\@babel\parser\lib\index.js" in require.cache
    at ExportsCache.set (<path_to_repo>\node_modules\require-in-the-middle\index.js:89:7)
    at Module.Hook._require.Module.require (<path_to_repo>\node_modules\require-in-the-middle\index.js:249:17)
    at require (node:internal/modules/cjs/helpers:103:18)
    at parse (<path_to_repo>\node_modules\@babel\core\src\parser\index.ts:2:1)
    at parser (<path_to_repo>\node_modules\@babel\core\src\parser\index.ts:28:14)
    at parser.next (<anonymous>)
    ...
```

There's a workaround for this issue as suggested by [this comment](https://github.com/elastic/require-in-the-middle/issues/72#issuecomment-1568715875) by defining `BABEL_DISABLE_CACHE=1`. This fix can be tested with the `dev:fix` script in this repo.

Tested with Node.js v18.13.0.
