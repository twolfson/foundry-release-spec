# foundry-release-spec

Specification for [foundry][] release tools

[foundry]: https://github.com/twolfson/foundry

This is intended to serve as documentation for consistency between [foundry][] release tool.

## Documentation
A [foundry][] release tool is a CLI that exposes the following commands.

It is expected that [foundry][] will run commands in the order:

1. update-files
2. commit
3. register
4. publish

### Framework
For convenience, we have written a framework called [foundry-release-base][]. This will alleviate the majority of the CLI integration.

// TODO: Build foundry-release-base and link it

### `--spec-version`
Semver string for the current version of `foundry-release-spec` it is supporting. This can be determined by looking at this repo's latest `git tag`.

https://github.com/twolfson/foundry-release-spec/tags

```bash
$ # Example
$ foundry-release-my-plugin --spec-version
1.0.0
```

### `update-files <version> <message>`
Command that adjusts the package contents (e.g. bump `version` in `package.json`, add to `CHANGELOG`).

- version `String` - Semantic version to adjust the package to
    - Semantic version documentation can be found at http://semver.org/
- message `String` - Short description about release (comparable to `git commit's -m`)

`stdin`, `stdout`, and `stderr` will be piped to users when `foundry` is running. Please include any user-specific information there.

To denote failures, please exit with a non-zero exit code.

```bash
$ # Example
$ foundry-release-my-plugin updates-files "1.0.0" "Release 1.0.0"
```

### `commit <version> <message>`
Command that commits any updates to the package's version control (e.g. `git commit`).

`version`, `message` and stdio are the same format as in `update-files`.

```bash
$ # Example
$ foundry-release-my-plugin commit "1.0.0" "Release 1.0.0"
```

### `register <version> <message>`
Command that registers package with its registry (e.g. `bower register`, `python setup.py register`).

`version`, `message` and stdio are the same format as in `update-files`.

```bash
$ # Example
$ foundry-release-my-plugin register "1.0.0" "Release 1.0.0"
```

### `publish <version> <message>`
Command that publishes package to its registry (e.g. `npm publish`).

`version`, `message` and stdio are the same format as in `update-files`.

```bash
$ # Example
$ foundry-release-my-plugin publish "1.0.0" "Release 1.0.0"
```

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
