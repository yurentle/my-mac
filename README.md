# my-mac

## 简介

这个仓库记录了我配置新Mac的内容和步骤，包括软件安装、系统设置和故障排除。

## 目录

- [brew 源修改](#brew-源修改)
- [安装工具](#安装工具)
- [Chrome 浏览器同步问题](#Chrome-浏览器同步问题)
- [Mac扬声器不出声音](#Mac扬声器不出声音)
- [Mac邮箱设置](#Mac邮箱设置)
- [Sequel Pro数据库连接问题](#Sequel-Pro数据库连接问题)
- [配置git的常用命令](#配置git的常用命令)
- [oh-my-zsh配置](#oh-my-zsh配置)
- [iTerm2配置](#iTerm2配置)
- [系统时间不准](#系统时间不准)
- [Charles抓包设置](#Charles抓包设置)

## brew 源修改

```bash
# 替换brew.git:
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

# 替换homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

# 替换Homebrew Bottles源(zsh配置)
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc
```

## 安装工具

```bash
homebrew
nvm
node
oh-my-zsh 
yarn
pnpm

Hammerspoon
iTem2
NeatDownloadManager
uTools
CheatSheet
Snipaste
Docker
Sequel Ace
Table plus
Visual Studio Code
Cursor
Windsurf
Xcode
Android Studio
```

## Chrome 浏览器同步问题

参考[Chrome 浏览器重启后就同步暂停](https://github.com/techial1042/Blog/issues/26)的解决方案。

## Mac扬声器不出声音

```bash
sudo killall coreaudiod
```

## Mac邮箱设置

参考[Mac邮箱设置](https://www.crifan.com/mac_use_mail_to_receive_tencent_enterprise_email/)。

## 通过Sequel Pro连接数据库时，提示：Authentication plugin 'caching_sha2_password' cannot be loaded 的错误

参考[解决方法](https://stackoverflow.com/questions/49194719/authentication-plugin-caching-sha2-password-cannot-be-loaded)：

```sql
ALTER USER 'yourusername'@'localhost' IDENTIFIED WITH mysql_native_password BY 'yourpassword';
```

## 配置git的常用命令

```bash
# 查看当前项目配置
git config -l

# 查看全局配置
git config --global --list

# 修改提交名
git config --global user.name "example"

# 设置全局邮箱
git config --global user.email example@example.com

# 设置别名
git config --global alias.br branch

# 删除配置项
git config --unset alias.co

# 关闭忽略大小写
git config --global core.ignorecase false
```

## oh-my-zsh配置

```bash
# 查看当前shell
echo $SHELL

# 查看可用shell
cat /etc/shells

# 安装zsh
brew install zsh

# 设置默认shell为zsh
chsh -s /bin/zsh

# 安装oh-my-zsh，查看配置
cd ~ && vim .oh-my-zsh/plugins/git/git.plugin.zsh

# 添加别名
vim ~/.zshrc
alias ns="npm start"
alias nd="npm run dev"
alias gam="git add . && git commit -m"
alias gcam="git commit --amend -m"
alias p="pnpm"
alias code="open -a Visual\ Studio\ Code ."
alias cs="open -a Cursor ."

# 查看主题内容
less ~/.oh-my-zsh/themes/robbyrussell.zsh-theme

# 选择主题为mira
ZSH_THEME="mira"

# 添加插件
plugins=(git z zsh-autosuggestions)
```

## iTerm2配置

```bash
# 鼠标滚动设置
Scroll wheel sends arrow keys when in alternate screen mode，设置为Yes

# 新建窗口默认大小
profiles-window-columns（120）rows（30）
```

## 系统时间不准

```bash
sudo sntp -sS pool.ntp.org

# 如果提示（kod\_init\_kod\_db(): Cannot open KoD db file /var/db/ntp-kod: No such file or directory）错误，执行：
sudo touch /var/db/ntp-kod
sudo chmod 666 /var/db/ntp-kod

# 或者设置crontab
sudo crontab -e
0 0 * * 1 /usr/bin/sntp -sS time.apple.com
```

## Charles抓包设置

```bash
# Chrome浏览器要装SwitchySharp插件才能抓到chrome的包，设置http代理127.0.0.1，端口8888
# 微信开发者工具要想抓包要设置代理为使用系统代理
# 如果还有问题，可能是开了shadowsocks
```
