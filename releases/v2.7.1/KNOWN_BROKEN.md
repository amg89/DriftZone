# ⚠️ KNOWN BROKEN VERSION

This release (v2.7.1) contains a JavaScript syntax error in the Inventory rendering
code (a nested template literal backtick that breaks the entire `<script>` tag).

**Symptom:** App fails to load entirely — blank tabs, nothing clickable.

**Fixed in:** v2.7.2 (see CHANGELOG.md)

**Do not roll back to this version.** This folder is kept only for historical
record-keeping. If you need a version before the recipe-stock fix, use v2.7.0
instead and re-apply needed changes manually, or jump straight to v2.7.2+.
