# Moving from NvChad to Native Neovim 0.12
> Part of my [dotfiles](https://github.com/j-dumas/dotfiles)

## Summary
---
I've wanted for a while now to move from [NvChad](https://nvchad.com/) to a more simple and personalized Neovim config. I thus decided to redo all my config in the new Neovim 0.12 from scratch by readding only what I need and throwing out the rest, things like `mason` and `mason-lspconfig`, `lazy`, etc.

## The Config
---
### What's Needed?
To transform Neovim into the experience I had with NvChad, i.e. close to a full IDE, I'll need

- LSP
- Highlight
- Autocompletion
- Formatter/linter
- Colorscheme
- Statusline
- Tree
- Something to search for files like Telescope or fzf-lua
- A Git client to not rely on switching tmux panes for lazygit

### Structure
Let's start with the structure of the config directory:
```txt
~/.config/nvim/
├── init.lua
└── lua/
	├── lsp/
	|   ├── init.lua
	|   ├── lua_ls.lua
	|   ├── clangd.lua
	|   └── pylsp.lua
	├── plugins/
	|   ├── init.lua
	|   ├── fzf-lua.lua
	|   └── ui.lua
	├── autocmds.lua
	├── keymaps.lua
	└── options.lua
	
```

### Options
Here are the options I used. These were taken from the NvChad config to have a similar feel and also from [a list of the most common options in Neovim](https://dotfiles.substack.com/p/neovim-options-the-most-common-ones).
```lua
require('vim._core.ui2').enable()

vim.g.netrw_banner = 0
vim.g.mapleader = ' '

vim.o.nu = true
vim.o.relativenumber = true

vim.o.tabstop = 4
vim.o.softtabstop = 4
vim.o.shiftwidth = 4
vim.o.expandtab = true
vim.o.smartindent = true

vim.o.inccommand = "split"
vim.o.splitbelow = true
vim.o.splitright = true

vim.o.ignorecase = true
vim.o.smartcase = true
vim.o.laststatus = 3

vim.o.swapfile = false
vim.o.backup = false
vim.o.undodir = vim.fn.stdpath("data") .. "/undodir"
vim.o.undofile = true

vim.o.clipboard = "unnamedplus"
vim.o.cursorline = true
vim.o.cursorlineopt = "number"
vim.o.scrolloff = 8
vim.o.signcolumn = "yes"
vim.o.termguicolors = true
vim.opt.whichwrap:append "<>[]hl"
```

### UI: Colorscheme and Statusline
Here are the two plugins I use for UI: `catppuccin-nvim` and `lualine`
```lua
vim.pack.add { 
    { 
        src = "https://github.com/catppuccin/nvim",
        name = "catppuccin" 
    } ,
    'https://github.com/nvim-tree/nvim-web-devicons',
    'https://github.com/nvim-lualine/lualine.nvim'
}
```
Since I already use Catppuccin Mocha nearly everywhere, I installed it for Neovim.  For a terminal, I use kitty with a transparent background, so I opted to have Neovim transparent as well. I also modified the colors of the sections to fit my tmux look (which is kind of a bastard between the dracula tmux plugin and catppuccin colors). I changed some highlights to fit my taste, like the `MatchParen` to remove colors of matching brackets and only keep the background highlight.
```lua
require("catppuccin").setup({
    flavour = "mocha",
    transparent_background = true,
    custom_highlights = function(colors)
        local U = require("catppuccin.utils.colors")
        return {
            MatchParen = { fg = colors.none, style = {} },
            IncSearch = { bg = colors.green },
        }
    end,
    integrations = {
        lualine = {
            mocha = function(colors)
                return {
                    normal = {
                        a = { bg = "#8bc2f0" },
                        b = { fg = colors.text },
                        c = { fg = colors.surface2 },
                    },
                    insert = {
                        b = { fg = colors.text },
                    },
                    visual = {
                        b = { fg = colors.text },
                    },
                    command = {
                        b = { fg = colors.text },
                    },
                }
            end
        }
    }
})
vim.cmd.colorscheme "catppuccin-nvim"
```
And here is lualine as I like:
```lua
require('lualine').setup({
    options = {
        component_separators = {left = '', right = ''},
        section_separators = {left = '◤', right = ''}
    },
    sections = {
        lualine_a = {'mode'},
        lualine_b = {{'filename', path = 1}},
        lualine_c = {'branch', 'diff'},
        lualine_x = {'diagnostics', 'lsp_status'},
        lualine_y = {'location'},
        lualine_z = {'progress'}
    },
    extensions = {'nvim-tree'}
})
```

### Tree: A File Viewer
I'm used to having a file viewer in the side bar and did not really want to use `netrw`, so I decided to try [Neo-tree](https://github.com/nvim-neo-tree/neo-tree.nvim). I added `nvim-webdev-icons` and `nvim-window-picker` for icons and picking a specific window when opening a file instead of opening in the last one, respectively. I added nicer colors for the window picker because the default was bright green. It's now red with a transparent background. Finally I changed the mappings to always ask which window to open a file when there are splits.
```lua
vim.pack.add({
  {
    src = 'https://github.com/nvim-neo-tree/neo-tree.nvim',
    version = vim.version.range('3')
  },
  -- Dependencies
  "https://github.com/nvim-lua/plenary.nvim",
  "https://github.com/MunifTanjim/nui.nvim",
  "https://github.com/nvim-tree/nvim-web-devicons",
  {
      src = 'https://github.com/s1n7ax/nvim-window-picker', 
      version = vim.version.range('2.*') 
  },
})

require 'window-picker'.setup({
    hint = 'statusline-winbar',
    selection_chars = 'ABCDEFGHIJKLMNOP',
    highlights = {
        enabled = true,
        statusline = {
            unfocused = {
                fg = '#f38ba8',
                bg = 'NONE',
                bold = true,
            },
        },
        winbar = {
            unfocused = {
                fg = '#f38ba8',
                bg = 'NONE',
                bold = true,
            },
        },
    },
})

require("neo-tree").setup({
  window = {
    mappings = {
      ["<cr>"] = "open_with_window_picker",
      ["s"]    = "split_with_window_picker",
      ["v"]    = "vsplit_with_window_picker",
      ["S"]    = "noop",
      ["w"]    = "noop",
    },
  },
})
```