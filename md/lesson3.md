# 設計製作論実習3

## 第3回

千葉工業大学 上田 隆一

<br />

<p style="font-size:50%">
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
</p>

---

### 実機を動かす（WSLの場合）

* `crane_x7_ros`がセットアップされたRaspberry Pi経由で接続
    * 現状、WSLからロボットへUSB接続できないのでしょうがなく
    * マシン同士を有線LANで接続し、以下の方法で接続
        * https://b.ueda.tech/?post=20190929_windows_raspi

---

### ラズパイ側の動作確認

* ラズパイにsshでログインして次のコマンドを実行
    * うまくいくとゆっくりマニピュレータが直立

```
$ roslaunch crane_x7_control crane_x7_control.launch
```


