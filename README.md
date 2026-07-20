# tree-sitter-damask

Tree-sitter grammar for [Damask](https://github.com/JWo1F/damask) `.dmk`
templates — compile-time components for Rust.

Damask templates are HTML with a `{ … }` tag syntax, JSX-style
`<Component/>` elements, and `<slot/>`s.

## Scope

The grammar owns the markup and the tag structure: elements, attributes, the
`class` forms, and the `{ }` tag family. It deliberately does **not** parse the
Rust inside a tag or the HTML it surrounds — those are exposed as regions for
injection, so the real Rust and HTML grammars highlight them.

```
{ expr }                             expression, HTML-escaped
{@html expr}  {@render expr}         directives
{#if c}…{:else}…{/if}                conditional
{#each E as p}…{/each}               loop
{#snippet name(params)}…{/snippet}   reusable fragment
{# … #}                              comment
```

## Use

Generate the parser at ABI 14 — Zed's bundled tree-sitter cannot compile ABI 15:

```sh
tree-sitter generate --abi 14
tree-sitter test
```

The generated sources under `src/` are committed, because editors that consume
this grammar compile `parser.c` directly rather than running the CLI.

## Development

This grammar is developed in the [Damask
monorepo](https://github.com/JWo1F/damask) under
`editors/zed/grammars/tree-sitter-damask/`, alongside the language server and
Zed extension that consume it. This repository is the standalone publication of
that directory, so editors can fetch it from a repository root.

## License

MIT.
