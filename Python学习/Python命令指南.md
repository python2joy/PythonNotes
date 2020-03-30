# Python命令指南
## 终端

|   命令    |    执行内容    | 备注 |
| :-------: | :------------: | :--: |
| command+Q |    退出终端    |      |
| command+T | 打开新的标签页 |      |
| command+N |  打开新的窗口  |      |







## 终端python

启动python：`ipython`







## pip

pip更新：
`python3 -m pip install --upgrade pip`
当使用这个出现报错的时候，可以使用下面的命令更新：
`python3 -m pip install -U pip`
pip更新非常重要，不然会导致某些库件安装不上。当库安装不上时一定要根据提示来执行库的安装。比如在安装dataset库时就一直提醒：
` You are using pip version 19.2.3, however version 20.0.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.`
对库进行更新后，就会发现能够正常安装。
需要注意的是在终端上通过pip命令更新会比较慢，如果网速较慢的话会导致安装不成功,出现`Read timed out`。可以多试几次，或者用手机给电脑开热点。

**pip更新所有库**

 查看可更新包：
` pip list  --outdated --format=columns`
 批量下载并更新：
 `pip install pip-review`
 `pip-review --local —interactive`



## Pycharm技巧

在一段代码后加`exit()`表示代码运行导致为止，后面的不再运行。