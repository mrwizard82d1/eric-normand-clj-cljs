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

## Creating a shadow-cljs build to manage compilation

If we open the `shadow-cljs.edn` file, we see the keys:

- `source-paths` - Where to find ClojureScript source code
- `dependencis` - Other ClojureScript libraries we need
- `builds` - The JavaScript files we want to build

Let's create a new build called `:app` by adding the following
item to the `:builds` map:

```Clojure
{:app ;; name of build
 {:target :browser ;; we target the browser
  :output-dir "public/app/js" ;; where to output JS files
  :asset-path "/app/js" ;; prefix for our page URLs
  :modules {:main ;; our application only needs one module
                  ;; we will generatethe JavaScript file, `main.js`
            ;; run `counter.app/init` when JavaScript loads
            {:init-fn counter.app/init}}}}
```

Remember, shadow-cljs performs **tree shaking** to determine all
the minimal JavaScript code needed to execute `counter.app/init`.
This process helps keep our JavaScript files small.

## Create a minimal HTML file

We previously defined the build, `:app`, to generate our JavaScript
file. We now want to create a minimal HTML file.

We create that page in the file `public/index.html`. This file 
contains a `script` tag that loads the `app/js/main.js` JavaScript 
file. Remember that the `:app` `:build` specification in 
`shadow-cljs.edn` described how to build our application.

## Serve HTML and JS over HTTP

We can specify the development web server details in the 
`shadow-cljs.edn` file by adding the item, 
`:dev-http {8080 "public"}`. We'll add this item just above the 
`:builds` key. These details tell shadow-cljs to make files in 
the "public" directory on port 8080.

## Write some ClojureScript

(Finally!)

We'll write minimal code. This code will simply write to the 
JavaScript console in the browser.

We've specified that shadow-cljs will run the function, 
`counter.app/init` when our application starts. The prefix, 
`counter.app` indicates that the `init` function is found in the file 
`counter/app.cljs`. Further, this file must be found in the `src/main`
subdirectory. So let's edit this file.

(Just to be clear, let's edit the file, `src/main/counter/app.cljs`.)

## Start shadow-cljs to begin hacking

As is typical with web applications, we had to specify many details 
to get to the point of running our (stupid simple) web application. 
Most of the time, we use a template to provide all this "boilerplate".
However, for teaching purposes, we wanted you to see "how the sausage 
is made."

We are finally ready to start the build. We want shadow-cljs to both
build our application once, but also to watch our build as the files 
change. To accomplish these goals, we run this command:

`npx shadow-cljs watch app`

`watch` is the shadow-cljs command to watch our source code for 
changes. If any changes are found, shadow-cljs will automatically
recompile them and send them to the browser. `app` specifies 
which build to use.

Once built (a few seconds), open the URL `http://localhost:8080/` in
a browser. The browser will display our (empty) page and will print 
our congratulatory message in the JavaScript console. (Additionally,
the title of our shiny new page is printed on our browser tab.)


