ts-migrate-extra is an extension to ts-migrate package with addition feature

# HOW to use

1. install all packages required for your project @types/libName
   i.e. npm i --save-dev @types/node @types/sequelize @types/axios @types/body-parser @types/config @types/cors @types/dotenv @types/express @types/lodash @types/qs @types/xml2js

2. create global.d.ts in your project and add all private packages in it:
   i.e.
   declare module '@ncid/core';
   declare module 'aws-cognito-srp-client';
   declare module 'aws-sdk';
   declare module 'aws-sdk-mock';

3. turn off all prettier/lint check
   i.e. comment out everything in .\.husky\pre-commit

4. npm install --save-dev ts-migrate-extra
   npx ts-migrate-extra-full <folder>
   i.e. npx ts-migrate-extra-full ./abcservice

After finishing migration (for building and running the project):

1.  change tsconfig.json to this:<br>
   ```
    {
    "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

            /* Language and Environment */
            "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */

            /* Modules */
            "module": "commonjs",                                /* Specify what module code is generated. */
            "rootDir": "./",                                  /* Specify the root folder within your source files. */
            "moduleResolution": "node",                       /* Specify how TypeScript looks up a file from a given module specifier. */

            /* Emit */
            "outDir": "./dist/server",                                   /* Specify an output folder for all emitted files. */

            /* Interop Constraints */
            // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
            // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
            "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
            // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
            "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

            /* Type Checking */
            "strict": true,                                      /* Enable all strict type-checking options. */
            "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */

        }
        }

```
2.  add
   ```
    "start": "node dist/server/server/index.js",
    "build": "rimraf ./dist && tsc -p tsconfig.json",
   ```
    <br>to package.json

# ts-migrate

_ts-migrate_ is a tool for helping migrate code to TypeScript.
It takes a JavaScript, or a partial TypeScript, project in and gives a compiling TypeScript project out.

_ts-migrate_ is intended to accelerate the TypeScript migration process. The resulting code will pass the build, but a followup is required to improve type safety. There will be lots of `// @ts-expect-error`, and `any` that will need to be fixed over time. In general, it is a lot nicer than starting from scratch.

_ts-migrate_ is designed as a set of plugins so that it can be pretty customizable for different use-cases. Potentially, more plugins can be added for addressing things like improvements of type quality or libraries-related things (like prop-types in React).

Plugins are combined into migration configs. We currently have two main migration configs:

- for the main JavaScript → TypeScript migration
- for the reignore script

These configs can be moved out of the default script, and people can add custom configs with a different set of plugins for their needs.

You can find instructions on how to install and run ts-migrate in the [main package](./packages/ts-migrate/). If you find any [issues](https://github.com/airbnb/ts-migrate/issues) or have ideas for improvements, we welcome your [contributions](https://github.com/airbnb/ts-migrate/blob/master/CONTRIBUTING.md)!

Check out the [blog post](https://medium.com/airbnb-engineering/ts-migrate-a-tool-for-migrating-to-typescript-at-scale-cd23bfeb5cc) about ts-migrate!

# Published Packages

| Folder                                                        | Version                                                                                                        | Package                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| [packages/ts-migrate](./packages/ts-migrate/)                 | [![npm version](https://badge.fury.io/js/ts-migrate.svg)](https://badge.fury.io/js/ts-migrate)                 | [ts-migrate](https://www.npmjs.com/package/ts-migrate)                 |
| [packages/ts-migrate-plugins](./packages/ts-migrate-plugins/) | [![npm version](https://badge.fury.io/js/ts-migrate-plugins.svg)](https://badge.fury.io/js/ts-migrate-plugins) | [ts-migrate-plugins](https://www.npmjs.com/package/ts-migrate-plugins) |
| [packages/ts-migrate-server](./packages/ts-migrate-server/)   | [![npm version](https://badge.fury.io/js/ts-migrate-server.svg)](https://badge.fury.io/js/ts-migrate-server)   | [ts-migrate-server](https://www.npmjs.com/package/ts-migrate-server)   |

# Unpublished Packages

| Folder                                                        | Description                                                                           |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [packages/ts-migrate-example](./packages/ts-migrate-example/) | basic example of usage of the ts-migrate-server with a writing a custom simple plugin |

# Authors

<table>
  <tbody>
    <tr>
      <td align="center" valign="top">
        <img width="100" height="100" src="https://github.com/brieb.png?s=150">
        <br>
        <a href="https://github.com/brieb">Brie Bunge</a>
      </td>
      <td align="center" valign="top">
        <img width="100" height="100" src="https://github.com/Rudeg.png?s=150">
        <br>
        <a href="https://github.com/Rudeg">Sergii Rudenko</a>
      </td>
      <td align="center" width="20%" valign="top">
        <img width="100" height="100" src="https://github.com/jjjjhhhhhh.png?s=150">
        <br>
        <a href="https://github.com/jjjjhhhhhh">John Haytko</a>
      </td>
      <td align="center" valign="top">
        <img width="100" height="100" src="https://github.com/elliotsa.png?s=150">
        <br>
        <a href="https://github.com/elliotsa">Elliot Sachs</a>
      </td>
      <td align="center" valign="top">
        <img width="100" height="100" src="https://github.com/lencioni.png?s=150">
        <br>
        <a href="https://github.com/lencioni">Joe Lencioni</a>
     </tr>
  </tbody>
</table>

# License

MIT, see [LICENSE](https://github.com/airbnb/ts-migrate/blob/master/LICENCE) for details.
