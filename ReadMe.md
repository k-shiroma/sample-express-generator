# sample-express-generator
express-generator を利用し Node.js + express のプロジェクト作成手順を記載するプロジェクトです

## 参考URL
- nodenv インストール
    - [mintsu's blog - Linux(Ubuntu)にnodenvを導入する方法](https://blog.mintsu-dev.com/posts/2020-07-22-install-nodenv-linux/#nodenv-install)
    - [Qiita - @282Haniwa - nodenvの環境構築](https://qiita.com/282Haniwa/items/a764cf7ef03939e4cbb1)
- express-generator
    - [Express のアプリケーション生成プログラム](https://expressjs.com/ja/starter/generator.html)

## 開発環境
| 名前 | バージョン |
|-|:-:|
| VirtualBox | 6.1 |
| ubuntu | 20.04.3 server |
| Visual Studio Code | 1.61.0 |
| nodenv | 1.4.0+3.631d0b6 |
| Node.js | 17.0.1 |
| express | 4.16.1 |
| express-generator | 4.16.1 |

## 実行手順
本プロジェクトを実行する場合、[環境構築](#環境構築) を行った後に下記を実行してください

### 構築/設定
```sh
# 1. ソース取得
git clone https://github.com/k-shiroma/sample-express-generator.git

# 2. ライブラリ取得
cd sample-express-generator
npm install
```

### 実行
1. 起動
    ```sh
    node index.js
    ```
1. http://localhost:8080 をブラウザで開く

## 開発手順
本プロジェクトの作成手順です

### 環境構築
```sh
# 1. nodenv
## apt アップデート
### install の前にはやっておいたほうがいい
### ubuntu20.04.3 だと build-essential インストール時にエラーになる
sudo apt update

## 開発ツールインストール (nodenv ビルド時に使用)
sudo apt install build-essential

## nodenv ダウンロード
git clone https://github.com/nodenv/nodenv.git ~/.nodenv

## nodenv ビルド
cd ~/.nodenv && src/configure && make -C src

## PATHを通す
echo 'export PATH="$HOME/.nodenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(nodenv init -)"' >> ~/.bashrc

## シェル再起動
exec $SHELL -l

## Node.js インストール用プラグイン インストール
git clone https://github.com/nodenv/node-build.git $(nodenv root)/plugins/node-build

## インストール確認
curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash

## こうなっていたらOK
## Checking for `nodenv' in PATH: /home/ubuntu/.nodenv/bin/nodenv
## Checking for nodenv shims in PATH: OK
## Checking `nodenv install' support: /home/ubuntu/.nodenv/plugins/node-build/bin/nodenv-install (node-build 4.9.57)
## Counting installed Node versions: none
##   There aren't any Node versions installed under `/home/ubuntu/.nodenv/versions'.
##   You can install Node versions like so: nodenv install 2.2.4
## Auditing installed plugins: OK

# 2. Node.js
## インストール可能なバージョンのリスト確認
nodenv install -l

## インストール(最新)
nodenv install 17.0.1

## システム全体で使用する Node.js 設定
nodenv global 17.0.1

## 確認
node -v
nodenv versions

# 3. express-generator
## インストール
npm install express-generator -g

## リンク更新
nodenv rehash

## 確認
express --version
```

### 設定
```sh
# 4. プロジェクト生成
## プロジェクトルート作成
cd ~/projects/
express sample-express-generator --no-view
cd ~/projects/sample-express-generator

## プロジェクトで使用する Node.js 設定
nodenv local 17.0.1

## Node.js バージョン確認
node -v
nodenv versions

## ライブラリ取得
npm install
```

### 実行
1. 起動
    ```sh
    npm start
    ```
1. http://localhost:3000 をブラウザで開く
