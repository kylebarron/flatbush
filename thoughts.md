Is there still interest in this? If it would be considered, I'd consider attempting a PR. My general thoughts would be:

- Have a flag on the class for whether the class is point-only or not.
- Change the computed `nodeByteSize` to be 2-per-node for point data https://github.com/mourner/flatbush/blob/4ab68d7e11607dba0e814efe50fb3583c69f90d6/index.js#L68
- Add an `addPoint` method that takes only `x` and `y` as arguments
- Update `add` to throw if `this.onlyPoints` is `true` (or maybe only throw if `minX !== maxX` and `minY !== maxY`).
- Updates to `finish` to ensure correct sorting for point data. ([I know...](https://knowyourmeme.com/photos/572078-how-to-draw-an-owl) but seems doable at a glance and left to explore fully in a pr)
- Bump the serialized format version number https://github.com/mourner/flatbush/blob/4ab68d7e11607dba0e814efe50fb3583c69f90d6/index.js#L4. We might also have to allocate an extra byte in the header so that there's a way to recollect whether the specified buffer only contains points or not (or if we assume the buffer is always valid input, I suppose you could check whether the length of the buffer matches what you'd expect with either 2-item or 4-item boxes?)
