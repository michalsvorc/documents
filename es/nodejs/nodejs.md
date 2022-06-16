# Node.js

Overview:

* [API](https://nodejs.org/api/)
* [Node.js Guides](https://nodejs.org/en/docs/guides/)
* [Knowledge base](https://nodejs.org/en/knowledge/)

References:

* [Command-line options](https://nodejs.org/api/cli.html#cli_command_line_options)
* [Environment variables](https://nodejs.org/api/cli.html#cli_environment_variables)
* [OS constants](https://nodejs.org/api/os.html#os_os_constants_1):
* [Error codes](https://nodejs.org/api/errors.html#errors_node_js_error_codes)

Resources:

* [(PDF) How To Code in Node.js](https://assets.digitalocean.com/books/how-to-code-in-nodejs.pdf)

Node.js is an open-source server side runtime environment built on Chrome's V8 JavaScript engine. It provides an event
driven, non-blocking (asynchronous) I/O and cross-platform runtime environment for building highly scalable server-side
applications using JavaScript.

Node.js consists of:

* V8 engine: The runtime environment in which JavaScript executes.
* Libuv: Asynchronous I/O based on event loops.

JavaScript is internally compiled by V8 with JIT compilation to speed up the execution.

## Event-Driven programming

Node.js is a single-threaded application, but it can support concurrency via the concept of event and callbacks.

Node uses an observer pattern. Node thread keeps an event loop and whenever a task gets completed, it fires the
corresponding event which signals the event-listener function to execute.

In an event-driven application, there is generally a main loop that listens for events, and then triggers a callback
function when one of those events is detected.

## Error-first callbacks

Most asynchronous methods exposed by the Node.js core API follow an idiomatic pattern referred to as an error-first
callback. With this pattern, a callback function is passed to the method as an argument.

When the operation either completes or an error is raised, the callback function is called with the Error object (if
any) passed as the first argument. If no error was raised, the first argument will be passed as null.

## Global object

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Global_object)

A global object is an object that always exists in the global scope. In Node.js, you can access the global object using
the `global` keyword.

`window`, `self`, or `frames` won’t work in the Node.js environment, you must instead use `global`.

Keep in mind that the top-level scope in Node.js is not the global scope. For example in browsers, `var a = 1` will
create a global variable `a`. In Node.js however, the variable will be local to the module itself.

### this

In Node modules, `this` at the top level doesn’t reference the global object. Instead, it has the same value as
`module.exports`.

### globalThis

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis)

The `globalThis` property provides a standard way of accessing the *global* `this` value (and hence the global object
itself) across environments.

```nodejs
console.log(globalThis);  // => Object [global] {...}
console.log(global);      // => Object [global] {...}
```

### Global objects

* [API](https://nodejs.org/api/globals.html#globals_global_objects)

Node.js global objects are global in nature and they are available in all modules. We do not need to include these
objects in our application, rather we can use them directly. 

* [`__dirname`](https://nodejs.org/api/globals.html#globals_dirname)
* [`__filename`](https://nodejs.org/api/globals.html#globals_filename)
* [global](https://nodejs.org/api/globals.html#globals_global)
* [module](https://nodejs.org/api/globals.html#globals_module)
* [process](https://nodejs.org/api/globals.html#globals_process)

## Modules

API:

* [Modules](https://nodejs.org/api/module.html)
* [Packages](https://nodejs.org/api/packages.html)

Guides:

* [Why CommonJS and ES Modules Can’t Get Along](https://redfin.engineering/node-modules-at-war-why-commonjs-and-es-modules-cant-get-along-9617135eeca1)
* [Determining module system](https://nodejs.org/api/packages.html#packages_determining_module_system)

Since Node 14, there are two kinds of modules: CommonJS and ECMAScript.

### CommonJS modules

* [API](https://nodejs.org/api/modules.html)

```javascript
const circle = require('./circle.js')
```

In CommonJS, `require()` is synchronous. Node.js uses the CommonJS modules internally.

### ECMAScript (ESM) modules

* [API](https://nodejs.org/api/esm.html)

```javascript
import circle from './circle.js'
```

In ESM, the module loader runs in asynchronous phases. In the first phase, it parses the script to detect calls to
import and export without running the imported script.

ECMAScript modules are the official standard format to package JavaScript code for reuse. Modules are defined using a
variety of import and export statements.

ESM scripts use Strict Mode by default.

Node.js treats JavaScript code as CommonJS modules by default. Authors can tell Node.js to treat JavaScript code as
ECMAScript modules via the `.mjs` file extension, the package.json `type` field, or the `--input-type` flag.

It is not possible to `require()` files that have the `.mjs` extension.

## HTTP

* [API](https://nodejs.org/docs/latest-v12.x/api/http.html)
* [Anatomy of an HTTP Transaction](https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/)

Constants:

* [http.METHODS](https://nodejs.org/api/http.html#http_http_methods)
* [http.STATUS_CODES](https://nodejs.org/api/http.html#http_http_status_codes)

## HTTPS

* [API](https://nodejs.org/docs/latest-v12.x/api/https.html#https_https)

HTTPS is the HTTP protocol over TLS/SSL. In Node.js this is implemented as a separate module.

## Process

* [API](https://nodejs.org/api/process.html)

The process object is a global that provides information about, and control over, the current Node.js process.

The process object is an instance of [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter).

* [process.argv](https://nodejs.org/api/process.html#process_process_argv)

The process.argv property returns an array containing the command-line arguments passed when the Node.js process was launched. 

```nodejs
[0]: /usr/local/bin/node                    // process.execPath
[1]: /Users/mjr/work/node/process-args.js   // path to the file being executed
[2]: baz
[3]: foo=bar
```

* [process.exit([code])](https://nodejs.org/api/process.html#process_process_exit_code)

The process is immediately and ungracefully forced to terminate. Otherwise, a program will gracefully exit when all the processing is done.

When you're running a server as an indefinite process, you need to send the command a `SIGTERM` signal, and handle that with the process signal handler. \

See [process exit codes](https://nodejs.org/api/process.html#process_exit_codes).

## CPU intensive tasks

* [Node.js
  multithreading](https://blog.logrocket.com/node-js-multithreading-what-are-worker-threads-and-why-do-they-matter-48ab102f8b10/)

### Child process

* [API](https://nodejs.org/api/child_process.html#child_process_child_process)

The child_process module provides the ability to spawn subprocesses in a manner that is similar, but not identical, to[
popen(3)](http://man7.org/linux/man-pages/man3/popen.3.html).

This capability is primarily provided by the `child_process.spawn()` function.

Forking a process is an expensive process in terms of resources. And it is slow. It means running a new virtual machine
from scratch using a lot of memory since processes don’t share memory.

### Worker Threads

* [API](https://nodejs.org/api/worker_threads.html)

Worker threads have isolated contexts. They exchange information with the main process using message passing, so we
avoid the race conditions problem threads have! But they do live in the same process, so they use a lot less memory.

## Events

* [API](https://nodejs.org/api/events.html)

Much of the Node.js core API is built around an idiomatic asynchronous event-driven architecture.

The `EventEmitter` calls all listeners synchronously in the order in which they were registered. This ensures the proper
sequencing of events and helps avoid race conditions and logic errors.

When appropriate, listener functions can switch to an asynchronous mode of operation using the `setImmediate()` or
`process.nextTick()` methods.

## File system

* [API](https://nodejs.org/api/fs.html)
* [Constants](https://nodejs.org/api/fs.html#fs_fs_constants)
* [Notes](https://nodejs.org/api/fs.html#fs_notes)

The fs module enables interacting with the file system in a way modeled on standard POSIX functions.

All file system operations have synchronous, callback, and promise-based forms, and are accessible using both CommonJS syntax and ES6 Modules (ESM).

* [Promise example](https://nodejs.org/api/fs.html#fs_promise_example)
* [Callback example](https://nodejs.org/api/fs.html#fs_callback_example)
* [Synchronous example](https://nodejs.org/api/fs.html#fs_synchronous_example)

## Buffer

* [API](https://nodejs.org/api/buffer.html)
* [String decoder API](https://nodejs.org/api/string_decoder.html)
* [Guide](https://nodejs.org/en/knowledge/advanced/buffers/how-to-use-buffers/)

Buffer objects are used to represent a fixed-length sequence of bytes. Many Node.js APIs support Buffers.

The `Buffer` class is a subclass of JavaScript's `Uint8Array` class and extends it with methods that cover additional
use cases. Node.js APIs accept plain `Uint8Arrays` wherever `Buffers` are supported as well.

When converting between Buffers and strings, a character encoding may be specified. If no character encoding is
specified, UTF-8 will be used as the default.

Converting a `Buffer` into a string using one of the above is referred to as decoding, and converting a string into a
`Buffer` is referred to as encoding.

The `string_decoder` module provides an API for decoding Buffer objects into strings in a manner that preserves encoded
multi-byte UTF-8 and UTF-16 characters.

## Stream

API:

* [API](https://nodejs.org/api/stream.html)

Libraries:

* [(Library) concat-stream](https://www.npmjs.com/package/concat-stream)

A stream is an abstract interface for working with streaming data in Node.js. All streams are instances of EventEmitter.

There are four fundamental stream types within Node.js:

* [Writable](https://nodejs.org/api/stream.html#stream_class_stream_writable)
* [Readable](https://nodejs.org/api/stream.html#stream_class_stream_readable)
* [Duplex](https://nodejs.org/api/stream.html#stream_class_stream_duplex)
* [Transform](https://nodejs.org/api/stream.html#stream_class_stream_transform)

All streams created by Node.js APIs operate exclusively on strings and `Buffer` (or Uint8Array) objects.

Both Writable and Readable streams will store data in an internal buffer. The amount of data potentially buffered depends on the `highWaterMark` option passed into the stream's constructor.

A key goal of the stream API, particularly the `stream.pipe()` method, is to limit the buffering of data to acceptable
levels such that sources and destinations of differing speeds will not overwhelm the available memory.

The highWaterMark option is a threshold, not a limit: it dictates the amount of data that a stream buffers before it
stops asking for more data.

With the support of async generators and iterators in JavaScript, async generators are effectively a first-class
language-level stream construct at this point.

Some common interop cases of using Node.js streams with async generators and async iterators are provided
[here](https://nodejs.org/api/stream.html#stream_streams_compatibility_with_async_generators_and_async_iterators).

## Asynchronous Context Tracking

* [API](https://nodejs.org/api/async_context.html)

These classes are used to associate state and propagate it throughout callbacks and promise chains. They allow storing
data throughout the lifetime of a web request or any other asynchronous duration. It is similar to thread-local storage
in other languages.

## Crypto

* [API](https://nodejs.org/api/crypto.html)
* [Guide](https://nodejs.org/en/knowledge/cryptography/how-to-use-crypto-module/)

The crypto module provides cryptographic functionality that includes a set of wrappers for OpenSSL's hash, HMAC, cipher,
decipher, sign, and verify functions.

## Timers

* [API](https://nodejs.org/api/timers.html)

### Immediate

Immediate object is created internally and is returned from `setImmediate()`. It can be passed to `clearImmediate()` in
order to cancel the scheduled actions.

`setImmediate()` schedules the "immediate" execution of the callback after I/O events' callbacks.

When multiple calls to `setImmediate()` are made, the callback functions are queued for execution in the order in which
they are created. The entire callback queue is processed every event loop iteration. If an immediate timer is queued
from inside an executing callback, that timer will not be triggered until the next event loop iteration.

### Timeout

Timeout object is created internally and is returned from `setTimeout()` and `setInterval()`. It can be passed to either
`clearTimeout()` or `clearInterval()` in order to cancel the scheduled actions.

The callback will likely not be invoked in precisely delay milliseconds. Node.js makes no guarantees about the exact
timing of when callbacks will fire, nor of their ordering. The callback will be called as close as possible to the time
specified.

## Utilities

### OS

* [API](https://nodejs.org/api/os.html)

The os module provides operating system-related utility methods and properties.

### Path

* [API](https://nodejs.org/api/path.html)

The path module provides utilities for working with file and directory paths.

### URL

* [API](https://nodejs.org/api/url.html)

The url module provides utilities for URL resolution and parsing.

### Util

* [API](https://nodejs.org/api/util.html)

The util module supports the needs of Node.js internal APIs. Many of the utilities are useful for application and module
developers as well.

* [`util.format(format[, ...args])`](https://nodejs.org/api/util.html#util_util_format_format_args)

Returns a formatted string using the first argument as a printf-like format string which can
contain zero or more format specifiers. Each specifier is replaced with the converted value from the corresponding
argument.

* [`util.promisify(original)`](https://nodejs.org/api/util.html#util_util_promisify_original)

Takes a function following the common error-first callback style, i.e. taking an `(err, value) => ...` callback as the
last argument, and returns a version that returns promises. Check if there already exists a promise-based version of a
function before using promisify.

* [`util.types`](https://nodejs.org/api/util.html#util_util_types)

Provides type checks for different kinds of built-in objects. 

## Debugging

* [Documentation](https://nodejs.org/en/docs/guides/debugging-getting-started/)

Available APIs:

* [Debugger](https://nodejs.org/api/debugger.html)
* [Assert](https://nodejs.org/api/assert.html)
* [Performance measurement](https://nodejs.org/api/perf_hooks.html)
* [Diagnostic report](https://nodejs.org/api/report.html)
* [util.inspect](https://nodejs.org/api/util.html#util_util_inspect_object_options)

Guides:

* [Easy profiling for Node.js Applications](https://nodejs.org/en/docs/guides/simple-profiling/)

## Zlib

* [API](https://nodejs.org/api/zlib.html#zlib_zlib)

The zlib module provides compression functionality implemented using Gzip, Deflate/Inflate, and Brotli.

