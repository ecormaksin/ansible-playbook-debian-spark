# 実行前準備

- 接続先サーバーでSSH公開鍵認証接続を可能にし、Ansible管理ホストにダウンロードしておく。（管理ホストで作成したものをアップロードでも可）
- `secrets.yml.dist` をコピーして `secrets.yml` を作成し、各パスワード等の機密情報を環境に応じて設定する。

# 実行

```
# playbookのシンタックスチェック
ansible-playbook -vv -i inventory.yml --extra-vars @control-node.yml --extra-vars @secrets.yml site.yml --syntax-check

# ドライラン
ansible-playbook -vv -i inventory.yml --extra-vars @control-node.yml --extra-vars @secrets.yml site.yml --check

# 実際に実行
ansible-playbook -vv -i inventory.yml --extra-vars @control-node.yml --extra-vars @secrets.yml site.yml

# 途中から実行
ansible-playbook -vv -i inventory.yml --extra-vars @control-node.yml --extra-vars @secrets.yml site.yml --start-at="<途中から開始したいタスク名>"
```
