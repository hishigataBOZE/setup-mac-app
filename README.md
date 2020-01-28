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
