Prepare 'static' folder
===

this is the folder for index.html, css, and images.
static folder can be placed outside or inside src folder

## folder structure
```
rust-dom
  - src
    lib.rs
      - static
        index.html
          - assets
            - css
            - img
            - fonts
```

## index.html
rust_dom.js can be differnt if your project name is helloworld, then you need to change it to helloworld.js. ** your project name is the package name in the cargo.toml.
```
<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <link rel="icon" type="image/png" href="favicon.png" />
        <title>Rust-Dom</title>
    </head>
    <body>
        <noscript>You need to enable JavaScript to run this app.</noscript>
        <script src="rust_dom.js"></script>
    </body>
</html>
```