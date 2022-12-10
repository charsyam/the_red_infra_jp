# the_red_infra
the red infra

# よくある質問
* EC2 VPC Not Found エラーが発生します
  * エラーは以下の場合に発生します。
    * VPCがAWSで作成する基本的なVPCではなく任意に作成したものである場合
    * この際、VPC idを明示的に入力すれば動作します。
    * 注釈 "#"で処理された部分で変更してみてください。

# Q/A
* Issueに質問を作成してください。

# setup

* 基本的なテストはubuntu 20.04で行われました(18.04でも動作します)。
* aptを正しく使用するためにapt updateを進めます。

```
sudo apt update
```

* pythonのインストールに必要なパッケージをインストールします。

```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
```

* the_red_infraをgit cloneで受け取り ./install_pyenv.shを実行します。bashを使う場合はsource~/.bashrc、zshを使う場合はsource~/.zshrc

```
	git clone https://github.com/charsyam/the_red_infra
	./install_pyenv.sh
	source ~/.bashrc
	./install_python.sh
    install_ansible_password.sh    
	install_terraform.sh	
```

* terraformの実行
```
    cd terraform/ec2/ap-northeast-1
    terraform init
    terraform plan -out "output"
    terraform apply "output"
```

* 以下はansibleの実行方法です。作成前にaws/hostsファイルに対象ホストの
設定が必要です。

apply ansible: geoip
```
    ansible-playbook -i aws the_red_1_base.yml
    ansible-playbook -i aws the_red_2_geoip.yml
    ansible-playbook -i aws the_red_2_lb.yml
```

apply ansible: monitor(prometheus + grafana)
```
    ansible-playbook -i aws the_red_1_base.yml
    ansible-playbook -i aws the_red_2_monitor.yml
```

apply ansible: ngrinder
```
    ansible-playbook -i aws the_red_1_jvm.yml
    ansible-playbook -i aws the_red_2_ngrinder.yml
```

# Ansile Reference
* Ansibelの基礎資料については、以下を参考にしてください。
 * [https://drive.google.com/file/d/1H51LfuebDhOaL75asxq8SLZisaB0uhkk/view?usp=sharing]
