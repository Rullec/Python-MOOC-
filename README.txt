这个爬虫可以自动爬取网络小说，并且保存到本地磁盘指定路径，支持进度条显示。

技术路线：requests-bs4-re

主要分为以下几个模块：
1.获取输入，并且查找是否存在该小说。
2.如果存在该小说，则返回目录页url，如果不存在，重新输入。	FindIndex()函数
3.进入该小说目录页，并且在指定路径建立该小说文件夹。如果路径下发现已经有了该小说文件夹，默认选择更新(即保持旧章节不动，)。
4.爬取并显示总进度条，随机更换headers；				Spider()函数，GetHtmlText()函数实现
5.关键字替换和屏蔽，利用正则表达式替代文字中的广告+乱码 	ProcName()函数
6.爬取结束

代码过程中所遇到的问题和心得总结：

1.遭遇了\a这一逃逸字符的问题，总是报错。国内找不到答案，之后在stackoverflow上找到了答案

2.在bs4解析时遭遇了len(Nonetype)的调用,是编码的锅，在https://github.com/cobrateam/django-htmlmin/issues/74找到了答案

3.尽管做了很大努力，但也许程序的健壮性有待提高

4.使用Pycharm，中途把源文件的编码改错了，改了很久也不好。最后使用idle重新保存一下，马上就解决了

5.编码为utf-8，写入需要用GB2312简体中文Windows大部分是GB2312，会出现'gb2312' codec can't encode character 错误
	解决： with open(path,'wr',encoding='utf-8')。因为windows系统的新txt文件，默认GBK，改成默认utf8即可