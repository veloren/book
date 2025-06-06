# Coordinate Systems

Various coordinate systems are used for different tasks throughout the codebase so it can be useful
to have a reference for how they work and relate to each other.

A not necessarily exhaustive list:

* ["world" coordinates](#world-coordinates)
* chunk coordinates
* weather sim cell coordinates
* "regions" used on the server for syncing to clients
* coordinate spaces used during rendering in voxygen
* LoD zones (see `common/src/lod.rs`)

> **Note:** This document is unfinished and details for more of these could be included.

## World coordinates

World coordinates can actually be broken down into two different kinds.

There are non-integer positions currently represented via `Vec3<f32>`, e.g. which can be used to
represent an entity position.

Then there are integer positions currently represented via `Vec3<i32>`, e.g. which can be used
for the position of a voxel in the world. The coordinates of the voxel containing a `Vec3<f32>`
point can be obtained via `.floor() as i32` on each element of the `Vec3`. Consequently, when the
integer position of a voxel is directly converted to a `Vec3<f32>`, this is located at the minimum
corner of that voxel. To obtain the center of a voxel in that space `0.5` must be added to each
element of the position.
