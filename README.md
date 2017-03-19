*This project is under active development and is not stable yet.*  

# Planck.js<sup>&alpha;</sup>

Planck.js is JavaScript rewrite of Box2D physics engine for cross-platform HTML5 game and interactive application development.

**[Check out demos!](http://piqnt.com/planck.js/)**

[![Car](./doc/img/screenshot.png "Play")](http://piqnt.com/planck.js/Car)

Key motivations in development of this project are:
- Taking advantage of Box2D's efforts and achievements
- Developing readable and maintainable JavaScript code
- Optimizing the library for web and mobile platforms
- Providing a JavaScrip-friendly API

## Install

#### Download

Latest builds are available on project [releases page](https://github.com/shakiba/planck.js/releases).

#### NPM

    npm install planck-js --save

#### Bower

    bower install planck-js --save


## Getting Started

Planck.js is a physics engine and does not include any renderer by default,
however to try or learn it you could use the testebed included in this repository.

There are three ways to get started with Planck.js.

#### Easy: Use Testbed Renderer

To try your code simply add `planck-with-testbed.js` script to your HTML code and call `planck.testbed(callback)`, for example:

```html
<script src="./path/to/planck-with-testbed.js"></script>
<script>
  planck.testbed(function(testbed) {
    var world = planck.World();
    
    // rest of your code
    
    return world; // make sure you return the world
  });
</script>

```

Check out [Car example on CodePen](https://codepen.io/ashakiba/pen/yMpvrX?editors=0010) to try this approach. See [`example`](./example/) directory for more testbed usage examples.

#### Advanced: Run Testbed with Live Build and Examples

Another way to use testbed and try included examples (in [`example`](./example/) directory) is running testbed with live build locally:

1. Install `git`, `npm` and `bower`

1. Clone or download this repository

1. Install npm and bower dependencies:

        npm install
        bower install

1. Run testbed and open it in your web browser (see command-line output for URL to open):

        npm run testbed



#### Advanced: Use Your Own Renderer

To write and use your own renderer, all you need to do is calling `world.step(hz)` in each frame and then iterating over world entities to draw or update them.
You may also want to listen to world events to remove objects which are removed from the world.

```javascript

var world = planck.World();

world.on('remove-fixture', function(fixture) {
  // remove fixture from ui
});

window.requestAnimationFrame(function() {
  world.step(1 / 60);
  for (var body = world.getBodyList(); body; body = body.getNext()) {
    for (var fixture = body.getFixtureList(); fixture; fixture = fixture.getNext()) {
      // add or update fixture
    }
  }
});

```

## Usage Manual

Planck.js public API closely follows Box2D API, with following differences:

- `b2` prefix is dropped from class names, for example `b2World` is now available as `planck.World`.
- Method names are converted from UpperCamelCase to lowerCamelCase.
- Definition classes/objects (BodyDef, FixtureDef, etc.) are replaced by inline JavaScript objects (`{}`).
- Shapes are made immutable and are not cloned when used to create fixtures.
- `World#on(eventName, listenerFn)` and `World#off(eventName, listenerFn)` are added to add and remove event listeners. Currently supported events are:
    - `'contact-begin'`
    - `'contact-end'`
    - `'pre-solve'`
    - `'post-solve'`
    - `'joint-removed'`
    - `'fixture-removed'`
    - `'body-removed'`


To learn Box2D please see Box2D <a href="http://box2d.org/documentation/" target="_blank">Manual</a> and <a href="https://github.com/erincatto/Box2D/wiki/FAQ" target="_blank">FAQ</a>.

## Architecture

Planck.js includes Box2D algorithms without modification and its internal architecture and public API are very similar to Box2D.
However some [changes](./CHANGES.md) and refactoring are made during rewrite to address differences between C++ and JavaScript.


## References

[**Box2D**](http://box2d.org/) is a popular C++ 2D rigid-body physics engine created by [Erin Catto](https://twitter.com/erin_catto). Box2D is used in several popular games, such as Angry Birds, Limbo and Crayon Physics, as well as game development tools and libraries such as Apple's SpriteKit.

[iforce2d](https://www.iforce2d.net/b2dtut/) website includes a collection of helpful tutorials and resources to learn Box2D.


## License

Planck.js is [available under the zlib license](./LICENSE.txt).