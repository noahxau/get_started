## 安装chrome

## fatcatcloud 配置 clash verge
1. 购买订阅: https://fatcatcloud.org/
2. 安装对应的客户端，肥猫云默认的clashX pro
3. 导入订阅
4. 启动clashX pro
5. 设置为系统代理
6. github下载clash verge替代clashX pro： https://github.com/Clash-Verge-rev/clash-verge-rev/releases
7. 重复3 4 5为clash verge配置订阅

## 配置 alias
- 配置代理，加速软件安装和github访问速度
```zsh
# github/google
alias proxy="export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890"
alias unproxy="unset https_proxy http_proxy all_proxy"
```

## 安装homebrew
```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 配置python开发环境
1. 安装python版本和项目管理工具uv
```zsh
brew install uv
```

2. 使用uv初始化项目并创建对应版本的venv
```zsh
mkdir py-demo && cd py-demo
uv init --python 3.12
uv venv --python 3.12
# pycharm 打开项目
```

3. 配置uv国内源
```zsh
export UV_INDEX_URL="https://pypi.tuna.tsinghua.edu.cn/simple"
```

## 配置node开发环境
1. 安装node版本管理器fnm： brew install fnm
2. 配置fnm use的shell： https://github.com/Schniz/fnm  eval "$(fnm env --use-on-cd --shell zsh)"
3. 配置fnm node国内源： export FNM_NODE_DIST_MIRROR="https://mirrors.tuna.tsinghua.edu.cn/nodejs-release/"
4. 安装切换node版本
```zsh
fnm list-remote
fnm install 22
fnm install v24
fnm use v24
node --version
npm --version
```
5. 配置node/yarn/pnpm国内源，缓存路径，
```zsh
npm i -g yarn pnpm

npm config get registry 
npm config set registry https://registry.npmmirror.com --global
npm config get cache
npm config set cache ~/cache/npm
npm cache clean --force

yarn config get registry
yarn config set registry https://registry.npmmirror.com
yarn cache dir
yarn config set cache-folder ~/cache/yarn
yarn cache clean

pnpm config get registry
pnpm config set registry https://registry.npmmirror.com
pnpm store path
pnpm config set store-dir ~/cache/pnpm
pnpm store prune
```

## 配置golang开发环境
```zsh
# 安装go https://golang.google.cn/
export GOPROXY=https://goproxy.cn
# 安装vscode 和 go 插件
# 设置vscode zoom 为0.3左右放大窗口
# 安装go插件的依赖（依赖GOPROXY否则会因为网络安装失败） shift+command+p >go:install/update tools  gopls + staticcheck + dlv 
# 设置
mkdir go-demo && cd go-demo
go mod init github.com/username/go-demo
touch main.go 测试插件情况
```

## 配置rust开发环境
1. 配置rustup和cargo代理： https://rsproxy.cn/
```zsh
export RUSTUP_DIST_SERVER="https://rsproxy.cn"
export RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"
```

2. 安装rustup: https://www.rust-lang.org
```zsh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
3. 快速demo验证
```zsh
cargo new rs-demo && cd rs-demo
cargo add axum tokio
```

<br>

## 汇总
- cat .zprofile
```zsh
eval "$(/opt/homebrew/bin/brew shellenv)"
```

- cat .zshrc
```zsh
# github/google
alias proxy="export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890"
alias unproxy="unset https_proxy http_proxy all_proxy"

# go 
export GOPROXY=https://goproxy.cn
export GOPATH="/Users/luke/go"
export PATH="$GOPATH/bin:$PATH"

# rust
export RUSTUP_DIST_SERVER="https://rsproxy.cn"
export RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"

# node
export FNM_NODE_DIST_MIRROR="https://mirrors.tuna.tsinghua.edu.cn/nodejs-release/"
eval "$(fnm env --use-on-cd --shell zsh)"
```

- cat ~/.cargo/config
```zsh
[source.crates-io]
replace-with = 'rsproxy-sparse'
[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"
[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"
[net]
git-fetch-with-cli = true
```

- ls $GOPATH/bin
```text
dlv		gopls		staticcheck
```