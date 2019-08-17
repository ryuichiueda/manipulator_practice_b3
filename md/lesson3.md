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

### 自身のリポジトリを作る（1/2）

* やること
    * GitHubのアカウント作成
        * [この資料の「アカウント作成」まで](https://github.com/ryuichiueda/robosys2018/blob/master/10_git.md)
    * GitHubにリポジトリを追加
        * ROSで作ったパッケージと同じ名前にしておく
* 手順
    * リポジトリにサンプルプログラムをコミット

```
$ cd ~/catkin_ws/src/my_crane_x7/
$ git init
Initialized empty Git repository in /home/ueda/catkin_ws/src/my_crane_x7/.git/
$ git add -A 
$ git commit -m "Initial commit"
[master (root-commit) 91a17e8] Initial commit
 3 files changed, 337 insertions(+)
 create mode 100644 CMakeLists.txt
 create mode 100644 package.xml
 create mode 100755 scripts/pose_groupstate_example.py
```

---

### 自身のリポジトリを作る（2/2）

* 手順（続き）
    * GitHubへプッシュ

```
$ git remote add origin https://github.com/ryuichiueda/my_crane_x7
$ git push --set-upstream origin master
Username for 'https://github.com': ###GitHubのユーザ名###
Password for 'https://ryuichiueda@github.com':  ###パスワード###
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 4.31 KiB | 4.31 MiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To https://github.com/ryuichiueda/my_crane_x7
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```


---

### 実機を動かす 
