# Hadoopクラスター・Spark構築用 Ansible Playbook

## 実行前準備

- 接続先サーバーでSSH公開鍵認証接続を可能にし、Ansible管理ホストにダウンロードしておく。（管理ホストで作成したものをアップロードでも可）
- `secrets.yml.dist` をコピーして `secrets.yml` を作成し、各パスワード等の機密情報を環境に応じて設定する。

## 実行

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

## Hadoop

### スタートアップ

- 特定のノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/hdfs namenode -format" -s /usr/bin/bash hdfs

  sudo su - -c "$HADOOP_HOME/bin/hdfs --daemon start namenode" -s /usr/bin/bash hdfs
  ```

- 各ノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/hdfs --daemon start datanode" -s /usr/bin/bash hdfs
  ```

- 特定のノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/yarn --daemon start resourcemanager" -s /usr/bin/bash yarn
  ```

- 各ノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/yarn --daemon start nodemanager" -s /usr/bin/bash yarn
  ```

- 特定のノード（プロキシ未設定の場合は実施不要）

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/yarn --daemon start proxyserver" -s /usr/bin/bash yarn
  ```

- 特定のノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/mapred --daemon start historyserver" -s /usr/bin/bash mapred
  ```

### シャットダウン

- 特定のノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/hdfs --daemon stop namenode" -s /usr/bin/bash hdfs
  ```

- 各ノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/hdfs --daemon stop datanode" -s /usr/bin/bash hdfs
  ```

- 特定のノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/yarn --daemon stop resourcemanager" -s /usr/bin/bash yarn
  ```

- 各ノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/yarn --daemon stop nodemanager" -s /usr/bin/bash yarn
  ```

- 特定のノード（プロキシ未設定の場合は実施不要）

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/yarn --daemon stop proxyserver" -s /usr/bin/bash yarn
  ```

- 特定のノード

  ```shell
  sudo su - -c "$HADOOP_HOME/bin/mapred --daemon stop historyserver" -s /usr/bin/bash mapred
  ```

