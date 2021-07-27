# Node.js
## Installing 
For linux (especially Ubuntu):
```bash
$ sudo apt-get install curl
$ curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
```

Next install Node.js with the following command:
```bash
$ sudo apt-get install -y nodejs
```

To make sure Node.js is installed, run the following two commands at a terminal/command prompt:
```bash
node -v
npm -v
```

## Creating JavaScript Projects
```bash
$ npm init
```

## Run Node Project
```bash
$ node index.js 
Menyalakan mesin kopi
Menggiling biji kopi
Memanaskan air
Mencampurkan air dan kopi
Menuangkan kopi ke dalam gelas
Menuangkan susu ke dalam gelas
Kopi Anda sudah siap!
```

## Run Scripts
Object scripts are objects that contain a collection of scripts in them. The script can be run at any time in our project. To run the script, use the command `npm run <script-name>` which you can write as below:
```bash
$ npm run test
```

In object scripts, we usually define scripts that are often used regularly, such as running applications (during the development process), compiling source code to the production stage, or doing testing.

To assign a new value to the scripts object, we write the script name as a property. Then write the command to be executed as the value of the property. Let's create a new script to run the code from the `index.js` file.

In the scripts object, write a new value with a property called `start`, then add the command to execute the file as the value:
```js
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
```

