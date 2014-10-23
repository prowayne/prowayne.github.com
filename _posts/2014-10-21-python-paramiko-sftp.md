--- 
title: 使用python的paramiko模块实现sftp
layout: post
category: python
---

## paramiko
使用python实现了ssh2协议,[项目地址][1]安装:

    sudo pip install paramiko

paramiko可以方便的实现远程主机的管理,这里使用它向远程主机发送或下载文件
    
[1]:https://github.com/paramiko/paramiko 'paramiko'   
   
## demo

```
import paramiko

class Sftp(object):
    def __init__(self, host, username, password, port=22):
        self.sftp = None
        self.sftp_open = False
        self.transport = paramiko.Transport((host, port))
        self.transport.connect(username=username, password=password)

    def _connection(self):
        if not self.sftp_open:
            self.sftp = paramiko.SFTPClient.from_transport(self.transport)
            self.sftp_open = True

    def get(self, remote_path, local_path=None):
        self._connection()
        self.sftp.get(remote_path, local_path)

    def put(self, local_path, remote_path=None):
        self._connection()
        return self.sftp.put(local_path, remote_path)

    def exists(self, path):"
        self._connection()
        try:
            self.sftp.stat(path)
        except IOError, e:
            if e[0] == 2:
                return False
        return True

    def mkdir(self, remote_dir):
        if not self.exists(remote_dir):
            self.sftp.mkdir(remote_dir)

    def close(self):
        if self.sftp_open:
            self.sftp.close()
            self.sftp_open = False
        self.transport.close()        
```

使用:

```
sftp = Sftp(host, username, password)
sftp.get(remote_path)
sftp.put(local_path, remote_path)
```

