How to Deploy Your Purescript Project

This is an example of a very simple purescript workflow.  It's probaly not ideal, but it should server as a good starting point for beginners.

```bash
# Create a new purescript project
pulp init

# Make sure to install the bower dependencies
bower install

# We will be putting our compiled javascript into the /dist folder
mkdir dist

# Create the script that will start our development workflow
touch development.sh
chmod +x development.sh
```

Put the following in development.sh...

```bash
#!/bin/bash
# ... This will do an initial compilation to dist/project, and then
# start the server via 'pulp server'.
# Prior to starting, it will watch all project files.  When a file
# change happens, the project recompiled into dist/project.js
pulp browserify --to dist/project.js
pulp server --before pulp --watch pulp browserify --to dist/project.js
```

Create index.html in your project root and include the project.js file...

```html
<html>
  <body>
    <script src="dist/project.js"></script>
  </body>
</html>
```

Now run your development.sh script, and go to localhost:1337 in your browser.

-----

To further break down the steps...

```
# To do a one time compile run...
pulp browserify --to dist/project.js
```

```
# To watch projects files and then compile run...
pulp --watch pulp browserify --to dist/project.js
```

Note that pulp browserify creates a standalone javascript file.  pulp build on the other hand will create a set of seperate files that work in conjunction with the browserify  module loader.
