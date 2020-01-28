# MacOSのアプリケーション（など）自動インストール

## コンセプト

- 最低限のおまじないは手動（bashで自動化できるけど、何をするかの意識付け）
- メンテナンス性の優先のため、playbook.ymlは100行超えない間は1ファイル

## 準備

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
$ ansible-playbook playbook.yml
```

## メンテナンス

### おさらい

- Homebrew：macOS用パッケージマネージャー（Apple非公式。「自作」という意味）
  https://brew.sh/index_ja
- Homebrew-Cask：（Homebrewの拡張。2015年にHomebrew本家と統合したよう）
  https://qiita.com/emonuh/items/5dc518a64e6ca722b08a
  https://github.com/Homebrew/homebrew-cask/pull/15381
  https://github.com/Homebrew/legacy-homebrew/pull/46795

### アプリケーションのバージョンアップ

執筆中。

```bash
# 手動だと
$ brew cask upgrade
```


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




