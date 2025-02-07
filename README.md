# 実行前準備

- 接続先サーバーでSSH公開鍵認証接続を可能にし、Ansible管理ホストにダウンロードしておく。（管理ホストで作成したものをアップロードでも可）

# 実行

```
# playbookのシンタックスチェック
ansible-playbook -i ./inventory/target.yml site.yml -vv --syntax-check

# ドライラン
ansible-playbook -i ./inventory/target.yml site.yml -vv --check

# 実際に実行
ansible-playbook -i ./inventory/target.yml site.yml -vv

# 途中から実行
ansible-playbook -i ./inventory/target.yml site.yml -vv --start-at="<途中から開始したいタスク名>"
```
