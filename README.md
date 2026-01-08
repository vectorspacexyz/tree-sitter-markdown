# tree-sitter-markdown no-indented-code-blocks fork

In this fork I merely removed indented code blocks from the grammar.

## Notes
```
git clone https://github.com/tree-sitter-grammars/tree-sitter-markdown.git
cd tree-sitter-markdown
```

Indented code blocks was removed by deleting every instance of it's mention
(searching "indented") in grammar.js and scanner.c files. Once that's done,
do:

```
tree-sitter generate src/grammar.json
tree-sitter build
```

This creates a `markdown.so` file. Find the absolute path to that file by
running `realpath markdown.so` and copy it to your clipboard. To test it out in
neovim add this in your `init.lua`, replacing the path variable value with the
one you just just copied:

```lua
vim.treesitter.language.add('markdown', {
  path = '/home/vector/admin/tree-sitter-markdown/tree-sitter-markdown/markdown.so'
})
```
