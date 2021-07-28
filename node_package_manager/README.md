# Node Package Manager
## Getting Started with NPM
NPM is a package manager that is widely used by JavaScript developers in managing packages, besides NPM there is also a Yarn Package Manager. Both, yarn or npm, are package managers that can help us develop web or node applications. However, in this material we will only discuss one of the package managers, namely NPM. This is because NPM is the standard package manager provided by Node.js.

Node Package Manager (NPM) is a package manager for JavaScript that can make it easier for us to manage packages available at [https://www.npmjs.com/](https://www.npmjs.com/). NPM is a standard package manager provided by Node.js and is automatically installed when installing Node.js on our computers.

There are many commands available in NPM. To see the list, we can run the npm help command at the terminal/command prompt.
```bash
$ npm help
```

Then use `-h` if we want to see a guide to using one of the commands. For example, you want to see details on how to use the install command, so to see it write the following command:
```bash
$ npm install -h

npm install (with no args, in package dir)
npm install [<@scope>/]<pkg>
npm install [<@scope>/]<pkg>@<tag>
npm install [<@scope>/]<pkg>@<version>
npm install [<@scope>/]<pkg>@<version range>
npm install <alias>@npm:<name>
npm install <folder>
npm install <tarball file>
npm install <tarball url>
npm install <git:// url>
npm install <github username>/<github project>

aliases: i, isntall, add
common options: [--save-prod|--save-dev|--save-optional] [--save-exact] [--no-save]
```

If you look at the guide in the image above, you can find several aliases. Aliases or aliases are another way of doing the command. That means we can write the install command with `i`, `ins`, `install`, `add`, or something else.
```bash
npm install
npm i
npm in
npm ins
npm isntal
npm add
```

You can get a full explanation of all the commands in NPM on the following official page: [https://docs.npmjs.com/cli/v7/commands](https://docs.npmjs.com/cli/v7/commands). However, there are some important commands that we will be used to in the material as well as further application development.
| Command | Description | Common Options | 
| - | - | - |
| init | Membuat berkas package.json pada project | [--force\|-f\|--yes\|-y\|--scope] | 
| install \<package-name> | Memasang dan mendaftarkan package pada berkas package.json | [-P\|--save-prod\|-D\|--save-dev\|-O\|--save-optional] [-E\|--save-exact] [-B\|--save-bundle] [--no-save] [--dry-run] | 
| run-script \<command> | Menjalankan perintah yang terdapat pada objek scripts di berkas package.json | [--silent] [-- \<args>...] | 
| uninstall \<package-name> | Menghapus dan mengeluarkan package dari berkas package.json | [-S\|--save\|-D\|--save-dev\|-O\|--save-optional\|--no-save] | 
| version | Untuk melihat versi package yang tersedia secara global atau lokal | [\<newversion> \| major \| minor \| patch \| premajor \| preminor \| prepatch \| prerelease [--preid=<prerelease-id>] \| from-git] | 

## Installing Packages
Before starting to install packages, we need to know first that there are two types of package installations, namely local installs and global installs.

The local package will be installed in the same directory or folder as our project. This package will be placed in the **node_modules** folder.

While the global package is installed in one place on our device system (depending on the settings during node/npm installation).

Generally, all packages must be installed locally. This ensures that every project or application on our computer has the right package and version for it. To install a package locally, the method is the same as we discussed earlier, namely with the npm install command.
```bash
$ npm install <package-name>
```

Then, when do we use the global package? A package should be installed globally only when it provides commands that can be executed from the CLI and reused in all projects. Some examples of packages that need to be installed globally include:
- [npm](https://www.npmjs.com/package/npm)
- [nodemon](https://www.npmjs.com/package/nodemon)
- [mocha](https://www.npmjs.com/package/mocha)
- [create-react-app](https://www.npmjs.com/package/create-react-app)

To install packages globally, we simply add the `-g` parameter to the npm install command. Where `-g` means global.
```bash
$ npm install -g <package-name>
```

There are actually two types of object dependencies in the **package.json** file. The first is a `dependency` object and the second is a `devDependencies` object.

The dependencies object is an object that holds the package that we use to build the application. While the devDependencies object is used for related packages only during the application development process, for example, the `jest` package which is used for testing. Packages like jest are only used during the application development process. It is deprecated when the application is released or used directly by the user.

To install a package as devDependencies, we can add the `--save-dev` parameter to the npm install command.
```bash
$ npm install <package-name> --save-dev
```

Inside the project will appear the **package-lock.json** file. This file is automatically generated by Node to describe the project structure and packages (one package can use another package). The **package-lock.json** file also defines which version of the package to use more specifically. What does it mean?

If you notice, in the package.json file we specify the version with the caret symbol (^). In addition to caret, npm also uses the tilde symbol (~). Both are used to determine the minor version and the patch version to use.

So if we see version ~1.0.2 it means npm can install version 1.0.2 or latest patch version like 1.0.4. If the package version is written with caret like ^1.0.2, it means that npm can install version 1.0.2 or the latest minor version like 1.1.0.

## Using Package
We need to understand again that the package that we add to the project is actually a module. That's why in our project the **node_modules** folder will also appear. It contains JavaScript code that composes a package. If you're “brave”, you can see what the code looks like inside the lodash package.

Since it is a module, we can add code from the package using `require()` as we learned in the Module material.
```js
const variableName = require('package-name');
```

So, to use the code from the lodash package that we installed, add the following code to the index.js file:
```js
const _ = require('lodash');
```

Naming using an underscore (_) as above is a standard from lodash that we need to follow.

In their documentation, lodash mentions that they provide utilities to make JavaScript easier by removing the hassle when using arrays, numbers, objects, strings, etc.

For example, to add up each number value in an array, do this in the following way.
```js
const _ = require('lodash');
 
const myArray = [1, 2, 3, 4];
let sum = 0;
 
for(let i = 0; i < myArray.length; i++) {
    sum += myArray[i];
}
 
console.log(sum);
 
/* output
10
*/
```

Alternatively, we can use the reduce function as follows:
```js
const _ = require('lodash');
 
const myArray = [1, 2, 3, 4];
let sum = myArray.reduce((prev, curr) => {
    return prev + curr;
});
 
console.log(sum);
 
/* output
10
*/
```

With lodash, we can summarize the code like this:
```js
const _ = require('lodash');
 
const myArray = [1, 2, 3, 4];
const sum = _.sum(myArray);
 
console.log(sum);
 
/* output
10
*/
```

## Uninstall Package
To do so is quite easy. If the package is in the dependencies object, we can remove it using the command:
```bash
$ npm uninstall <package-name>
```

If the package is in devDependencies, we can simply add `--save-dev` at the end of the command.
```bash
npm uninstall <package-name> --save-dev
```

Apart from removing the value from **package.json**, this command will also delete all files related to the lodash package in the **node_modules** folder.

