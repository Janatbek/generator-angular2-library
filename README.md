### Clone the repo [web-platform-library](https://bitbucket.micron.com/bbdc/projects/ITENG/repos/web-platform-library/browse)

```bash
$ git clone https://JSHARSHEYEV@bitbucket.micron.com/bbdc/scm/iteng/web-platform-library.git
```
### Navigate to the `web-platform-library` directory

```bash
$ cd web-platform-library
```

### Checkout to the 'consuming-library-dev-environment' branch 

```bash
$ git checkout consuming-library-dev-environment
```

### You will see this structure of the app:

```bash
.
├── assets
│   ├── css
│   ├── fonts
│   ├── js
│   ├── .gitkeep
│   └── platform.css
├── src
│  ├── classes
│  ├── components
│  ├── interfaces
│  ├── services
│  ├── appRoutingModule.ts
│  ├── index.ts
│  ├── package.json
│  ├── tsconfig.es5.json
│  └── tsconfig.spec.json
├── tools
│   └── inline-resources.js
├── .gitignore
├── .npmignore	
├── .travis.yml
├── .yo-rc.json	
├── gulpfile.js	
├── package.json	
├── PublishToArtifactory.bat	
├── PublishToPublic.bat	
├── README.MD
├── tsconfig.json	
└── tslint.json

```
### Building your web-platform-library
You can then add or edit `*.ts` files in the `src/` directory and run:

```bash
$ npm run build
```

to automatically create all `*.js`, `*.d.ts` and `*.metadata.json` files in the `dist` directory:

```bash
dist
├── assets
├── classes
├── components
├── interfaces
├── services
├── index.ts
├── index.js
├── package.json
├── README.MD
├── package.json
├── web-platform-library-test.umd
├── web-platform-library.d.ts
└── web-platform-library-metadata.json
```

## TypeScript config

The generator creates 2 TypeScript config files:

- `tsconfig.json` is used to configure your editor during development and is not used for building your library
- `src/tsconfig.es5.json` is used by the Angular compiler to build the files in the `dist` directory when you run `npm run build`

## Linting your code

web-platform-library comes pre-configured with tslint and codelyzer support. To lint your code:

```bash
$ npm run lint
```

## Building web-platform-library

From the root of your web-platform-library directory, run:

```bash
$ npm run build
```

This will generate a `dist` directory with:

- a `package.json` file specifically for distribution with Angular listed in the `peerDependencies`
- `index.js`: a Flat ES Module (FESM) file that contains all your library code in a single file
- `web-platform-library.umd.js`: a Universal Module Definition (UMD) bundle file that contains all your web-platform-library code in UMD format for use in Node.js, SystemJS or via a script tag (e.g. in Plunker, Fiddle, etc)
- `*.d.ts`: type definitions for you library
- `web-platform-library.metadata.json`: metadata for your library to support AOT compilation 

## Consuming web-platform-library during development

To consume your library before you publish it to npm, you can follow the following steps:

1. Navigate to the `web-platform-library` directory:
  ```
  $ cd web-platform-library
  ```
  
2. Compile your library files:
  ```
  $ npm run build
  ```
  
3. From the `web-platform-library/dist` directory, create a symlink in the global node_modules directory to the `dist` directory of your library:
  ```
  $ cd dist
  $ npm link
  ```
## Consuming web-platform-library
6. Navigate to the `web-platform-app-engineering` directory:
  ```
  $ cd web-platform-app-engineering
  ``` 
    

7. From the `web-platform-app-engineering` directory, link the global `web-platform-library` directory to node_modules of the `web-platform-app-engineering` directory:
  ```
  $ npm link web-platform-library
  ```

10. When you make a change to the web-platform-library, recompile your library files again from your `web-platform-library` directory:
  ```
  $ npm run build
  ```
    
11. If you want to automatically recompile the web-platform-library files when a file in `src` changes, run
  ```
  $ npm run build:watch
  ```
  
12. If you are using a `Web-Platform-App-Engineering` to consume your `Web-Platform-Library`, make sure to set up a [path mapping](https://github.com/angular/angular-cli/wiki/stories-linked-library#use-typesscript-path-mapping-for-peer-dependencies) in `/src/tsconfig.app.json` of your consuming application (not your library):
  ```typescript
  {
    "compilerOptions": {
      // ...
      // Note: these paths are relative to `baseUrl` path.
      "paths": {
        "@angular/*": [
          "../node_modules/@angular/*"
        ]
      }
    }
  }
  ```
  
When you npm link a library with peer dependencies, the [consuming application searches for the peer dependencies in the library's parent directories instead of the application's parent directories](http://codetunnel.io/you-can-finally-npm-link-packages-that-contain-peer-dependencies).

If you get `Error: Unexpected value '[object Object]' imported by the module 'AppModule'. Please add a @NgModule annotation.`, then try:

```
$ ng serve --preserve-symlinks
```
or

```
$ npm start --preserve-symlinks
```

to make sure the consuming application searches for the peer dependencies in the application's node_modules directory.  
   

### web-platform-library
### v1.0.8

- Added documentation
- Added boilerplate consuming
- Initial version

