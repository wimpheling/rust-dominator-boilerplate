Use WebPack to build for Production
===

this tutorial would prepare the environment to allow production build.


## 3 files to prepare.
create the following files at the root of your project folder tree, side by side Cargo.toml
1. bootstrap.js
2. package.json
3. webpack.config.js


### bootstrap.js
```
import("./pkg").then(module => {
  module.run_app();
});
```

### package.json
```
{
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack --mode development",
    "build": "webpack --mode production",
    "start:dev": "webpack-dev-server --mode development",
    "start": "webpack-dev-server --mode production"
  },
  "devDependencies": {
    "@wasm-tool/wasm-pack-plugin": "^1.0.1",
    "copy-webpack-plugin": "^5.0.4",
    "webpack": "^4.29.4",
    "webpack-cli": "^3.1.2",
    "webpack-dev-server": "^3.7.2"
  }
}
```

### webpack.config.js
```
const path = require('path');
const WasmPackPlugin = require('@wasm-tool/wasm-pack-plugin');
const CopyWebpackPlugin = require('copy-webpack-plugin');

const distPath = path.resolve(__dirname, "dist");
module.exports = (env, argv) => {
  return {
    devServer: {
      contentBase: distPath,
      compress: argv.mode === 'production',
      port: 8000,
    },
    entry: './bootstrap.js',
    output: {
      path: distPath,
      filename: "rust_dom.js",
      webassemblyModuleFilename: "rust_dom.wasm"
    },
    plugins: [
      new CopyWebpackPlugin([
        { from: './src/static', to: distPath }
      ]),
      new WasmPackPlugin({
        crateDirectory: ".",
        extraArgs: "--no-typescript",
      })
    ],
    watch: argv.mode !== 'production'
  };
};
```

##Go Deploy!
```
yarn install
yarn build
yarn start
```

open browser and go to http://localhost:8000
