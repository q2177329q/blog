#iterm 2
* 下载 https://iterm2.com/downloads.html
* 配色集合 https://ethanschoonover.com/solarized/
* 下载oh-my-zsh  https://github.com/ohmyzsh/ohmyzsh
* 字体补丁二选一 
  * [Menlo-Powerline](https://github.com/abertsch/Menlo-for-Powerline) 
  * 用的这个 [Monaco-Powerline](https://github.com/supermarin/powerline-fonts/blob/bfcb152306902c09b62be6e4a5eec7763e46d62d/Monaco/Monaco%20for%20Powerline.otf)

```
# ~/.zshrc
SH_THEME="agnoster"  #使用 agnoster 主题，很好很强大
DEFAULT_USER="你的用户名"     #增加这一项，可以隐藏掉路径前面那串用户名
plugins=(git brew node npm)   #自己按需把要用的 plugin 写上
```
