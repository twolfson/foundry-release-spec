# foundry-release-spec

Specification for [foundry][] release plugins

[foundry]: https://github.com/twolfson/foundry

This is intended to serve as documentation for consistency between [foundry][] release plugins.

## Documentation
A [foundry][] release plugin should expose the following functions on its `exports`.

It is expected that [foundry][] will run the plugins in the order of:

1. setVersion
2. register
3. publish

### `exports.setVersion(params, cb)`
Optional function that adjusts the package's version (e.g. bump `package.json`).

**This is expected to detect whether the package metadata exists or not. This means it can run when the metadata store does not exist (e.g. no `package.json`).**

- params `Object` - Collection of parameters to set version based off of
    - version `String` - Semantic version to adjust the package to
        - Semantic version documentation can be found at http://semver.org/
    - message `String` - Short description about release (comparable to `git commit's -m`)
    - description `String|null` - Optional long description for release (comparable to `git commit's body`)
- cb `Function` - Error-first callback method to run when version is done being set
    - The function signature should be `(err)`

### `exports.register(params, cb)`
Optional function that registers package with its registry (e.g. `bower register`, `python setup.py register`).

**As with `exports.setVersion`, this must detect whether the package metadata exists or not.**

> Currently, this function will only be run when `0.1.0` releases occur. This should be configurable when [twolfson/foundry#7][] is resolved.

[twolfson/foundry#7]: https://github.com/twolfson/foundry/issues/7

`params` and `cb` are the same format as in `exports.setVersion`.

### `exports.publish(params, cb)`
Optional function that publishes package to its registry (e.g. `npm publish`).

**As with `exports.setVersion`, this must detect whether the package metadata exists or not.**

`params` and `cb` are the same format as in `exports.setVersion`.

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style.

## Donating
Support this project and [others by twolfson][gittip] via [gittip][].

[![Support via Gittip][gittip-badge]][gittip]

[gittip-badge]: https://rawgithub.com/twolfson/gittip-badge/master/dist/gittip.png
[gittip]: https://www.gittip.com/twolfson/

## Unlicense
As of Feb 01 2014, Todd Wolfson has released this repository and its contents to the public domain.

It has been released under the [UNLICENSE][].

[UNLICENSE]: UNLICENSE
