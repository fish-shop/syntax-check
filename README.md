<img alt="fish" src="images/fish-market.png" width="160" align="right">

# fish-shop/syntax-check

[![Tests](https://img.shields.io/github/actions/workflow/status/fish-shop/syntax-check/test.yml?branch=main&color=brightgreen&label=tests)](https://github.com/fish-shop/syntax-check/actions) [![Issues](https://img.shields.io/github/issues/fish-shop/syntax-check)](https://github.com/fish-shop/syntax-check/issues) [![Dependabot](https://img.shields.io/badge/dependabot-active-brightgreen.svg)](https://github.com/fish-shop/syntax-check/network/dependencies) [![License](https://img.shields.io/badge/license-MIT-blue)](https://opensource.org/licenses/mit-license.php) [![fish](https://img.shields.io/badge/fish-3.2.2-blue)](https://fishshell.com)

A GitHub action for syntax checking [fish shell](https://fishshell.com) files.

<hr>

Here's an example from the test workflow for [Pond](https://github.com/marcransome/pond):

<img src="example.png">

## Prerequisites

This action requires [fish shell](https://fishshell.com). You can install it using the [fish-shop/install-fish-shell](https://github.com/fish-shop/install-fish-shell) action.

## Usage

Add a `uses` step to your GitHub [workflow](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions) as shown below:

```yaml
- name: Syntax check
  uses: fish-shop/syntax-check@v2
```

By default, all files under `$GITHUB_WORKSPACE` with a `.fish` file extension are checked. To override the default behaviour, provide one or more space-separated pattern values to the `patterns` input. For example, to check all `.fish` files starting in the `src` directory and descending into subdirectories:

```yaml
- name: Syntax check
  uses: fish-shop/syntax-check@v2
  with:
    patterns: src/**.fish
```

Each pattern value may include [wildcards](https://fishshell.com/docs/current/language.html#expand-wildcard) and/or [brace expansion](https://fishshell.com/docs/current/language.html?highlight=brace+expansion#brace-expansion):

```yaml
- name: Syntax check
  uses: fish-shop/syntax-check@v2
  with:
    patterns: init.fish functions/**.fish {conf.d,completions}/**.fish tests/???-*.fish
```

> [!IMPORTANT]
> The `?` wildcard character is [deprecated](https://fishshell.com/docs/current/language.html#wildcards-globbing) and can be disabled via the `fish` feature flag `qmark-noglob`. Support for the `?` wildcard may therefore be dependent upon the version of `fish` shell in use and/or the configuration of its feature flags.

## Inputs

Configure the action using the following inputs:

| Name          | Description                            | Default               |
|---------------|----------------------------------------|-----------------------|
| `annotations` | The string value `'true'` or `'false'` indicating whether to enable [annotations](#annotations) or not | `true` |
| `patterns`    | A space-separated list of file patterns to match against when running syntax checks; each pattern may include [wildcards](https://fishshell.com/docs/current/language.html#expand-wildcard) and/or [brace expansions](https://fishshell.com/docs/current/language.html?highlight=brace+expansion#brace-expansion) | `**.fish` |
| `title`       | The title to display in the [job summary](#job-summary); can be used to distinguish multiple summaries generated from a single workflow  | `Syntax check results` |

## Outputs

The following outputs are made available to subsequent steps in a workflow:

| Name     | Description                                   |
|----------|-----------------------------------------------|
| `total`  | The total number of files syntax checked      |
| `passed` | The number of files that passed syntax checks |
| `failed` | The number of files that failed syntax checks |

## Annotations

Syntax issues identified by this action are displayed as [annotations](https://github.blog/news-insights/product-news/introducing-check-runs-and-annotations/) on the workflow summary page:

<img alt="Workflow summary annotations" src="images/annotations-workflow-summary.png" width="909">

Annotations are also displayed directly alongside the code in the 'Files changed' tab of pull requests:

<img alt="Pull request annotations" src="images/annotations-pull-request.png" width="909">

This behaviour can be disabled by setting the `annotations` input to `false`.

## Job summary

This action generates a [job summary](https://github.blog/news-insights/product-news/supercharging-github-actions-with-job-summaries/) at run-time which can be viewed from the workflow run summary page:

<img alt="Job summary" src="images/job-summary.png" width="909">

## Action versions

Use one of the following patterns when specifying the version reference for this action in your workflow (i.e. the `{ref}` value in `uses: fish-shop/syntax-check@{ref}`):

| Pattern  | Example   | Description                                                            |
|----------|-----------|------------------------------------------------------------------------|
| `vX`     | `v1`      | the latest `v1.*` release including non-breaking changes and bug fixes |
| `vX.Y`   | `v1.1`    | the latest `v1.1.*` release including bug fixes                        |
| `vX.Y.Z` | `v1.1.0`  | the `v1.1.0` release only                                              |

> [!TIP]
> The recommended pattern is `vX` (e.g. `v1`). This will ensure that the version of the action used in your workflow includes the latest non-breaking changes and bug fixes, and guarantees compatibility with previous versions of that major release number.

Using a `main` branch reference in your workflow is _not_ recommended as this branch may include breaking changes intended for the next major release.

## Other GitHub actions

A number of related composite actions are also available from the [fish-shop](https://github.com/fish-shop) 🐟. Check them out:

* [fish-shop/indent-check](https://github.com/fish-shop/indent-check) - A GitHub action for checking indentation in fish shell files
* [fish-shop/install-fish-shell](https://github.com/fish-shop/install-fish-shell) - A GitHub action for installing fish shell
* [fish-shop/install-plugin](https://github.com/fish-shop/install-plugin) - A GitHub action for installing fish shell plugins
* [fish-shop/install-plugin-manager](https://github.com/fish-shop/install-plugin-manager) - A GitHub action for installing a fish shell plugin manager
* [fish-shop/run-fishtape-tests](https://github.com/fish-shop/run-fishtape-tests) - A GitHub action for running Fishtape tests

## Acknowledgements

* This project was inspired by [fish-actions/syntax-check](https://github.com/fish-actions/syntax-check)
* Fish market icon made by [Freepik](https://www.flaticon.com/authors/freepik) from [www.flaticon.com](https://www.flaticon.com/)

## License
`fish-shop/syntax-check` is provided under the terms of the [MIT License](https://opensource.org/licenses/mit-license.php).

## Contact
Email me at [marc.ransome@fidgetbox.co.uk](mailto:marc.ransome@fidgetbox.co.uk) or [create an issue](https://github.com/fish-shop/syntax-check/issues).
