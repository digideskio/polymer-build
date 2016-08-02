# polymer-build

Polymer-build is a library for building Polymer projects. While the [Polymer CLI](https://github.com/Polymer/polymer-cli) is still the easiest way to build a project, it's customization options are limited. Polymer-build allows you to create a completely customized build pipeline, which can include additional streams and build tasks in any order. Use polymer-build over the CLI if you:

- Need to customize your build(s) without using command-line flags/arguments
- Need to run your source code through custom optimizers/processors before, after, or during build
- Need to hook additional logic into any part of the build process


## Installation

```
npm install --save-dev polymer-build
```


## Usage

 The library was built for Gulp, but it can be used anywhere that Node streams can.

 See the [examples/](examples/) directory for examples of how polymer-build can be used to create a full build-pipeline for your application.


### let project = new PolymerProject(options)

PolymerProject gives you access to a collection of streams and helpers for creating your custom build pipeline.

The following options are supported:

```js
// See ProjectOptions in src/polymer-project.js for more information
let project = new PolymerProject({
  root: process.cwd(),
  entrypoint: 'index.html',
  shel': 'src/my-app.html',
  fragments: [
    'src/my-view1.html',
    'src/my-view2.html',
    'src/my-view3.html'
  ],
  sourceGlobs: [
    'src/**',
    'images/**',
    'bower.json',
  ],
  includeDependencies: [
  	'bower_components/webcomponentsjs/webcomponents-lite.min.js',
  ]
}
```

### project.sources()

Returns a readable stream for your source files.

### project.dependencies()

Returns a readable stream for your dependencies.

### project.analyzer

Analyzes your files (sources and dependencies).

### project.bundler

Bundles your application.

### project.splitHtml()

Splits the HTML files in your stream into seperate HTML, CSS, and JS files. Useful for linting/processing specific files with tools that need single-language files.

### project.rejoinHtml()

Rejoin split files.

### let newStream = forkStream(stream)

Helper function for forking a readable stream. This creates a new stream that will read the same data as the given stream, which can be piped somewhere new. Similar to https://github.com/mariocasciaro/gulp-clone

### generateServiceWorker()

Generates a service worker, returns a promise.

### addServiceWorker()

Similar to `generateServiceWorker()`, but also writes that file to disk.


## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

You can compile polymer-build from source by cloning the repo and then running `npm run build`. Make sure you have already run `npm install` before compiling.


## Supported Node.js Versions

polymer-build targets the current LTS version (4.x) of Node.js and later.

