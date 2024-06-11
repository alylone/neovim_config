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

## 插件的使用

Lsp Mason的用法

```lua
:Mason
```



## 踩坑

### 关闭缓冲区tag报错

```lua
nvim-ts-rainbow的问题 与 bufferline的冲突问题

-- 相关帖子
-- https://github.com/LunarVim/LunarVim/issues/4227
-- https://github.com/neovim/neovim/issues/28084

需要将旧版本的rainbow更换为HiPhish/nvim-ts-rainbow2
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


