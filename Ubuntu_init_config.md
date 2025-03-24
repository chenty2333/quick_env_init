```
sudo apt update && sudo apt install -y \
    ninja-build meson automake autoconf libtool flex bison nasm yasm gperf patchelf \
    gcc llvm gdb lldb mold ccache clang cmake make cmake-gui build-essential g++ libstdc++-12-dev \
    pkg-config libboost-all-dev libssl-dev libcurl4-openssl-dev libxml2-dev libjsoncpp-dev \
    tldr bat fzf ripgrep zsh neofetch figlet cowsay lolcat atool ranger fd-find httpie \
    curl wget gnupg ncdu arandr scrot imagemagick ffmpeg vlc gimp inkscape \
    git vim vim-gtk3 neovim tmux screen tree zip unzip jq eza colordiff xclip xsel \
    git-lfs clang-format clang-tidy valgrind strace lsof rsync htop nmap



# ccache配置
export CC="ccache clang"
export CXX="ccache clang++"
export CC="ccache gcc"
export CXX="ccache g++"


# eza配置
alias ls='exa --icons --color=auto'


# Ubuntu安装python解释器
sudo apt install python3.12
sudo apt install python3.13-distutils
sudo apt install python3-pip


# miniconda配置
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
conda init


# zsh配置
## 设置成默认shell
chsh -s $(which zsh)
## oh my zsh安装
## powerlevel10k主题
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k

ZSH_THEME="powerlevel10k/powerlevel10k"

p10k configure

## 补全插件
git clone https://github.com/zsh-users/zsh-autosuggestions \
  $ZSH_CUSTOM/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-completions \
  $ZSH_CUSTOM/plugins/zsh-completions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# 启用 alias 补全
setopt COMPLETE_ALIASES

# 连续按 Tab 显示补全菜单
setopt AUTO_MENU

# 启用补全系统
autoload -Uz compinit
compinit

zstyle ':completion:*' menu select

plugins=(git zsh-autosuggestions zsh-syntax-highlighting zsh-completions)


# 设置历史记录文件大小限制
HISTFILE=~/.zsh_history
HISTSIZE=10000      # 内存中保存多少条历史
SAVEHIST=10000      # 写入 ~/.zsh_history 的条数


# 历史记录设置建议
setopt HIST_IGNORE_DUPS     # 忽略重复命令
setopt HIST_IGNORE_ALL_DUPS # 忽略所有重复命令（更严格）
setopt HIST_REDUCE_BLANKS   # 去除多余空格
setopt HIST_VERIFY          # 让你可以编辑历史命令再执行
setopt SHARE_HISTORY        # 多终端共享历史记录

## fzf命令搜索
fzf-history-widget() {
  BUFFER=$(history 1 | tail -n 500 | fzf --tac +s --no-sort --query "$LBUFFER") && CURSOR=$#BUFFER
  zle reset-prompt
}
zle -N fzf-history-widget
bindkey '^R' fzf-history-widget

# 快速搜索历史记录
bindkey '^R' fzf-history-widget

FZF_DEFAULT_OPTS="--height 40% --layout=reverse --border"
FZF_DEFAULT_COMMAND='fd --type f'

alias nvf='nvim $(fzf)'   # 用 fzf 快速 fuzzy 选文件用 nvim 打开
alias cdf='cd $(fd --type d | fzf)' # fuzzy 选个目录进入

```



在 Ubuntu 24.04 系统中，如果您希望在整个系统范围内交换 Caps Lock 键和 Esc 键的功能，可以通过以下方法实现：

**方法一：使用 `dconf-editor` 工具**

1.**安装 `dconf-editor`：**

打开终端，输入以下命令安装 `dconf-editor`：

```bash
sudo apt update
sudo apt install dconf-editor
```

2.**启动 `dconf-editor`：**

在终端中输入以下命令启动 `dconf-editor`：

```bash
dconf-editor
```

3.**导航到键盘设置：**

在 `dconf-editor` 中，依次展开以下路径：

```
org
└── gnome
    └── desktop
        └── input-sources
```

4.**修改键盘选项：**

在右侧窗格中，找到 `xkb-options` 设置。如果该设置为空数组（`[]`），请将其修改为：

```
['caps:swapescape']
```

如果已有其他选项，请将其添加到数组中，确保格式正确，例如：

```
['caps:swapescape', '其他选项']
```

5.**保存并应用更改：**

修改完成后，关闭 `dconf-editor`。更改应立即生效，无需重启系统。

