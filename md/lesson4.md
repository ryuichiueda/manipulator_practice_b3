# 設計製作論実習3

## 第4回

千葉工業大学 上田 隆一

<br />

<p style="font-size:50%">
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
</p>

---

### 立ち上げ

* PCにロボットをUSBで接続して次のコマンドを実行
   * うまくいくとゆっくりマニピュレータが直立
```
$ sudo chmod 777 /dev/ttyUSB0 
$ roslaunch crane_x7_control crane_x7_control.launch
```
   * さらにアームを動かす
```
$ roslaunch crane_x7_bringup demo.launch fake_execution:=false
別の端末で$ rosrun crane_x7_examples pose_groupstate_example.py 
```

---

### ネットワークの設定（ラズパイ側）

* `/etc/hosts`と`~/.bashrc`の編集

```
$ sudo vi /etc/hosts
・・・
127.0.0.1 localhost
### 以下追加 ###
192.168.2.23 raspi
192.168.2.24 wsl
```


```
$ vi ~/.bashrc 
・・・
source /opt/ros/melodic/setup.bash
source /home/ubuntu/catkin_ws/devel/setup.bash
export ROS_MASTER_URI=http://wsl:11311      # wslになっていること
export ROS_HOSTNAME=raspi                   # raspiになっていること
$ source ~/.bashrc
```

---

### ネットワークの設定（WSL側）

* ssh接続可能にする
* `/etc/hosts`と`~/.bashrc`の編集

```
$ sudo apt install openssh-server
$ vi /etc/ssh/sshd_config
・・・
PasswordAuthentication yes      #yesにする
（vi終了）
$ sudo ssh-keygen -A
$ sudo service ssh restart
```

```
$ sudo vi /etc/hosts
・・・
192.168.2.23 raspi
192.168.2.24 wsl
```

```
$ vi ~/.bashrc 
・・・
export ROS_MASTER_URI=http://wsl:11311
export ROS_HOSTNAME=wsl
（vi終了）
$ source ~/.bashrc
```

---

### 接続確認

* WSLからラズパイ、ラズパイからWSLに`raspi`、`wsl`でssh接続

```
WSL側$ ssh ubuntu@raspi 
（パスワード）
ラズパイ側$ ssh ueda@wsl  #ユーザ名は適宜変更
（パスワード）
```

* ROSのマスタがWSL、CRANE-X7のコントローラがラズパイ側で動く

```
WSL側$ roscore 
ラズパイ側$ roslaunch crane_x7_control crane_x7_control.launch
```
