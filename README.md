# NPM Package using ng-packagr

Writing a typescript library is HARD.  The `@angular/cli`
has tools for creating one, but I want to have to include
as little as possible to build my library.

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

## Links:

* https://angular.dev/tools/libraries/angular-package-format
* https://github.com/ng-packagr/ng-packagr
* https://www.npmjs.com/package/ng-packagr