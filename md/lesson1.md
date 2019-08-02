# 設計製作論実習3

## 第1回

千葉工業大学 上田 隆一

<br />

<p style="font-size:50%">
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
</p>

---

## ROSのセットアップ

Windows編

---

### WSLでのROS環境構築

* 使うツール
    * WSL: [Windows Subsystem for Linux](https://ja.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
    * ROS: [robot operating system](http://wiki.ros.org/)
* 参考にしたサイト
    * WSL+ROS
	* [WSL(Windows Subsystem for Linux)でROSを動かす | naonaorange's blog](https://naonaorange.hatenablog.com/entry/2018/11/05/200715)
        * [WSL: Windows Subsystem for Linuxのインストールと設定 | demura.net](https://demura.net/lecture/15062.html)
        * [WSL: RvizやGazeboが起動しない | demura.net](https://demura.net/lecture/15304.html)
        * 注意: 参考になりますが、以後のスライドと設定が微妙に異なります。
    * SSH接続について
        * https://yuta0508.hatenablog.com/entry/2018/05/03/195616

---

### WSLのインストール

* Ubuntu 18.04 LTSをインストール（左図）
* 使えるようにシステムを設定（右図）

<img width="56%" src="./figs/ubuntu18_download.png" />
<img width="40%" src="./figs/wsl_enable.png" />


---

### ROSのインストール

* GitHub上のインストールスクリプトを利用
    * https://github.com/ryuichiueda/ros_setup_scripts_Ubuntu18.04_desktop

```
$ git clone https://github.com/ryuichiueda/ros_setup_scripts_Ubuntu18.04_desktop.git
$ cd ros_setup_scripts_Ubuntu18.04_desktop/
$ sudo apt update
$ sudo apt upgrade
$ ./locale.ja.bash
$ ./step0.bash
$ ./step1.bash
```

---

### 動作確認

```
$ source ~/.bashrc
$ roscore
... logging to /home/ueda/.ros/log/d26a0c78-b52f-11e9-a961-001c4252779e/roslaunch-1C7F-429.log
Checking log directory for disk usage. This may take awhile.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.

started roslaunch server http://localhost:49975/
ros_comm version 1.14.3


SUMMARY
========

PARAMETERS
 * /rosdistro: melodic
 * /rosversion: 1.14.3

NODES

auto-starting new master
process[master]: started with pid [439]
ROS_MASTER_URI=http://localhost:11311/

setting /run_id to d26a0c78-b52f-11e9-a961-001c4252779e
process[rosout-1]: started with pid [450]
started core service [/rosout]
```

* Windowsがネットワークのアクセスがどうのこうのと文句を言ってきたら「許可」で
* プログラムの終了は`Ctrl+C`で

---

### ワークスペース
