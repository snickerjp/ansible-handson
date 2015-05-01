# ansible-handson
Ansible ハンズオンの手順書

---

```
Vagrant でやるのは、「まだ時間がかかったり」「つまったり」する可能性があるので・・・
とりあえず『Ansible』が動くようにする
```


## 流れ

### Ansible の Playbook を実行するマシン (ansible-setup)
- 仮想マシンの起動(AWSなど)
- host名を設定する
- `git` のインストール
- `Ansible` のインストール
- `private key`の配置
- (optional) `Vagrant` のセットアップ

### 構成管理されるマシン(slave)
- 仮想マシンの起動(AWSなど)

--- 

## 『Ansible の Playbook を実行するマシン (ansible-setup) 』のセットアップ

### 仮想マシンの起動(AWSなど)

- クラウド、VMWareなどで、仮想マシンを立ち上げる
- その際、鍵認証用の`private key` を作成する
- 手元に`private key` を落としておく

### host名を設定する

わからなくなっちゃうので、ホスト名を設定します
```
sudo hostname ansible-setup
```

### git のインストール

```
sudo yum update -y
sudo yum install git
```

### Ansible のインストール

#### Amazon Linuxの場合

Amazon Linuxの場合は、EPELで入れると余計なパッケージ(python26)が追加されるので、pipで！
```
sudo pip install ansible
```

#### CentOS(epel)の場合

思いのほか`EPEL`のパッケージが新しかったのでyumで！
```
sudo yum install http://ftp.riken.jp/Linux/fedora/epel/6/i386/epel-release-6-8.noarch.rpm
sudo yum --enablerepo=epel install ansible
```
### private key の配置

今、立ち上げたマシン(ansible-setup)で

```
cp private.pem ~/.ssh/id_rsa
chmod 400 ~/.ssh/id_rsa
```
--- 

## 『構成管理されるマシン(slave)』のセットアップ

### 仮想マシンの起動(AWSなど)

- クラウド、VMWareなどで、仮想マシンを立ち上げる
- その際、鍵認証用の`private key` を同じで `public key` を設定する

### host名を設定する

わからなくなっちゃうので、ホスト名を設定します
```
sudo vi /etc/sysconfig/network

HOSTNAME=slave

sudo hostname slave
```


### 『Ansible チュートリアル』をもとに作業する

[Ansible チュートリアル | Ansible Tutorial in Japanese](http://yteraoka.github.io/ansible-tutorial/)


を参考に作業を進める！

『3. Ansible の疎通確認』 以降からの作業で大丈夫なはずー
