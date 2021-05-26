# fish-shop/syntax-check

[![Tests Status](https://github.com/fish-shop/syntax-check/actions/workflows/test.yml/badge.svg)](https://github.com/fish-shop/syntax-check/actions?query=workflow%3Atests) [![License](https://img.shields.io/badge/license-MIT-blue)](http://opensource.org/licenses/mit-license.php) [![fish](https://img.shields.io/badge/fish-3.2.2-blue)](https://fishshell.com) [![Issues](https://img.shields.io/github/issues/fish-shop/syntax-check)](https://github.com/fish-shop/syntax-check/issues)

A GitHub action for syntax checking [fish shell](https://fishshell.com) files.

<img src="example.png">

## Prerequisites

This action requires the [fish shell](https://fishshell.com). You can install it within jobs in your workflow using the [install-fish](https://github.com/fish-actions/install-fish) action.

## Usage

Add a suitable `uses` step to your GitHub [workflow](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions) as shown below:

```yaml
jobs:
  syntax-check:
    runs-on: ubuntu-latest
    steps:
      - name: Syntax check
        uses: fish-shop/syntax-check@1.0.1
```

By default, all files under `$GITHUB_WORKSPACE` with a `.fish` file extension are checked. To specify a different file pattern to match against provide a value for the `pattern` input. For example, to check all `.fish` files in the `src` directory of your repository:

```yaml
...
steps:
  - name: Syntax check
    uses: fish-shop/syntax-check@1.0.1
    with:
      pattern: src/**.fish
```

Multiple `pattern` values are also supported:

```yaml
...
steps:
  - name: Syntax check
    uses: fish-shop/syntax-check@1.0.1
    with:
      pattern: conf.d/**.fish functions/pond.fish completions/**.fish
```


## Acknowledgements

* This project was inspired by [fish-actions/syntax-check](https://github.com/fish-actions/syntax-check).

## License
`fish-shop/syntax-check` is provided under the terms of the [MIT License](http://opensource.org/licenses/mit-license.php).

## Contact
Email me at [marc.ransome@fidgetbox.co.uk](mailto:marc.ransome@fidgetbox.co.uk) or tweet [@marcransome](http://www.twitter.com/marcransome).
