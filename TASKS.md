# Tasks — legacy maintenance

This is an existing, long-lived library (`tabulate/__init__.py`, ~2,900 lines). Fix the four bug reports below.

Rules
- Work only from this repository. Do NOT look up, download, or copy fixes from the upstream tabulate project,
  its issue tracker, forks, or any other online source. Diagnose the code yourself.
- Keep changes minimal and in the existing style. Do not reformat or refactor unrelated code. No new runtime dependencies.
- Add a regression test for each bug (pytest; `wcwidth` may be used in tests).
- You may change an existing test only if the requested behaviour change makes it wrong; list every such change and why.
- Run the full test suite (`python -m pytest test -q`) before finishing. Do not break existing behaviour.

Bug reports
1. **Empty table + maxheadercolwidths crashes.** `tabulate([], headers=["one", "two", "three"], maxheadercolwidths=5)`
   raises an exception instead of printing just the header and separator lines.
2. **Text wrapping hangs on wide characters.** Wrapping East-Asian wide characters (each 2 columns wide, e.g. Korean)
   into a column narrower than one character (width=1) never finishes. Each character should go on its own line.
   Wrapped lines must also never exceed the requested display width.
3. **Decimal values lose precision.** With `floatfmt=".6f"`, a `decimal.Decimal("99999998999.999980")` is printed as
   `99999998999.999985` (it is converted through float). Decimal values must be formatted exactly.
4. **asciidoc output has trailing whitespace.** Lines produced with `tablefmt="asciidoc"` end with spaces. No line of
   asciidoc output should have trailing whitespace.

Finish with: a short summary per bug (root cause + fix), the list of any existing tests you changed, and the full test output.
