---
name: sg-file
description: Read a file from Sourcegraph and summarize it.
---

# Sourcegraph File Read

Use `read_file` to fetch Sourcegraph file contents based on input after `/sourcegraph:sg-file`.

Interpret input in one of these forms:

- `repo path` (default revision)
- `repo rev path`

After reading the file:

1. Summarize what the file does.
2. Call out key exported symbols or entry points.
3. Mention related files that should be read next.
