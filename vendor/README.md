# vendor/

`supabase-2.117.2-chrome80.js` is `@supabase/supabase-js` 2.117.2 from npm, bundled for Chrome 80 and newer so the
consent page loads on Android 11's stock Chrome 83. esm.sh's build imports a `node/process` polyfill that uses `??=`
(Chrome 85), and jsDelivr's UMD uses `||=` and private methods (Chrome 84/85). See LemonVanilla KNOWN-PITFALLS #796.

Rebuild (same output for the same versions):

```
npm install --ignore-scripts @supabase/supabase-js@2.117.2 esbuild@0.24.2
echo "export { createClient } from '@supabase/supabase-js';" > entry.mjs
npx esbuild entry.mjs --bundle --format=iife --global-name=supabase --target=chrome80 --minify --platform=browser --outfile=supabase-2.117.2-chrome80.js
```

sha256 `b55e635258aca661d1786905586993c7d0be48e2bfca7dd1fb6db06e075d0087`. Both pages (`index.html`, `dev/index.html`) load it with a
classic `<script>` before their module script and read `window.supabase.createClient`.
