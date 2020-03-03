# stylus-bundle

Bundles all SCSS imports into a single file recursively. This is a fork of [scss-bundle](https://github.com/reactway/scss-bundle) which now only supports non-cli usage. Any help appreciated.

[![NPM version](https://img.shields.io/npm/v/stylus-bundle.svg?logo=npm)](https://www.npmjs.com/package/stylus-bundle)

[![Total downloads](https://img.shields.io/npm/dt/stylus-bundle.svg)](https://www.npmjs.com/package/stylus-bundle)

[![Dependencies](https://img.shields.io/david/ledzz/tiny-emitter.svg)](https://david-dm.org/ledzz/stylus-bundle)

[![Dev dependencies](https://img.shields.io/david/dev/ledzz/tiny-emitter.svg)](https://david-dm.org/ledzz/stylus-bundle?type=dev)

## Non-CLI usage
This package now supports only non-CLI usage.

### Simple example

```typescript
import path from "path";
import { Bundler } from "stylus-bundle";

(async () => {
    // Absolute project directory path.
    const projectDirectory = path.resolve(__dirname, "./cases/tilde-import");
    const bundler = new Bundler(undefined, projectDirectory);
    // Relative file path to project directory path.
    const result = await bundler.bundle("./main.styl");
})();
```

# API

## Bundler

```typescript
import { Bundler } from "stylus-bundle";
```

### Constructor

```ts
constructor(fileRegistry: FileRegistry = {}, projectDirectory?: string) {}
```

##### Arguments

-   `fileRegistry?:` [Registry](#registry) - Dictionary of files contents by full path
-   `projectDirectory?: string` - Absolute project location, where `node_modules` are located. Used for resolving tilde imports

### Methods

#### bundle

```typescript
public async bundle(file: string, fileRegistry: Registry = {}): Promise<BundleResult>
```

##### Arguments

-   `file: string` - Main file full path
-   `fileRegistry:` [Registry](#registry) - Dictionary of files contents by full path

##### Returns

`Promise<`[BundleResult](#bundleresult)`>`

### Contracts

#### BundleResult

```typescript
import { BundleResult } from "stylus-bundle";
```

```typescript
interface BundleResult {
    imports?: BundleResult[];
    tilde?: boolean;
    filePath: string;
    content?: string;
    found: boolean;
}
```

##### Properties

-   `imports:` [BundleResult](#bundleresult)`[]` - File imports array
-   `tilde?: boolean` - Used tilde import
-   `filePath: string` - Full file path
-   `content: string` - File content
-   `found: boolean` - Is file found

#### Registry

```typescript
import { Registry } from "stylus-bundle";
```

```typescript
interface Registry {
    [id: string]: string | undefined;
}
```

##### Key

`id: string` - File full path as dictionary id

##### Value

`string | undefined` - File content

## License

Released under the [MIT license](LICENSE).
