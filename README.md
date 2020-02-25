# AliWenXue
阿里文学JS破解
目标网站：aHR0cHM6Ly93d3cuYWxpd3guY29tLmNuL3JlYWRlcj9iaWQ9NjcyNTgwNiZjaWQ9NzIxNjY1


1.首先F12刷新网页可以看到下面请求



这个sign一看就是个加密。再看一看返回正文内容：

这个ChapterContent一看就是加密的，全局搜索这个关键字：

这个decodeCont看上去就是解密的地方，打上断点跟进去看一下

直接把整个函数扣下来改写一下，传入密文就可以了。

然后sign的值直接可以从html页面搜索拿到（这个sign我真的找了好久，最后请教别人在html页面里面找到的。。）


===========================================================
中间碰到一个坑搜索了好久才解决，运行demo.py的时候
一直会报如下错误：
Exception in thread Thread-1:
Traceback (most recent call last):
  File "D:\tools\Python3.6\lib\threading.py", line 916, in _bootstrap_inner
    self.run()
  File "D:\tools\Python3.6\lib\threading.py", line 864, in run
    self._target(*self._args, **self._kwargs)
  File "D:\tools\Python3.6\lib\subprocess.py", line 1083, in _readerthread
    buffer.append(fh.read())
UnicodeDecodeError: 'gbk' codec can't decode byte 0xb4 in position 211: illegal multibyte sequence

Traceback (most recent call last):
  File "D:/zjf_workspace/003、自己测试用的/002加密和验证码破解/02-js加密破解/023、烯牛数据/执行.py", line 44, in <module>
    result_decode = get_decode(data)
  File "D:/zjf_workspace/003、自己测试用的/002加密和验证码破解/02-js加密破解/023、烯牛数据/执行.py", line 34, in get_decode
    result_decode = ct.call('decode_get_data', data)
  File "D:\tools\Python3.6\lib\site-packages\execjs\_abstract_runtime_context.py", line 37, in call
    return self._call(name, *args)
  File "D:\tools\Python3.6\lib\site-packages\execjs\_external_runtime.py", line 92, in _call
    return self._eval("{identifier}.apply(this, {args})".format(identifier=identifier, args=args))
  File "D:\tools\Python3.6\lib\site-packages\execjs\_external_runtime.py", line 78, in _eval
    return self.exec_(code)
  File "D:\tools\Python3.6\lib\site-packages\execjs\_abstract_runtime_context.py", line 18, in exec_
    return self._exec_(source)
  File "D:\tools\Python3.6\lib\site-packages\execjs\_external_runtime.py", line 87, in _exec_
    output = self._exec_with_pipe(source)
  File "D:\tools\Python3.6\lib\site-packages\execjs\_external_runtime.py", line 103, in _exec_with_pipe
    stdoutdata, stderrdata = p.communicate(input=input)
  File "D:\tools\Python3.6\lib\subprocess.py", line 863, in communicate
    stdout, stderr = self._communicate(input, endtime, timeout)
  File "D:\tools\Python3.6\lib\subprocess.py", line 1133, in _communicate
    stdout = stdout[0]
IndexError: list index out of range


解决步骤
1、进去错误这个D:\tools\Python3.6\lib\subprocess.py文件


2、搜索：encoding=
这个搜索方式，是我找了好一会才懂，所以记录下来，大家可以参考下。

3、修改编码格式为utf-8

注意事项：
建议注释一行，毕竟修改的是模块的源码，万一弄错了好改回来。



至此修改完毕，可以尝试运行了
