# tsconfig-config

`@ycookiey/tsconfig` — a shared strict [TypeScript config](https://www.typescriptlang.org/tsconfig/) for apps that a bundler builds. `tsc` checks the types and emits nothing; the bundler emits the JavaScript.

## Install

```sh
npm install --save-dev @ycookiey/tsconfig typescript
```

Works with TypeScript 5.9, 6.0 and 7.0.

## Usage

`tsconfig.json`:

```json
{
  "extends": "@ycookiey/tsconfig/base.json",
  "compilerOptions": {
    "baseUrl": null,
    "paths": { "@/*": ["./src/*"] }
  },
  "include": ["src"]
}
```

Write `include`, and `paths` if you use path aliases, in your own `tsconfig.json`. TypeScript resolves the `include`, `baseUrl` and `paths` of an extended config from the folder of that config, here `node_modules/@ycookiey/tsconfig`, so with `extends` alone it finds no input files. `"baseUrl": null` removes the `baseUrl` of this config, which TypeScript 6.0 reports as a deprecation error and TypeScript 7.0 rejects.

The config turns on `strict` and checks for unused variables and parameters, switch fallthrough and implicit returns, resolves modules as a bundler does (`moduleResolution: "Bundler"`), and targets `ESNext` with the DOM types. See [`base.json`](base.json) for every option.

To have `tsc` emit JavaScript, set `"noEmit": false` together with `"allowImportingTsExtensions": false`, as TypeScript allows importing `.ts` extensions only when it emits nothing. With an `outDir`, TypeScript 6.0 and later also ask for `rootDir` when the sources are in a subfolder such as `src`.

## License

[MIT](LICENSE)
