## `myitcv/ts_react_node_types_repro`

```
git clone https://github.com/myitcv/ts_react_node_types_repro
cd ts_react_node_types_repro
npm install
./node_modules/.bin/jspm install
```

Then in a new terminal:

```
./node_modules/.bin/tsc -w
```

Notice this compiles without any errors. This is _not_ expected because `React` has not been imported.

Now in another terminal:

```
./node_modules/.bin/http-server -c-1 -a localhost -p 8080
```

and browse to http://localhost:8080; observe the error in the console.

So at this point we have TypeScript code that compiles but that fails at runtime. This is _not_ expected or
desirable.

Now uncomment the `import` at the top of `src/index.ts` and save. Notice this also compiles without errors; this is as
expected because we are correctly importing `React`. Reload in the browser and observe there is now no error in the
console (instead the function is logged); this is as expected.

Now switch your attention to `node_modules/@types/react/index.d.ts` and comment out the line:

```
export as namespace React;
```

Comment out the `import` in `src/index.ts` (effectively returning the file to its initial state) and observe
you now get compile errors as expected:

```
src/index.ts(3,13): error TS2304: Cannot find name 'React'.
src/index.ts(6,12): error TS2304: Cannot find name 'React'.
```
