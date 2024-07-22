# jq-playground.nvim

> Interact with jq in Neovim, using interactive buffers

![Example screenshot](example/screenshot.png)

Like jqplay.org or Neovims builtin Treesitter playground
([`:InspectTree`](https://neovim.io/doc/user/treesitter.html#%3AInspectTree)).

## Setup

Using the default configuration with lazy.nvim as package manager:

```lua
{
  "yochem/jq-playground.nvim",
  config = true,
}
```

If you use another package manager than lazy.nvim, make sure to run the setup
function to register the `:JqPlayground` command:

```lua
require("jq-playground").setup()
```

## Configuration

There are options available for defining the window layout. These are the
options, along with their defaults:

```lua
require("jq-playground").setup({
  output_window = {
    split_direction = "right",
    width = nil,
    height = nil,
  },
  query_window = {
    split_direction = "bottom",
    width = nil,
    height = 0.3,
  },
})
```

- `split_direction`: can be `"left"`, `"right"`, `"above"` or `"below"`. The
  split direction of the output window is relative to the input window, and the
  query window is relative to the output window.
- `width` and `height`:
  - `nil`: use the default (half of current width/height)
  - `0-1`: percentage of current width/height
  - `>1`: absolute width/height in number of characters or lines

## `:JqPlayground`

Navigate to a JSON file, and execute the command `:JqPlayground`. Two scratch
buffers will be opened: a buffer for the JQ-filter and one for displaying the
results. Simply press `<CR>` (enter) in the filter window to refresh the
results buffer.

You can also provide a filename to the `:JqPlayground` command. This is useful
if the JSON file is very large and slows Neovim down:

```
:JqPlayground sample.json
```

## Tips

If you have a saved filter that you want to load into the filter window, then
run:

```
:r /path/to/some/query.jq
```

If you want to save the current query or output json, navigate to that buffer
and run:

```
:w /path/to/save/{query.jq,output.json}
```

If you want to use a keymap instead of the `:JqPlayground` command, use this:

```lua
vim.keymap.set('n', '<leader>jq', vim.cmd.JqPlayground)
```
