# The Two Pillars of JavaScript
https://medium.com/javascript-scene/the-two-pillars-of-javascript-ee6f3281e7f3#.qc5i0rzho

## JavaScript's two main paradigms

* Prototypal Inheritance (objects without classes, and prototype delegation, aka OLOO - Objects Linking to Other Objects)
* Functional Programming (enabled by lambdas with closures)

### Constructors

Constructors violate the open/close principle because they couple all callers to the details of how your object gets instantiated.

If you return an arbitrary object from a constructor function, it will break your prototype links, and the 'this' keyword will no long be bound to the new object instance in the constructor. It's also less flexible than a real factory function because you can't use 'this' at all in the factory.

Constructors that aren't running in strict mode can be dangerous. If a caller forgets 'new' and you're not using strict mode or ES6 classes, anything you assign to 'this' will pollute the global namespace.

In JavaScript, factory functions are simply constructor functions minus the 'new' requirement, global pollution danger and awkward limitations.

JavaScript doesn't need constructor functions because any function can return a new object. With dynamic object extension, object literals and 'Object.create()', we have everything we need - with none of the mess. And 'this' behaves just like it does in any other function.

#### The Gorilla and Banana Problem

“The problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.” ~ Joe Armstrong

#### The Tight Coupling Problem

The coupling between a child class and its parent is the tightest form of coupling in OO design. That’s the opposite of reusable, modular code.

#### The Duplication by Necessity Problem

The obvious solution to taxonomy troubles is to go back in time, build up new classes with subtle differences by changing up what inherits from what — but it’s too tightly coupled to properly extract and refactor. You end up duplicating code instead of reusing it. You violate the DRY principle.

The `class` keyword will probably be the most harmful feature in JavaScript.

#### The Fallout

These problems have a multiplying effect as your application grows, and eventually, the only solution is to rewrite the application from scratch or scrap it entirely.

* You can use Stampit
* You can not use 'new' and 'this' at all and opt for an entirely functional approach to code reuse. All functions are stateless bags of functions, or data-only objects, with no methods.
* You can make a better use of JavaScript modules an alternative to inheritance (npm and ES6 modules with Browserify or WebPack). or simply cloning objects by copying properties from a source object to a new object (e.g. `Object.assign()`, `$.extend()`, `_.extend()`, etc…).
* The copy mechanism is another form of prototypal inheritance. Sources of clone properties are a specific kind of prototype called exemplar prototypes, and cloning an exemplar prototype is known as concatenative inheritance.

“Program to an interface, not an implementation,” and “favor object composition over class inheritance.”

Douglas Crockford got Object.create() added to the language so he wouldn’t have to use `new`.

### Good Code is Simple

#### As you strip constructors and classical inheritance out of JavaScript, it:

* Gets simpler (Easier to read and to write. No more wrong design taxonomies.)
* Gets more flexible (Switch from new instances to recycling object pools or proxies? No problem.)
* Gets more powerful & expressive (Inherit from multiple ancestors? Inherit private state? No problem.)

#### Closures

Like objects, closures are a mechanism for containing state. In JavaScript, a closure is created whenever a function accesses a variable defined outside the immediate function scope. To create closures just define a function inside another function, and expose the inner function, either by returning it, or passing it into another function. The variables used by the inner function will be available to it, even after the outer function has finished running.

You can use closures to create data privacy in JavaScript using a factory function:

```JavaScript
var counter = function counter() {
    var count = 0;
    return {
        getCount: function getCount() {
            return count;
        },
        increment: function increment() {
            count += 1;
        }
    }
}
```
