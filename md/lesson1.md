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
