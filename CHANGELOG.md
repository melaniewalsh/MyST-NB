# Change Log

## 0.10.0 - 2020-08-28

⬆️ UPGRADE: jupyter-sphinx v0.3, jupyter-cache v0.4.1 and nbclient v0.5.
These upgrades allow for full Windows OS compatibility, and improve the stability of notebook execution on small machines.

👌 IMPROVE: Formatting of stderr is now similar to stdout, but with a slight red background.

🧪 TESTS: Add Windows CI

## 0.9.2 - 2020-08-27

⬆️ UPGRADE: myst-parser patch version, to ensure a few new features and bug fixes are incorporated (see its [CHANGELOG.md](https://github.com/executablebooks/MyST-Parser/blob/master/CHANGELOG.md))

## 0.9.1 - 2020-08-24

More configuration!

- ✨ NEW: Add stderr global configuration: `nb_output_stderr`
  (see [removing stderr](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#removing-stdout-and-stderr))
- ✨ NEW: Add `nb_render_key` configuration
  (see [formatting outputs](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#images))
- 🐛 FIX: `auto` execution not recognising (and skipping) notebooks with existing outputs

## 0.9.0 - 2020-08-24

This versions see's many great changes; utilising the ⬆️ upgrade to `myst-parser=v0.12`
and accompanying ⬆️ upgrade to `sphinx=v3`,
as well as major refactors to the execution ([#236](https://github.com/executablebooks/MyST-NB/commit/2bc0c11cedbad6206f70546819fad85d779ce449)) and code output rendering ([#243](https://github.com/executablebooks/MyST-NB/commit/04f3bbb928cf1794e140de6a919fb58578753300)).
Plus much more configuration options, to allow for a more configurable workflow (the defaults work great as well!).

Below is a summary of the changes, and you can also check out many examples in the documentation, <https://myst-nb.readthedocs.io/>,
and the MyST-Parser Changelog for all the new Markdown parsing features available: <https://github.com/executablebooks/MyST-Parser>.

### New ✨

- Custom notebook formats:

  Configuration and logic has been added for designating additional file types to be converted to Notebooks, which are then executed & parsed in the same manner as regular Notebooks.
  See [Custom Notebook Formats](https://myst-nb.readthedocs.io/en/latest/examples/custom-formats.html) for details.

- Allow for configuration of render priority (per output format) with `nb_render_priority`.

- The code cell output renderer class is now loaded from an entry-point, with a configurable name,
  meaning that anyone can provide their own renderer subclass.
  See [Customise the render process](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#customise-the-render-process) for details.

- Assignment of metadata tags `remove-stdout` and `remove-stderr` for removal of the relevant outputs ([see here](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#removing-stdout-and-stderr))

- Render `text/markdown` MIME types with an integrated CommonMark parser ([see here](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#markdown)).

- Add code output image formatting, *via* cell metadata, including size, captions and labelling ([see here](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#images)).

- Notebook outputs ANSI lexer which is applied to stdout/stderr and text/plain outputs, and is configurable *via* `nb_render_text_lexer` ([see here](https://myst-nb.readthedocs.io/en/latest/use/formatting_outputs.html#ansi-outputs)).

- Capture execution data in sphinx env, which can be output into the documentation, with the `nb-exec-table` directive. See [Execution statistics](https://myst-nb.readthedocs.io/en/latest/use/execute.html#execution-statistics) for details.

### Improved 👌

- Standardise auto/cache execution

    Both now call the same underlying function (from `jupyter-cache`) and act the same.
    This improves `auto`, by making it output error reports and not raising an exception on an error.
    Additional config has also been added: `execution_allow_errors` and `execution_in_temp`.
    As for for `timeout`, `allow_errors` can also be set in the notebook `metadata.execution.allow_errors`
    This presents one breaking change, in that `cache` will now by default execute in a the local folder as the CWD (not a temporary one).

### Fixed 🐛

- Code cell source code is now assigned the correct lexer when using custom kernels ([39c1bb9](https://github.com/executablebooks/MyST-NB/commit/39c1bb99e73b35812474366f2f1760850fe40a57))

### Documented 📚

- Add example of using kernels other than Python ([676eb2c](https://github.com/executablebooks/MyST-NB/commit/676eb2c46b1ca605980180479c845b43ec64c5fb))

### Refactored ♻️

- Add more signature typing and docstrings
- Move config value validation to separate function
- Rename functions in cache.py and improve their logical flow
- Rename variable stored in sphinx environment, to share same suffix:
  - `path_to_cache` -> `nb_path_to_cache`
  - `allowed_nb_exec_suffixes` -> `nb_allowed_exec_suffixes`
  - `excluded_nb_exec_paths` -> `nb_excluded_exec_paths`
- Initial Nb output rendering:
  - Ensure source (path, lineno) are correctly propagated to `CellOutputBundleNode`
  - Capture cell level metadata in `CellOutputBundleNode`
  - New `CellOutputRenderer` class to contain render methods
  - Simplify test code, using sphinx `get_doctree` and `get_and_resolve_doctree` methods

## 0.8.5 - 2020-08-11

### Improved 👌

- Add configuration for traceback in stderr (#218)

### Fixed 🐛

- MIME render priority lookup

### Upgrades ⬆️

- myst-parser -> 0.9
- jupyter-cache to v0.3.0

### Documented 📚

- More explanation of myst notebooks (#213)
- Update contributing guide

## Contributors for previously releases

Thanks to all these contributors 🙏:

[@AakashGfude](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3AAakashGfude+updated%3A2020-03-28..2020-08-11&type=Issues) | [@akhmerov](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Aakhmerov+updated%3A2020-03-28..2020-08-11&type=Issues) | [@amueller](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Aamueller+updated%3A2020-03-28..2020-08-11&type=Issues) | [@choldgraf](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Acholdgraf+updated%3A2020-03-28..2020-08-11&type=Issues) | [@chrisjsewell](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Achrisjsewell+updated%3A2020-03-28..2020-08-11&type=Issues) | [@codecov](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Acodecov+updated%3A2020-03-28..2020-08-11&type=Issues) | [@consideRatio](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3AconsideRatio+updated%3A2020-03-28..2020-08-11&type=Issues) | [@jstac](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Ajstac+updated%3A2020-03-28..2020-08-11&type=Issues) | [@matthew-brett](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Amatthew-brett+updated%3A2020-03-28..2020-08-11&type=Issues) | [@mmcky](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Ammcky+updated%3A2020-03-28..2020-08-11&type=Issues) | [@phaustin](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Aphaustin+updated%3A2020-03-28..2020-08-11&type=Issues) | [@rossbar](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Arossbar+updated%3A2020-03-28..2020-08-11&type=Issues) | [@rowanc1](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Arowanc1+updated%3A2020-03-28..2020-08-11&type=Issues) | [@seanpue](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Aseanpue+updated%3A2020-03-28..2020-08-11&type=Issues) | [@stefanv](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Astefanv+updated%3A2020-03-28..2020-08-11&type=Issues) | [@TomDonoghue](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3ATomDonoghue+updated%3A2020-03-28..2020-08-11&type=Issues) | [@tonyfast](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Atonyfast+updated%3A2020-03-28..2020-08-11&type=Issues) | [@welcome](https://github.com/search?q=repo%3Aexecutablebooks%2FMyST-NB+involves%3Awelcome+updated%3A2020-03-28..2020-08-11&type=Issues)
