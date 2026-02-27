# INGR File Format

- **Extension:**: `.ingr`
- **Purpose:** Compact, deterministic, self-describing, Git-friendly fixed-line record format.

## Links

 - [INGR File Format Specifiaction](https://github.com/ingr-io/ingr-file-format)
 
 # Summary

`.ingr` is a self-describing, deterministic, fixed-line record format:

- Line 1: `# https://INGR.io | {recordset_name}: $ID, col2, col3, ...`
- Lines 2…(end-N): `N` JSON-encoded values per record, one value per line
- First footer line: `# {N} records` (required, with `\n` unless last line)
- Additional footer lines: optional `#`-prefixed lines (e.g. `# sha256:{hex}`)
- No record delimiters
- Optimised for simplicity and Git friendliness

### Example (fields: `$ID`, `name`, `age`)

```
# https://INGR.io people: $ID, name, age
"john"
"John Doe"
35
"jane"
"Jane Smith"
29
# 2 records
# sha256:3a7bd3e2360a3d80...
```

Parsed as:

| $ID  | name       | age |
|------|------------|-----|
| john | John Doe   | 35  |
| jane | Jane Smith | 29  |
