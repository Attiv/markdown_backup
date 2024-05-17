1. [exa](https://github.com/ogham/exa) 代替 `ls`, 支持语法高亮: `exa -l` 可以设置个 `alias`

```Shell
alias ls="exa"
alias ll="exa -l -a"
```

1. [fd](https://github.com/sharkdp/fd) 代替 `find`, 查找文件比较快

```Dart
Usage: fd [OPTIONS] [pattern] [path]...

Arguments:
  [pattern]  搜索模式 (正则表达式，除非使用了 '--glob'; 可选的)
  [path]...  文件系统搜索的根目录 (可选的)

Options:
  -H, --hidden                     搜索隐藏的文件和目录
  -I, --no-ignore                  不遵从 .(git|fd)ignore 文件
  -s, --case-sensitive             区分大小写的搜索 (默认: 智能大小写)
  -i, --ignore-case                不区分大小写的搜索 (默认: 智能大小写)
  -g, --glob                       基于Glob的搜索 (默认: 正则表达式)
  -a, --absolute-path              显示绝对路径而不是相对路径
  -l, --list-details               使用带有文件元数据的长列表格式
  -L, --follow                     遵循符号链接
  -p, --full-path                  搜索完整路径 (默认: 仅文件名)
  -d, --max-depth <depth>          设置最大搜索深度 (默认: 无)
  -E, --exclude <pattern>          排除符合给定 glob 模式的条目
  -t, --type <filetype>            按类型过滤: file (f), directory (d), symlink (l),
                                   executable (x), empty (e), socket (s), pipe (p)
  -e, --extension <ext>            按文件扩展名过滤
  -S, --size <size>                根据文件的大小限制结果
      --changed-within <date|dur>  按文件修改时间过滤 (较新)
      --changed-before <date|dur>  按文件修改时间过滤 (较旧)
  -o, --owner <user:group>         按拥有文件的用户 (和/或者) 组
  -x, --exec <cmd>...              对每个搜索结果执行命令
  -X, --exec-batch <cmd>...        一次执行包含所有搜索结果的命令
  -c, --color <when>               什么时候使用颜色 [默认: auto] [可以使用的值: auto,
                                   always, never]
  -h, --help                       打印帮助信息 (使用 `--help` 获取更多细节)
  -V, --version                    打印版本信息
```

1. [ripgrep](https://github.com/BurntSushi/ripgrep) 代替 `grep`, 可以设置: `alias lf="ll | rg -i"`
2. [z.lua](https://github.com/skywind3000/z.lua) 快速跳转，比 `auto jump` 快的多
3. git log 美化：

```Dart
git config --global alias.hist "log --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(cyan)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --graph --date=format:'%Y-%m-%d %H:%M:%S'”
```

1. git diff 美化: [https://github.com/so-fancy/diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)
2. [dust](https://github.com/bootandy/dust) (终端展示文件大小)