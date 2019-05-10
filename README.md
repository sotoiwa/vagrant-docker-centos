# vagrant-k8s-centos

Dockerイメージのビルド環境を作る手順です。

## 前提

以下のソフトウェアをインストールします。

- [Git](https://git-scm.com/)
- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)

## 手順

VagrantはホストOSのカレントディレクトリーがVMの`/vagrant`にマウントするので、このディレクトリーを使って`Dockerfile`などファイルの受け渡しができます。しかし、デフォルトではVM起動時にrsyncするだけなので、リアルタイムに同期するためには、VirtualBoxのGuest Additionsが必要です。これを自動でインストールしてくれるVagrantのプラグインを導入します。

```
vagrant plugin install vagrant-vbguest
```

VMを起動します。

```shell
# このgitリポジトリをクローン
git clone https://github.com/sotoiwa/vagrant-docker-centos
# クローンしたディレクトリーに入る
cd vagrant-k8s-centos
# VM起動
vagrant up
```

イメージの中に入ります。あとは自由にビルドします。

```
# イメージに入る
vagrant ssh
# Dockerのバージョン確認
docker version
# Dockerfile作成
cat <<EOF > Dockerfile
FROM alpine:3.9
CMD ["echo", "Hello world!"]
EOF
# イメージをビルド
docker build -t test:test .
# イメージを確認
docker images
# イメージを実行確認
docker run --rm -it test:test
# イメージをsave
docker save test:test -o test_test.tar
# イメージをマウントしているディレクトリーにコピー
cp test_test.tar /vagrant
# VMを抜ける
exit
# VMの停止
vagrant halt
# VMの削除
vagrant destroy
```
