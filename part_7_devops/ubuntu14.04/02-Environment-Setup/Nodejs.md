# Ubuntu 14.04配置Nodejs开发环境

## 使用NVM来安装Node.js
NVM也就是 "Node.js version manager"

Using nvm, you can install multiple, self-contained versions of Node.js which will allow you to control your environment easier. It will give you on-demand access to the newest versions of Node.js, but will also allow you to target previous releases that your app may depend on.

To start off, we'll need to get the software packages from our Ubuntu repositories that will allow us to build source packages. 
首先需要从Ubuntu库中安装一些软件包用来编译：

The nvm script will leverage these tools to build the necessary components:

```bash
sudo apt-get update
sudo apt-get install build-essential libssl-dev
```

安装完成后从nvm的[Github页面](https://github.com/creationix/nvm)上下载nvm的安装脚本，注意脚本的版本，例如：
> Ubuntu 14.04 默认没有安装 `curl`

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
# 或者
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
```

默认会安装到当前用户的目录下，并添加到环境变量(`~/.profile`)中，但要直接使用`nvm`，要么退出重新登录，要么使用 :

```bash
source ~/.profile
```
这样就可以使用nvm了，

### nvm列出所有可安装的node

```bash
nvm ls-remote
```
这里我们使用LTS版本 4.6.2

### 安装 

```bash
nvm install 4.6.2
```

### 指定使用哪个版本的node

```bash
nvm use 4.6.2
node -v 
```

如果想设置默认的node版本

```bash
nvm alais default 4.6.2
```

### 使用npm
默认 全局安装的node package会安装到 

```
~/.nvm/versions/node/"node_version"/lib/node_modules/"package"
```

### 配置npm registry
https://npm.taobao.org/

```bash
npm config set registry https://registry.npm.taobao.org 
```

### 常用包安装：
npm 
yo 
bower
gulp
node-gyp
pm2


## 参考
https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-an-ubuntu-14-04-server

## 安装node4.4.1
https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions

```bash
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```


