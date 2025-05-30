# rails-i18n-hover

A Neovim plugin to instantly hover and browse Rails I18n translations under your cursor. It parses your `**/config/locales/*.yml` files and shows translations in a floating window.

![image](https://github.com/user-attachments/assets/a9e4193a-7409-4f1f-927e-626292ff12b2)



## Features

- 🔄 Parses and flattens all Rails locale YAML files in the background  
- 🎛️ Hover with a keymap to see translations for all available languages  
- 📄 `gf` binding to jump straight to the source YAML file for a given key  
- ⚙️ Easy configuration of keymaps and filetypes

## Prerequisites

- Neovim v0.7+  
- 'nvim-neotest/nvim-nio' plugin for async parsing 
- Ruby 1.8+ (plugin invokes: `ruby scripts/flatten_locales.rb <project_root>`)  
- A `Gemfile` at your project root (otherwise the plugin will not load)

## Installation

### lazy.nvim

```lua
require("lazy").setup({
  {
    "moguls753/rails-i18n-hover.nvim",
    config = function()
      require("rails-i18n-hover").setup()
    end,
    dependencies = {
      "nvim-neotest/nvim-nio",
    },
  },
})
```

## Usage

- Open any file in your Rails project (e.g. `.rb`, `.erb`, `.js`, `.vue`, `.html`, etc.).

- Move your cursor over an I18n lookup, for example:

```ruby
I18n.t("welcome.title")
```

- Press your hover keymap (`<leader>ih` by default) to see all translations in a floating window.

Press `gf` on the same key to jump to the corresponding YAML file (defaults to english `"en"` files).

## Configuration

Call `setup()` with your own options:

```lua
require("rails-i18n-hover").setup({
    keymap    = "<leader>tt",               -- change the hover keybinding
    filetypes = { "rb", "eruby", "js" },    -- limit to specific filetypes
    goto_lang     = "de"
    goto_file_keymap     = "gt"             -- if default gf disturbs other plugins
})
```

| Option     | Default                                                                                      | Description                                                  |
| ---------- | -------------------------------------------------------------------------------------------  | ------------------------------------------------------------ |
| `keymap`   | `"<leader>ih"`                                                                               | Normal‐mode key to show hover translations                   |
| `filetypes`| `{ "lua", "js", "ts", "vue", "html", "rb", "eruby", "slim" }`                                | Filetypes on which to enable the keymaps                     |
| `goto_lang`| `"en"`                                                                                       | language yaml file for `gf` (e.g. en.yml)                    |
| `goto_file_keymap`| `"gf"`                                                                                       | keymap for opening the yaml file which contains the key under cursor                    |

