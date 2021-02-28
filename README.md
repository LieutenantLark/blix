# Blix — [Demo](https://voormann.github.io/blix)
A particle system built for Canvas 2D that's simple to use and customize. The main focus is performance with batch rendering, minimal color state changes with a predefined palette, object pooling with separate pools for explosions and particles to reduce garbage collection hits, efficient object sorting, and simplifying the particles' shape as they shrink.


### Basic setup
1. The particle system is initialized by calling `particles.init()`.
2. Your tick/render loop needs to include:
```js
explosions.update();
particles.draw();
```
3. Explosions can be spawned by using:
```js
const explosion = explosions.create();
explosion.init(/* X position */, /* Y position */);
```


### Customization
The basic settings can be changed in the explosion object:
```js
const explosion = {
    colors: ['#6434E9', '#2C7CE5', '#49CC5C', '#F8C421', '#FB6640', '#F82553'],
    variations: 6,
    multiplier: 8
};
```
`variations` corresponds to how many color indices present in the `colors` array, while `multiplier` decides how many particles spawn per color index (e.g. 6 * 8 = 48 particles per explosion).

How the particles behave can be changed in the Particle class' init function:
```js
init(x, y) {
    this.x = x;
    this.y = y;
    const direction = Math.random() * Math.PI * 2;
    const velocity = Math.random() * 3.5;
    this.vx = Math.cos(direction) * velocity;
    this.vy = Math.sin(direction) * velocity;
    this.wither = Math.random() * 0.007 + 0.007;
    this.radius = 2 + Math.random() * 4;
    this.dead = false;
}
```
`direction` shapes the explosion. `velocity`/`radius` gives the particles their speed and initial radius. `wither` sets the constant rate at how fast the particles' `radius` decreases. Note: the `wither` value should be randomized to spread out pooling operations.
