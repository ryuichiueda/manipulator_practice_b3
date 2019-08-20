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

### カメラを扱う

* シミュレータ（Gazebo）
* 実機

---

### シミュレーション環境の構築

* 準備
    * 自身のシミュレータ環境を設定するリポジトリを作る
        * `crane_x7_gazebo`を`my_crane_x7_gazebo`としてコピー
        * パッケージの名前が記述されているところを修正
* 手順
```
$ cd ~/catkin_ws/src/
$ cp -r crane_x7_ros/crane_x7_gazebo/ ./my_crane_x7_gazebo
$ cd my_crane_x7_gazebo/
### crane_x7_gazeboをmy_crane_x7_gazeboに変更 ###
$ sed -i 's/crane_x7_gazebo/my_&/g' CMakeLists.txt package.xml launch/crane_x7_with_table.launch 
$ ( cd ~/catkin_ws/ && catkin_make )
$ source ~/.bashrc 
```
* GitHubにリポジトリを作ってpushしておきましょう

---

### シミュレーション環境の動作確認

* とりあえず箱を隠してみましょう
    * `table.world`（worldファイル）
    * 次の手順で箱が消えることを確認

```
$ vi worlds/table.world 
（次のように箱の部分をコメントアウト）
・・・
<!-- 
    <model name="wood_cube_5cm">
      <include>
        <uri>model://wood_cube_5cm</uri>
      </include>

      <pose>0.20 0 1.0 0 0 0</pose>
    </model>
-->
・・・
（閉じる）
$ roslaunch my_crane_x7_gazebo crane_x7_with_table.launch 
```

---

### カメラをロボットに取り付ける

* ロボットのモデルのリポジトリを作成
    * `crane_x7_description`から`my_crane_x7_description`を作成
    * パッケージの名前が記述されているところを修正
* 手順

```
$ cd ~/catkin_ws/src/
$ cp -r crane_x7_ros/crane_x7_description/ ./my_crane_x7_description
$ sed -i 's/crane_x7_description/my_&/g' CMakeLists.txt package.xml launch/display.launch urdf/*
```
