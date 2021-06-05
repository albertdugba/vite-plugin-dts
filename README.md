# vite-plugin-dts

A vite plugin that generate `d.ts` file from containing `.vue` files base on `ts-morph`.

## Install

```sh
yarn add vite-plugin-dts -D
```

## Usage

```ts
import { resolve } from 'path'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import dts from 'vite-plugin-dts'

export default defineConfig({
  build: {
    lib: {
      entry: resolve(__dirname, 'src/index.ts'),
      name: 'MyLib',
      formats: ['es'],
      fileName: 'my-lib'
    }
  },
  plugins: [vue(), dts()]
})
```

## Options

```ts
import type { ProjectOptions } from 'ts-morph'

type FilterType = string | RegExp | (string | RegExp)[] | null | undefined

interface TransformWriteFile {
  filePath?: string
  content?: string
}

export interface PluginOptions {
  // Code directory and file format to be converted
  // Default: ['**/*.vue', '**/*.ts', '**/*.tsx']
  include?: FilterType

  // Excluded files/folders
  // Default: 'node_modules/**'
  exclude?: FilterType

  // Depends on the root directory
  // Default: process.cwd()
  root?: string

  // Declaration files output directory
  // Defaults base on your vite config output options
  outputDir?: string

  // Project init Options using by ts-morph
  // Default: null
  projectOptions?: ProjectOptions | null

  // Whether transform '.vue.d.ts' to '.d.ts'
  // Default: false
  cleanVueFileName?: boolean

  // Whether transform dynamic import to static
  // eg. 'import('vue').DefineComponent' to 'import { DefineComponent } from "vue"'
  // Default: false
  staticImport?: boolean

  // Before declaration file be writed hook
  // You can transform declaration file-path and content through it
  // Default: () => {}
  beforeWriteFile?: (filePath: string, content: string) => void | TransformWriteFile
}
```

## Example

Run the following script:

```sh
yarn run test:e2e
```

Then check `example/types`.

## License

MIT License.
