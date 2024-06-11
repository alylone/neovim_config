[本次部署使用了蛋老师的配置视频教程](https://www.bilibili.com/video/BV1Td4y1578E/?spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=3268ce5f8f29db48f5c4973357c7dfad)
> project view

插件管理:packer / Lazy

在main分支中为packer管理 在lazy分支中为 Lazy管理

# neovim配置

采用Lua语言

## packer

```lua
部署：通过将packer插件管理的lua代码，复制到一个配置文件中，并在init.lua中引用  -- 分布式存储

packer需要将存储packer代码的文件,每次保存来进行插件的更新 (更新与卸载)
即进入到对应的文件 命令行模式下输入 :w

-- 加入插件
在指定的位置，通过 use ""的方法来安装
例：
  use "nvim-treesitter/nvim-treesitter" -- 语法高亮

安装完毕后，可能需要:so 重新载入或者是完全退出重新进入 来使安装的插件生效
```

## Lazy

```lua
也是将指定代码复制到lua文件中，并在init.lua中引用  

通过命令:Lazy 来管理插件

-- 加入插件
在指定位置加入包名 通过" "
例:
local plugins = {
  "folke/tokyonight.nvim", -- 主题
    ...
    }

```

## 插件安装

> 一般安装方法

```lua
在通过包管理器安装后，一部分插件可直接使用，但一般插件还需要进行一定配置
-- 配置
将配置文件放在xxx.lua中 ,并在init.lua中引用

安装插件一般流程
-- 在包管理中安装
-- 补充配置文件
-- 在init.lua中引用配置文件
```

## 插件的使用

Lsp Mason的用法

```lua
:Mason
-- 寻找需要的LSP，按I安装
-- 在配置文件(lsp.lua)中添加启动配置代码

例:
Pyright:
- :Mason
- 找到Pyright,按i安装
- 修改lsp.lua文件
--[[
require("lspconfig").pyright.setup {
  capabilities = capabilities,
  settings = {
    python = {
      analysis = {
        autoSearchPaths = true,
        diagnosticMode = "workspace",
        useLibraryCodeForTypes = true,
        typeCheckingMode = "off",
      }
    }
  },
}
--]]


- 重新加载后即可正常使用
```



## 踩坑

### 关闭缓冲区tag报错

```lua
nvim-ts-rainbow的问题 与 bufferline的冲突问题

-- 相关帖子
-- https://github.com/LunarVim/LunarVim/issues/4227
-- https://github.com/neovim/neovim/issues/28084

需要将旧版本的rainbow更换为HiPhish/nvim-ts-rainbow2

-- 但是 ！！！BUT！
HiPhish/nvim-ts-rainbow2会导致插件(nvim-treesitter、rainbow2等)在Lazy管理下，加载时间很长
```

### 字体显示问题

```lua
安装指定的字体即可

-- hack nerd font
-- http://www.guopher.cn/article/article-detail/88/
-- https://github.com/ryanoasis/nerd-fonts/releases/tag/v3.2.1  寻找 hack nerd font.zip
```

### nvim-treesitter 报错

```lua
显示为 没有"help"的parser
将"help"更改为 "vimdoc" 
即原文将变成 ensure_installed = { "vim", "vimdoc", ...}
```

### clipboard 问题

```shell
通过:checkhealth找到问题
## Clipboard (optional)
  - WARNING: No clipboard tool found. Clipboard registers (`"+` and `"*`) will not work.
    - ADVICE:
      - :help clipboard

# 详细帖子 https://github.com/neovide/neovide/issues/544

# 解决方案: 安装win32yank.exe
curl -sLo/tmp/win32yank.zip https://github.com/equalsraf/win32yank/releases/download/v0.0.4/win32yank-x64.zip
unzip -p /tmp/win32yank.zip win32yank.exe > /tmp/win32yank.exe
chmod +x /tmp/win32yank.exe
sudo mv /tmp/win32yank.exe /usr/local/bin/ # 将win32yank.exe放在环境变量中即可 $PATH
```

