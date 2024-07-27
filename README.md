# NPM Package using ng-packagr

Writing a typescript library is HARD.  The `@angular/cli`
has tools for creating one, but I want to have to include
as little as possible to build my library.

Below I have a Log showing what I did with comments as I go.
Here are the steps:

1. create a package with `npm init`
2. install ng-packagr with `npm install -D ng-packagr`
3. add build script to your package.json: `"build": "ng-packagr -p ng-package.json"`
4. add a new file `ng-package.json`:
    ```
    {
      "$schema": "./node_modules/ng-packagr/ng-package.schema.json"
    }
    ```
5. add a new file `src/public_api.ts`:
    ```
    export function add(a: number, b: number): number {
      return a + b
    }
    ```
6. run `npm build`

That's it.   The 'dist' directory contains your package.
It can be published with `npm publish dist`.   If you go
into it you can run `npm link` and then use it from
other projects on your computer with `npm link <package-name>`
with whatever package name you have in the package.json.

## Log

I created this directory and ran `npm init -y` inside it,
and created this `README.md` file and a `.gitignore`
file to ignore node_modules. ('First Commit')

I ran `npm install -D ng-packagr`

Following instructions on [ng-packagr npm](https://www.npmjs.com/package/ng-packagr)
I created the ng-package.json file with no contents. I added a script
so I could run it  using `npm pack -- <args>`:

    "pack": "ng-packagr"

Then ran it:

    npm run pack -- -p ng-package.json

That didn't recognize it, so I actually had to add the base schema content:

    {
      "$schema": "./node_modules/ng-packagr/ng-package.schema.json"
    }

Then it ran with an error because it didn't have enough information.

Added recommended build script to make it even easier:

    "build": "ng-packagr -p ng-package.json"

Created second commit: "Added ng-packagr"

Ok, time to create some code.   This is the error I get:

```
------------------------------------------------------------------------------
Building entry point 'my-packager'
------------------------------------------------------------------------------
✖ Compiling with Angular sources in Ivy partial compilation mode.
error TS6053: File 'C:/git/OneHitWonder/npm-test/my-packager/src/public_api.ngtypecheck.ts' not found.
  The file is in the program because:
    Root file specified for compilation
error TS6053: File 'C:/git/OneHitWonder/npm-test/my-packager/src/public_api.ts' not found.  The file is in the program because:
    Root file specified for compilation
```

So it's looking for `src/public_api.ts`, let's add that and some actual
code...

    export function add(a: number, b: number): number {
      return a + b
    }

Pretty cool, that actually worked!  Now copying from an angular project, I'm going to
add `/dist` to `.gitignore`.

So at this point I have the OUTPUT library in the `/dist` folder.
You can publish from there, but in my case for development I'm
going to switch to the `/dist` folder and run `npm link`.  This
creates a link to the package 'my-packager' on my computer when
it's added elsewhere.

Then I went to a vuetify project I created and ran `npm link my-packager`
which links to what I did above.  Adding this code and running
the app showed it worked!

    import { add } from 'my-packager'
    console.log(`3 + 19 = ${add(3, 19)}`)

## Links:

* https://angular.dev/tools/libraries/angular-package-format
* https://github.com/ng-packagr/ng-packagr
* https://www.npmjs.com/package/ng-packagr