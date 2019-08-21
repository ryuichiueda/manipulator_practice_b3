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

### カメラをロボットに取り付ける<br />（準備）

* ロボットのモデルのリポジトリを作成
    * `crane_x7_description`から`my_crane_x7_description`を作成
    * パッケージの名前が記述されているところを修正
    * `my_crane_x7_gazebo`の中で`crane_x7_description`を`my_crane_x7_description`に変更

```
$ cd ~/catkin_ws/src/
$ cp -r crane_x7_ros/crane_x7_description/ ./my_crane_x7_description
$ sed -i 's/crane_x7_description/my_&/g' CMakeLists.txt package.xml launch/display.launch urdf/*
$ roscd my_crane_x7_gazebo/
$ sed -i 's/crane_x7_description/my_&/g' package.xml launch/crane_x7_with_table.launch
```

---

### カメラスタンドの取り付け（1/4）

* 手順
    * `my_crane_x7_description/urdf/crane_x7.xacro`ファイルに次のように1行追加
        * urdfファイル: ロボットのリンクや関節を記述したファイル 
        * xacroファイル: urdfファイルを簡潔に書いたもの

```
<?xml version="1.0"?>
<robot xmlns:xacro="http://ros.org/wiki/xacro">
・・・
  <xacro:include filename="$(find my_crane_x7_description)/urdf/crane_x7_wide_two_finger_gripper.xacro"/>
  <!--追加！！！-->
  <xacro:include filename="$(find my_crane_x7_description)/urdf/camera.urdf"/>
・・・
```

---

### カメラスタンドの取り付け（2/4）

* `camera.urdf`の記述
    * XMLで以下を記述
        * リンク（棒）を一本
        * ロボットとリンクを取り付ける固定関節を一個

```
<?xml version="1.0"?>

<robot name="camera">
  <link name="camera_stand_link">
      リンクに関する記述（次ページ）
  </link>

  <joint name="camera_stand_joint" type="fixed">
      関節に関する記述（次々ページ）
  </joint>

</robot>
```

---

### カメラスタンドの取り付け（3/4）

* リンクの記述
    * inertia: 慣性モーメント（この例では適当に軽く設定してある）
    * visual: 見かけの姿（20cm、半径1cmの丸棒）

```
<link name="camera_stand_link">
  <inertial>
    <mass value="1e-6"/>
    <origin xyz="0 0 0" rpy="0 0 0"/>
    <inertia ixx="1.0" ixy="0.0" ixz="0.0" iyy="1.0" iyz="0.0" izz="1.0"/>
  </inertial>
  <visual>
    <geometry>
      <cylinder length="0.20" radius="0.01"/>
    </geometry>
    <material name="white">
      <color rgba="0 0 0 1" />
    </material>
  </visual>
</link>
```

---

### カメラスタンドの取り付け（4/4）

* 関節の記述
