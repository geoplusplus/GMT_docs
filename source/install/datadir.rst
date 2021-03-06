GMT 数据库的建立
========================

在使用 GMT 绘图时，经常会用到某些数据，比如地形起伏数据、正确的国界线数据、
中国地质构造分界线数据等等。
社区已经提供了一个数据集，包含了一些常见的数据：http://gmt-china.org/datas/。

这些数据有一共性：固定性。即这些数据几乎不需要改动就可以直接使用。
同时，这些数据很有可能会在用于不同的图件。如果在每一个绘图脚本的路径上
都复制一份，则会造成数据冗余。如果将数据放在某个特定的目录，需要在命令中
指定该绝对路径，而绝对路径往往很长，万一路径变了还要修改所有脚本，很麻烦。

从原理上说，当 GMT 在命令中遇到某个文件时，首先会在当前目录下寻找该文件，如果
找不到，则会到环境变量 ``GMT_DATADIR`` 中寻找。若环境变量 ``GMT_DATADIR`` 未定义，
则在默认路径下寻找（不同的操作系统，默认路径不同）。

因而，最简单的做法就是把所有的地形数据、国界数据等等，都放在默认路径下，构成
一个自己的 GMT 数据库。此时，在 GMT 命令中直接使用文件名即可，既不需要将数据
复制到当前目录，也不需要指定绝对路径。

如果不想使用默认路径，则需要修改 ``GMT_DATADIR`` 环境变量。下面介绍不同系统的
默认路径和 ``GMT_DATADIR`` 环境变量。

Linux 和 Mac
------------

Linux 和 Mac 下的默认路径都是 ``~/.gmt/`` 。

如果想要修改环境变量，则在 shell 的配置文件中加入 ``GMT_DATADIR`` 即可。在 bash 中是::

    export GMT_DATADIR=/path/to/my/gmt/database

如果喜欢将不同的数据分类放在不同的目录下也可以，可以添加多个目录，多个目录中间
用 ``:`` 分隔即可::

    export GMT_DATADIR=/path/to/my/coast:/path/to/my/boundary

需要注意的是，在 Linux 上 ``GMT_DATADIR`` 不具有递归性，即该路径的子路径是无效的，
如果要包含，要自己再添加。而在 Mac 上子路径有效，GMT 会先找父路径再找子路径。

Windows
-------

Windows下的默认路径是 ``C:\Users\用户名\.gmt`` 。

需要注意：正常情况下无法通过文件管理器直接建立名为 ``.gmt`` 文件夹。正确的做法是，
打开“命令提示符”，执行命令 ``mkdir .gmt`` 以创建该文件夹。

若C盘容量不够，可以在其他盘下建GMT数据库数据库。具体做法是，

#. 建立GMT数据库目录 ``F:\GMTDATABASE`` （具体路径自行决定）
#. 打开“我的电脑”->“属性”->“高级”->“环境变量”
#. 添加环境变量，变量名为 ``GMT_DATADIR`` ，值为 ``F:\GMTDATABASE``
#. 重启电脑使得环境变量生效
