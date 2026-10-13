# maki-swatches

The shared color list for [maki](https://github.com/tontinton/maki)
plugins: one canonical set of swatch names (`red`, `cyan`, `teal`, ...)
for user-facing color pickers, with `resolve(name)` answering `#rrggbb`
so a caller paints with the hex directly.

`swatch_list()` layers the running theme's palette on top when the build
exposes `maki.ui.get_theme_palette`; otherwise the canonical list is the
list. Entries that share one hex merge into a single row labeled with
every name. Hex is never an input.

## This is a library to vendor, not a package to install

maki packages cannot `require` each other — a package's `require` is
sandboxed to its own `lua/` directory — so a consuming package copies
`swatches.lua` in:

```sh
git clone https://github.com/amirs-maki-plugins/maki-swatches
cp maki-swatches/lua/swatches.lua your-package/lua/
```

Installing this repo with `maki.pack.add` does nothing: it registers no
tool or command, and nothing outside it can reach its modules.

## Tests

`lua/swatches_spec.lua` holds the behavior contract (pure Lua, no maki
needed):

```sh
lua swatches_spec.lua   # or run it through your own spec runner
```

## Consumers

- [maki-progress-bar](https://github.com/amirs-maki-plugins/maki-progress-bar) — vendored copy
