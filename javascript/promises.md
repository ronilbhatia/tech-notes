# Promises

* Javascript objects that take an _executor_ function which will either _resolve_ or _reject_, based on the success in executing the promise.
* When a `.then` is chained onto a promise, you pass it two callbacks as arguments - these two functions are respectively used as the `resolve` and `reject` callbacks in the context of the promise.
* When constructing a promise you first write the code that the promise is actually intended to execute (for example, making an API call), and then you create some constraint to determine whether or not the promise executed successfully, invoking the `resolve` callback on success, and the `reject` callback on failure.
  * If the thing you are doing is async, then you will want to implement the logic for determining whether the promise was *fulfilled* or *rejected*, as a callback to the async function.
  * In Vanilla JS, only one argument may be passed to both the `resolve` and `reject` callbacks.
  * jQuery has *deferreds*, which are the things returned by `$.ajax` - which sometimes take multiple arguments such as the following:
    * `resolve(response, statusText, xhrObj)`
    * `reject(xhrObj, statusText, error)`
* A promise has an **action**, which is the thing it is supposed to do before it either fails or succeeds based on some constraint
* A promise can be
  * **Fulfilled** - The promise's *action* succeeded
    * This results in the `resolve` callback being invoked
  * **Rejected** - The promise's *action* failed
    * This results in the `reject` callback being invoked
  * **Pending** - The promise's *action* is ongoing (hasn't fulfilled or rejected yet)
  * **Settled** - The promise's *action* has finished (is either fulfilled or rejected)
* Promise-like objects are sometimes referred to as being *thenable*, meaning that you are able to chain `.then` onto them.
  * Javascript API will treat anything with a `.then` method defined on it as *thenable*.
* P
