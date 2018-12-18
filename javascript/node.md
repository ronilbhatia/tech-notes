# Node

* **Node** is a Javascript runtime built on *Chrome's V8 Javascript Engine*
  * uses an event-driven, non-blocking I/O model that makes it lightweight and efficient
    * event-driven refers to the code *listening* for *events* that occur in the application. These event are performed *asynchronously* and are *non-blocking*, because we can run more than one of them at the same time.
      * Note that Node is *single-threaded* but the non-blocking I/O allows processes to occur simultaneously
* **NPM** is node's package ecosystem, and the largest existing ecosystem of open-source libraries in the world
  * *lodash* is a great npm library for a lot of simple utility functions (specific sorts, 'deep-dup' object merging, etc.)
* Node allows for the use of Javascript outside of a browser
* Node takes Javascript code, compiles it into machine code and runs it.
* Node's *global* is the equivalent of the browser's *window*; *process* is the equivalent of *document*
* `module.exports` is just an object used to structure exports from a file. This is why when you import files you have to destructure them if there are multiple exports. If there is a default export then that is what `module.exports` points to, rather than an object holding multiple exports.
* `process.argv` -> gives you the arguments vector, which is an array of all arguments from the command line that were passed when the application was run. The first two will always be `node` and the name of the application run.
