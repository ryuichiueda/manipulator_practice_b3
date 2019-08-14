# 設計製作論実習3

## 第2回

千葉工業大学 上田 隆一

<br />

<p style="font-size:50%">
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
</p>

---

## <span style="text-transform:none">MoveIt!</span>を使う

* [マニピュレータの制御とMoveIt!の利用](https://gbiggs.github.io/ros_moveit_rsj_tutorial/manipulators_and_moveit.html)

---

### 題材

* CRANE-X7のROSパッケージ
    * まずは[README](https://github.com/rt-net/crane_x7_ros/blob/master/README.md)をよく読む
        * 実機についての言及がありますが、まだ実機は扱いません
        * Gazeboのシミュレーションのところをよく読みましょう

---

### 起動

```
$ roslaunch crane_x7_gazebo crane_x7_with_table.launch
```

<img width="60%" src="./figs/launch_x7_gazebo.png" />

* 左下: Gazebo
    * シミュレータ
* 右上: RViz 
    * ROSのモニタリング/コントロールツール

---

### <span style="text-transform:none">MoveIt!</span>の操作

* こちらの資料を使わせていただきましょう
    * [マニピュレータの制御とMoveIt!の利用](https://gbiggs.github.io/ros_moveit_rsj_tutorial/manipulators_and_moveit.html)
        * [ハードウェアのロボットを制御](https://gbiggs.github.io/ros_moveit_rsj_tutorial/manipulators_and_moveit.html#%E3%83%8F%E3%83%BC%E3%83%89%E3%82%A6%E3%82%A7%E3%82%A2%E3%81%AE%E3%83%AD%E3%83%9C%E3%83%83%E3%83%88%E3%82%92%E5%88%B6%E5%BE%A1)のRViz上での操作から順番に操作方法を確認
        * ちょっとボタンやプルダウンの項目が違うので注意
* やること
    * ランダムに姿勢を選んで計画->実行

---

## サンプルコードを動かす

---

### 準備

* Gazeboを立ち上げておく
```
$ roslaunch crane_x7_gazebo crane_x7_with_table.launch
```
<img width="50%" src="../figs/gazebo_hand.png" />
* サンプルプログラムのディレクトリに移動
```
$ cd ~/catkin_ws/src/crane_x7_ros/crane_x7_examples/scripts/
```




---

### ハンドの開閉

* `gripper_action_example.py`
    * ハンドを開いて閉じる
    * 動かし方
```
$ rosrun crane_x7_examples gripper_action_example.py 
```

---

### ハンドが開閉する仕組み

* ROSのアクションという仕組みを使用
    * サンプルプログラムと、裏で動いているシステム側のプログラム（システムプログラムと呼ぶ）が連携して動作
        * サンプルプログラム: ある動作をシステムプログラムに依頼して待つ
        * システムプログラム: ロボットに動きを伝える
    * このような構成をとることでGazeboでも実機でも同じサンプルで動く
        * ROSの利点
* [解説つきコード](https://github.com/ryuichiueda/my_crane_x7_samples/blob/master/scripts/gripper_action_example.py)
