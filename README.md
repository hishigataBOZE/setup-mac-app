# MacOSのアプリケーション（など）自動インストール

## コンセプト

- 最低限のおまじないは手動（bashで自動化できるけど、何をするかの意識付け）
- メンテナンス性の優先のため、playbook.ymlは100行超えない間は1ファイル


## 準備

### 事前インストール

```bash
# homebrewをインストール
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew --version
Homebrew 2.2.4
Homebrew/homebrew-core (git revision 72b9; last commit 2020-01-28)

# ansibleをインストール
$ brew install ansible
$ ansible --version
ansible 2.9.3
:
```

## 実行

```bash
$ ansible-playbook -i inventory playbook.yml
:
Password: <<<< パスワードを求められたら素直に入力
:
```

## アプリケーションがansibleでインストールされたか確認 

caskのみ判別可能
```bash
$ brew cask list
```


## 付録. ansible管理への移行について

### Homebrewでインストールしたアプリケーション

特になし。

### 手動でインストールしたアプリケーション

1. `/Application`からアプリケーションを削除
2. `ansible`を実行


## 付録. メンテナンス

### おさらい

- Homebrew：macOS用パッケージマネージャー（Apple非公式。「自作」という意味）
  https://brew.sh/index_ja
- Homebrew-Cask：（Homebrewの拡張。2015年にHomebrew本家と統合したよう）
  https://qiita.com/emonuh/items/5dc518a64e6ca722b08a
  https://github.com/Homebrew/homebrew-cask/pull/15381
  https://github.com/Homebrew/legacy-homebrew/pull/46795

### アプリケーションのバージョンアップ

1. `ansible`を実行 **※未検証**

### アプリケーションの探し方と設定

#### Homebrewでインストールするアプリケーション

```bash
$ brew search wget
==> Formulae
wget                                               wgetpaste
```

Formulae（「公式」の意）と表示されたので、`brew_packages:`に追加する。

```yml:playbook.yml
    brew_packages:
      # wgetコマンド
      - wget
```

#### Homebrew-Caskでインストールするアプリケーション

```bash
$ brew search google-chrome
==> Casks
homebrew/cask-versions/google-chrome-beta          homebrew/cask-versions/google-chrome-dev
homebrew/cask-versions/google-chrome-canary        homebrew/cask/google-chrome
```

Casksと表示されたので、`brew_cask_apps:`に追加する。

```yml:playbook.yml
    brew_cask_apps:
      # Google 日本語入力
      - google-japanese-ime
```


## 参考

- https://t-wada.hatenablog.jp/entry/mac-provisioning-by-ansible
- https://qiita.com/fukushi_yoshikazu/items/5e327103066ac80629f3#3-ansible-vault%E3%81%A7%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%82%92%E6%9A%97%E5%8F%B7%E5%8C%96%E3%81%97%E3%81%A6%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E5%85%A5%E5%8A%9B%E3%82%92%E7%9C%81%E7%95%A5