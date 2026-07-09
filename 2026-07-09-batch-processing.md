# Batch Processing

Batch processing in Claude Code lets you run the same operation across many files, tasks, or inputs without manually triggering each one. Instead of asking Claude to handle one file at a time, you can describe a pattern and let it iterate — renaming, refactoring, or analyzing dozens of items in a single session. This is especially powerful when combined with shell loops or Claude's ability to read a list of targets from a file or command output.

## Copy-Pasteable Example

```bash
# Batch rename all .jpeg files to .jpg in the current directory
for f in *.jpeg; do
  claude "Rename $f to ${f%.jpeg}.jpg and update any imports referencing it"
done

# Or give Claude a manifest and let it work through it
ls src/components/*.tsx | claude "Audit each of these files for missing aria-label attributes and fix them"
```

You can also pass a newline-separated list directly in a prompt:

```
Refactor each of the following files to use named exports instead of default exports:
- src/utils/format.ts
- src/utils/validate.ts
- src/utils/parse.ts
```

## Try It Yourself

Pick a folder with 3–5 similar files (e.g., React components or Python modules). Ask Claude: *"Add a JSDoc comment to every exported function in each of these files: [list them]."* Watch how it works through them sequentially, maintaining context between edits.
