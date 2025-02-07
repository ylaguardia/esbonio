v0.8.0 - 2021-11-26
-------------------

Features
^^^^^^^^

- The language server now respects the project's ``default_role`` setting. (`#72 <https://github.com/swyddfa/esbonio/issues/72>`_)
- Initial implementation of the ``textDocument/documentSymbols`` request which for example, powers the "Outline" view in VSCode.
  Currently only section headers are returned. (`#242 <https://github.com/swyddfa/esbonio/issues/242>`_)
- The ``esbonio.sphinx.buildDir`` option now supports ``${workspaceRoot}`` and ``${confDir}`` variable expansions (`#259 <https://github.com/swyddfa/esbonio/issues/259>`_)


Fixes
^^^^^

- Role target ``CompletionItems`` now preserve additional cross reference modifiers like ``!`` and ``~`` (`#211 <https://github.com/swyddfa/esbonio/issues/211>`_)
- Intersphinx projects are now only suggested if they contain targets relevant to the current role. (`#244 <https://github.com/swyddfa/esbonio/issues/244>`_)
- Variables are now properly substituted in diagnostic messages. (`#246 <https://github.com/swyddfa/esbonio/issues/246>`_)


v0.7.0 - 2021-09-13
-------------------

Features
^^^^^^^^

- Add initial goto definition support.
  Currently only support definitions for ``:ref:`` and ``:doc:`` role targets. (`#209 <https://github.com/swyddfa/esbonio/issues/209>`_)


Fixes
^^^^^

- Completion suggestions for ``:option:`` targets now insert text in the correct format (``<progname> <option>``) (`#212 <https://github.com/swyddfa/esbonio/issues/212>`_)
- Diagnostics are now correctly cleared on Windows (`#213 <https://github.com/swyddfa/esbonio/issues/213>`_)
- Completion suggestions are no longer given in the middle of Python code. (`#215 <https://github.com/swyddfa/esbonio/issues/215>`_)
- ``CompletionItems`` should no longer corrupt existing text when selected. (`#223 <https://github.com/swyddfa/esbonio/issues/223>`_)


Misc
^^^^

- Updated ``pygls`` to ``v0.11.0`` (`#218 <https://github.com/swyddfa/esbonio/issues/218>`_)


v0.6.2 - 2021-06-05
-------------------

Fixes
^^^^^

- The language server now correctly handles windows file URIs when determining Sphinx's
  build directory. (`#184 <https://github.com/swyddfa/esbonio/issues/184>`_)
- Role and role target completions are now correctly generated when the role
  is being typed within parenthesis e.g. ``(:kbd:...`` (`#191 <https://github.com/swyddfa/esbonio/issues/191>`_)
- Path variables like ``${confDir}`` and ``${workspaceRoot}`` are now properly expanded
  even when there are no additional path elements. (`#208 <https://github.com/swyddfa/esbonio/issues/208>`_)


Misc
^^^^

- The cli arguments ``--cache-dir``, ``--log-filter``, ``--log-level`` and
  ``--hide-sphinx-output`` have been replaced with the configuration
  parameters ``esbonio.sphinx.buildDir``, ``esbonio.server.logFilter``,
  ``esbonio.logLevel`` and ``esbonio.server.hideSphinxOutput`` respectively (`#185 <https://github.com/swyddfa/esbonio/issues/185>`_)
- The language server's startup sequence has been reworked. Language clients are now
  required to provide configuration parameters under the ``initializationOptions`` field
  in the ``initialize`` request. (`#192 <https://github.com/swyddfa/esbonio/issues/192>`_)
- The language server will now send an `esbonio/buildComplete` notification to
  clients when it has finished (re)building the docs. (`#193 <https://github.com/swyddfa/esbonio/issues/193>`_)
- An entry for ``esbonio`` has been added to the ``console_scripts``
  entry point, so it's now possible to launch the language server by
  calling ``esbonio`` directly (`#195 <https://github.com/swyddfa/esbonio/issues/195>`_)


v0.6.1 - 2021-05-13
-------------------

Fixes
^^^^^

- Intersphinx projects are now only included as completion suggestions for roles
  which target object types in a project's inventory. (`#158 <https://github.com/swyddfa/esbonio/issues/158>`_)
- Fix the uri representation of Windows paths when reporting diagnostics (`#166 <https://github.com/swyddfa/esbonio/issues/166>`_)
- The language server now attempts to recreate the Sphinx application if the user
  updates a broken ``conf.py``. (`#169 <https://github.com/swyddfa/esbonio/issues/169>`_)
- The language server no longer crashes if clients don't send the ``esbonio.sphinx``
  configuration object (`#171 <https://github.com/swyddfa/esbonio/issues/171>`_)
- Docstrings from Sphinx and Docutils' base directive classes are no longer
  included in completion suggestions as they are not useful. (`#178 <https://github.com/swyddfa/esbonio/issues/178>`_)
- Sphinx build time exceptions are now caught and reported (`#179 <https://github.com/swyddfa/esbonio/issues/179>`_)
- Fix ``Method not found: $/setTrace`` exceptions when running against VSCode (`#180 <https://github.com/swyddfa/esbonio/issues/180>`_)


v0.6.0 - 2021-05-07
-------------------

Features
^^^^^^^^

- The Language Server will now offer filepath completions for the ``image``,
  ``figure``, ``include`` and ``literalinclude`` directives as well as the
  ``download`` role. (`#34 <https://github.com/swyddfa/esbonio/issues/34>`_)
- Language clients can now override the default ``conf.py`` discovery mechanism
  by providing a ``esbonio.sphinx.confDir`` config option. (`#62 <https://github.com/swyddfa/esbonio/issues/62>`_)
- Language clients can now override the assumption that Sphinx's ``srcdir``
  is the same as its ``confdir`` by providing a ``esbonio.sphinx.srcDir``
  config option. (`#142 <https://github.com/swyddfa/esbonio/issues/142>`_)


Fixes
^^^^^

- The Language Server no longer throws an exception while handling errors raised
  during initialization of a Sphinx application. (`#139 <https://github.com/swyddfa/esbonio/issues/139>`_)
- The Language Server now correctly offers completions for ``autoxxx`` directive options
  (`#100 <https://github.com/swyddfa/esbonio/issues/100>`_)


Misc
^^^^

- Upgrage pygls to v0.10.x (`#144 <https://github.com/swyddfa/esbonio/issues/144>`_)


v0.5.1 - 2021-04-20
-------------------

Fixes
^^^^^

- Pin ``pygls<0.10.0`` to ensure installs pick up a compatible version (`#147 <https://github.com/swyddfa/esbonio/issues/147>`_)


v0.5.0 - 2021-02-25
-------------------

Features
^^^^^^^^

- The language server now reports invalid references as diagnostics (`#57 <https://github.com/swyddfa/esbonio/issues/57>`_)
- Add ``--log-level`` cli argument that allows Language Clients to
  control the verbosity of the Language Server's log output. (`#87 <https://github.com/swyddfa/esbonio/issues/87>`_)
- Directive completions are now domain aware. (`#101 <https://github.com/swyddfa/esbonio/issues/101>`_)
- Role and role target completions are now domain aware. (`#104 <https://github.com/swyddfa/esbonio/issues/104>`_)
- Intersphinx completions are now domain aware (`#106 <https://github.com/swyddfa/esbonio/issues/106>`_)
- Add ``log-filter`` cli argument that allows Language Clients to choose
  which loggers they want to recieve messages from. Also add
  ``--hide-sphinx-output`` cli argument that can suppress Sphinx's build
  log as it it handled separately. (`#113 <https://github.com/swyddfa/esbonio/issues/113>`_)
- Add ``-p``, ``--port`` cli arguments that start the Language Server in
  TCP mode while specifying the port number to listen on. (`#114 <https://github.com/swyddfa/esbonio/issues/114>`_)
- Add ``--cache-dir`` cli argument that allows Language Clients to
  specify where cached data should be stored e.g. Sphinx's build output. (`#115 <https://github.com/swyddfa/esbonio/issues/115>`_)


Fixes
^^^^^

- The language server now reloads when the project's ``conf.py`` is modified (`#83 <https://github.com/swyddfa/esbonio/issues/83>`_)
- ``$/setTraceNotification`` notifications from VSCode no longer cause exceptions to be thrown
  in the Language Server. (`#91 <https://github.com/swyddfa/esbonio/issues/91>`_)
- Consistency errors are now included in reported diagnostics. (`#94 <https://github.com/swyddfa/esbonio/issues/94>`_)
- Ensure ``:doc:`` completions are specified relative to the project root. (`#102 <https://github.com/swyddfa/esbonio/issues/102>`_)


v0.4.0 - 2021-02-01
-------------------

Features
^^^^^^^^

- Directive option completions are now provided
  within a directive's options block (`#36 <https://github.com/swyddfa/esbonio/issues/36>`_)
- For projects that use ``interpshinx`` completions
  for intersphinx targets are now suggested when available (`#74 <https://github.com/swyddfa/esbonio/issues/74>`_)


Fixes
^^^^^

- Regex that catches diagnostics from Sphinx's
  output can now handle windows paths. Diagnostic reporting now sends a
  proper URI (`#66 <https://github.com/swyddfa/esbonio/issues/66>`_)
- Diagnostics are now reported on first startup (`#68 <https://github.com/swyddfa/esbonio/issues/68>`_)
- Fix exception that was thrown when trying to find
  completions for an unknown role type (`#73 <https://github.com/swyddfa/esbonio/issues/73>`_)
- The server will not offer completion suggestions outside of
  a role target (`#77 <https://github.com/swyddfa/esbonio/issues/77>`_)


v0.3.0 - 2021-01-27
-------------------

Features
^^^^^^^^

- Errors in Sphinx's build output are now parsed and published
  to the LSP client as diagnostics (`#35 <https://github.com/swyddfa/esbonio/issues/35>`_)
- Directive completions now include a snippet that
  prompts for any required arguments (`#58 <https://github.com/swyddfa/esbonio/issues/58>`_)


Fixes
^^^^^

- Errors encountered when initialising Sphinx are now caught and the language
  client is notified of an issue. (`#33 <https://github.com/swyddfa/esbonio/issues/33>`_)
- Fix issue where some malformed ``CompletionItem`` objects were
  preventing completion suggestions from being shown. (`#54 <https://github.com/swyddfa/esbonio/issues/54>`_)
- Windows paths are now handled correctly (`#60 <https://github.com/swyddfa/esbonio/issues/60>`_)
- Server no longer chooses ``conf.py`` files that
  are located under a ``.tox`` or ``site-packages`` directory (`#61 <https://github.com/swyddfa/esbonio/issues/61>`_)


v0.2.1 - 2020-12-08
-------------------

Fixes
^^^^^

- Directives that are part of the ``std`` or ``py`` Sphinx domains
  will now be included in completion suggestions (`#31 <https://github.com/swyddfa/esbonio/issues/31>`_)


v0.2.0 - 2020-12-06
-------------------

Features
^^^^^^^^

- Python log events can now published to Language Clients (`#27 <https://github.com/swyddfa/esbonio/issues/27>`_)
- Sphinx's build output is now redirected to the LSP client as log
  messages. (`#28 <https://github.com/swyddfa/esbonio/issues/28>`_)
- Suggest completions for targets for a number of roles from the
  `std <https://www.sphinx-doc.org/en/master/usage/restructuredtext/domains.html#the-standard-domain>`_
  and `py <https://www.sphinx-doc.org/en/master/usage/restructuredtext/domains.html#the-python-domain>`_
  domains including ``ref``, ``doc``, ``func``, ``meth``, ``class`` and more. (`#29 <https://github.com/swyddfa/esbonio/issues/29>`_)


Fixes
^^^^^

- Fix discovery of roles so that roles in Sphinx domains are used and
  that unimplemented ``docutils`` roles are not surfaced. (`#26 <https://github.com/swyddfa/esbonio/issues/26>`_)


v0.1.2 - 2020-12-01
-------------------

Misc
^^^^

- Use ``ubuntu-20.04`` for Python builds so that the correct version of ``pandoc`` is
  available (`#25 <https://github.com/swyddfa/esbonio/issues/25>`_)


v0.1.1 - 2020-12-01
-------------------

Misc
^^^^

- Ensure ``pandoc`` is installed to fix the Python release builds (`#24 <https://github.com/swyddfa/esbonio/issues/24>`_)


v0.1.0 - 2020-12-01
-------------------

Features
^^^^^^^^

- The language server can now offer completion suggestions for ``directives`` and
  ``roles`` (`#23 <https://github.com/swyddfa/esbonio/issues/23>`_)


0.0.6 - 2020-11-21
------------------

Misc
^^^^

- Add ``--version`` option to the cli that will print the version number and exit. (`#11 <https://github.com/swyddfa/esbonio/issues/11>`_)


0.0.5 - 2020-11-20
------------------

Misc
^^^^

- Update build pipeline to use ``towncrier`` to autogenerate release notes
  and changelog entries (`#5 <https://github.com/swyddfa/esbonio/issues/5>`_)
