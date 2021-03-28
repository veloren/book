# ECS

Veloren uses an Entity Component System (ECS). This is a relatively new paradigm in game engine development that
competes against traditional object-oriented design models that make heavy use of hierarchy, inheritance, and
polymorphism. It encourages game developers to design data structures in a way that allows for efficient batch
processing of data on modern CPU architectures with deep caches by storing batchable data contiguously in memory.

Traditionally, the representation of entities within a game are done like so:

```rust
struct Entity {
    position: Vec3<f32>,
    velocity: Vec3<f32>,
}
```

When representing multiple entities, it's common to use an array-like data structure.

```rust
struct World {
    entities: Vec<Entity>,
}
```

However, this comes with problems. Modern CPUs have deep caches, meaning that they are significantly faster at accessing
memory that is closer in the address space to memory they have already accessed. The most efficient storage formats pack
data to be processed very close together in memory. Our current representation looks like the following:

```
| Entity 0            | Entity 1            | Entity 2            |
|---------------------|---------------------|---------------------|
| position | velocity | position | velocity | position | velocity |
```

Let us imagine a 'typical' operation that we'd like to perform: applying gravity to the entities. This involves adding
`9.81` in vertical velocity to each of the entities. Unfortunately, the access pattern of this operation involves
touching each `velocity` field, but skipping each `position` field. These gaps in our data make the operation slower. In
technical jargon, we call this a lack of 'cache coherency'.

All is not lost.

A design pattern you might have heard of is called Struct Of Arrays, or SOA. It suggests that instead of packing the
data associated with each entity together in one place, we should instead group data according to its purpose.

```rust
struct World {
    positions: Vec<Vec3<f32>>,
    velocities: Vec<Vec3<f32>>,
}
```

Now our representation is much more densely packed and our application of gravity to entities is more efficient because
we no longer need to skip over the position data while iterating through entity velocities.

```
| Entity 0 | Entity 1 | Entity 2 |     | Entity 0 | Entity 1 | Entity 2 |
|----------|----------|----------| ... |----------|----------|----------|
| position | position | position |     | velocity | velocity | velocity |
```

ECS is this idea taken to its logical conclusion: entities as associated but separate collections of components, with
each type of component stored in its own distinct storage buffer. This approach comes with more advantages too: because
components are stored separately, it is easy and fast to add or remove components from an entity as the game is running,
thereby altering the behaviour of the entity and its capabilities. This is a remarkably powerful technique and allows
for what amount to the ability to radically alter the behaviour of the game and the entities within it while the game is
running and without sacrificing performance.

The specific ECS crate that Veloren uses is [SPECS](https://github.com/amethyst/specs/). You can read more about ECS and
the specifics of how SPECS works [here](https://specs.amethyst.rs/docs/tutorials/). If you're looking to work on
Veloren, I strongly recommend reading this resource from cover to cover (it's quite short).
