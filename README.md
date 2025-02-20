# lcov_ex

Test coverage module to generate a `lcov.info` file for an Elixir project.

The docs can be found at [https://hexdocs.pm/lcov_ex](https://hexdocs.pm/lcov_ex).

## Why

Many test coverage tools use [`lcov`](https://manpages.debian.org/stretch/lcov/geninfo.1.en.html#FILES) files as an input to generate reports.

You can use it as I do to watch coverage progress in the following editors:

- VSCode:
  - Using the [Coverage Gutters](https://github.com/ryanluker/vscode-coverage-gutters) extension.
  - Using the [Koverage](https://marketplace.visualstudio.com/items?itemName=tenninebt.vscode-koverage) extension (add "cover" in settings as coverage folder, or output the report to the "coverage" folder, see below).
- Atom, using the [lcov-info](https://atom.io/packages/lcov-info) extension (it requires you to change the output folder to "coverage", see below).

Please let me know if you made it work in your previously unlisted favorite editor. Or, if you're really nice, just add it to this list yourself :slightly_smiling_face:

## Installation

Add to your dependencies:

```elixir
  def deps do
    [
      {:lcov_ex, "~> 0.2", only: [:dev, :test], runtime: false}
    ]
  end
```

## Usage

```shell
mix lcov
```

File should be created at `./cover/lcov.info` by default.

To run silently use the `--quiet` option:

```shell
mix lcov --quiet
```

To output the file to a differnt folder, use the `--output` option:

```shell
mix lcov --output coverage
...
Coverage file successfully created at coverage/lcov.info
```

### As test coverage tool

Alternatively, you can set up `LcovEx` as your test coverage tool in your project configuration:

```elixir
  def project do
    [
      ...
      test_coverage: [tool: LcovEx, output: "cover"],
      ...
    ]
```

And then, run with:

```shell
mix test --cover
```

The `output` option indicates the output folder for the generated file.

Optionally, the `ignore_paths` option can be a list of prefixes to ignore when generating the coverage report.

```elixir
  def project do
    [
      ...
      test_coverage: [tool: LcovEx, output: "cover", ignore_paths: ["test/"]]
      ...
    ]
```

## TODOs

- Add missing `FN` lines, for the sake of completion.
