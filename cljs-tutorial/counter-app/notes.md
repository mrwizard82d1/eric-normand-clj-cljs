# ClojureScript Tutorial

Notes from [ClojureScript Tutorial](https://ericnormand.me/guide/clojurescript-tutorial)
by Eric Normand.

## Start a ClojureScript project with shadow-cljs

Using shadow-cljs to build a (skeleton) ClojureScript project requires:

- Node.js
- npm
- Java

After installing the pre-requisite software, execute the command, 
`npx create-cljs-project counter-app`. This command constructs a 
complete but skeletal ClojureScript application. Note that 
creating this application may take a surprisingly long time -
even on a fast computer. The source code for the project can be 
found in the `counter-app` subdirectory.

The `counter-app` subdirectory contains:

- `node_modules` - where npm keeps the installed npm libraries
- `package.json` - lists the npm packages to install
- `package-lock.json` - defines the installed npm packages along 
  with the detailed version information
- `shadow-cljs.edn`- the shadow-cljs project configuration file
- `src` - folder for ClojureScript source code

The `src` directory contains two subdirectories:

- `main` contains the production Clojure(Script) code
- `test` contains the Clojure(Script) for testing

These two directories are **created empty**

You actually now have a **working** if skeletal project. Additionally,
after having created the project structure, this command will open a
browser REPL session. (To open this session later, execute the 
command, `npx shadow-cljs clj-repl`. After starting the REPL session,
you will need to navigate to `localhost:9630:/repl-js/browser-repl` 
to see the root web page.) 

When executed the first time, `npx create-cljs-project <app-name>` will 

- Create the project source code
- Download all necessary packages (takes time) 
- Open the application in a new browser window
- Open a REPL connected to an `nREPL` server

We can now test our REPL connection by entering the expression, 
`(js/alert "Hello!")` at the REPL prompt in the terminal.


