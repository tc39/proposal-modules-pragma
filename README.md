# ECMAScript proposal: `"use module";`

## Status

This proposal is in stage 1 of [the TC39 process](https://tc39.github.io/process-document/).

## Motivation

Since the _Script_ and _Module_ syntaxes have some overlap (in particular, most modules with no `import` or `export` declarations are valid scripts), there are situations where either a host environment or simply a human reader may not be able to infer whether a piece of code is intended to be a script vs a module.

Some host environments may offer out-of-band mechanisms for specifying the mode, such as HTML attributes (`<script type=module>`), configuration parameters (`"module": "main.js"`), command-line switches (`node -m`), or file extensions (`.mjs`). However, an in-band pragma for enforcing the mode can be useful for a number of reasons:

  * **Portability:** A source file that wants to work in multiple host environments can be sure to select its mode without being sensitive to configuration parameters where it's used.
  * **Compatibility:** If a host environment like Node chooses to use file extensions to determine the mode, some content may wish to preserve existing filenames (for example, for clients that require the module by full filename) when migrating to standard modules. An in-band opt-in makes that possible.

Finally, the fact that this is a pragma means that ecosystems where there is no formal or conceptual ambiguity -- in particular, ecosystems that author entirely using modules -- do not need to pollute their source code.

## Alternatives

Today, programmers can use a programming pattern to enforce that a file is a module:

```js
export {};
```

This syntax has no effect except to force a parsing error if a host environment attempts to parse it as a script.

This is suboptimal for readability, since it does not clearly convey what its intended effect is. It is also not applicable for solving the complementary problem of enforcing that a source file is intended to be parsed as `script`.

## Specification

  * [Ecmarkup source](https://github.com/tc39/proposal-modules-pragma/blob/master/spec.html)
  * [HTML version](https://tc39.github.io/proposal-modules-pragma/)

