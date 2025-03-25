```
sudo pacman -Syu --noconfirm

sudo pacman -S --needed --noconfirm \
    ninja meson automake autoconf libtool flex bison nasm yasm gperf patchelf \
    gcc llvm gdb lldb mold ccache clang cmake make base-devel pkgconf boost openssl \
    curl libxml2 jsoncpp tldr bat fzf ripgrep zsh neofetch figlet cowsay atool ranger fd httpie \
    wget gnupg ncdu arandr scrot imagemagick ffmpeg vlc gimp inkscape \
    git vim gvim neovim tmux screen tree zip unzip jq colordiff xclip xsel \
    git-lfs clang-format clang-tidy valgrind strace lsof rsync htop nmap \
    python python-pip
```



```bash
# 安装 paru（命令行方式）
cd /tmp
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
# -------------------------------
# 3. 安装 AUR 中的软件包
# -------------------------------
yay -S --noconfirm cmake-gui lolcat eza

# -------------------------------


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

```
# Caps Lock和Esc键互换
sudo pacman -S dconf-editor
## 打开 dconf-editor
org → gnome → desktop → input-sources
## 修改 xkb-options 为：
['caps:swapescape']
```

