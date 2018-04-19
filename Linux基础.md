# Linux基础学习

- ### 硬链接（符号链接）
    指向目录中的目标文件的文件名，即一个文件指向另一个文件的文件名
    修改(读写)会影响彼此，删除不会影响彼此。
    命令：ln -s 源文件 目标文件
- ### 软链接
    修改(读写)会影响彼此，当删除的是软链接目录下的文件，不会影响其原来创始的文件；当删除的是最初创建它的文件，则也会删除其链接的文件。
    命令：ln 源文件 目标文件
- ### 软链接和硬链接的区别：
    软链接：    链接文件和被链接文件可以位于不同的文件系统	 可以建立指向目录的软链接。
    硬链接：	链接文件和被链接文件必须位于同一个文件系统	 不能建立指向目录的硬链接。
<br>
- ### grep
&emsp;&emsp;在文本文件中查找指定的字符串（按关键字提取文本文件中匹配的行）
| 参数 |  说明 |
| :---: | :---- |
| -c | 显示匹配行的次数 |
| -i | 搜索不区分大小写 |
| -n | 输出匹配行的行号 |
| -v | 输出不匹配的行 |
|-r|对目录（子目录）的所有文件递归进行|
| --color=auto | 匹配内容高亮显示 |
| -A NUM | 同时输出匹配行的后NUM行 |
| -B NUM | 同时输出匹配行的前NUM行 |
| -C NUM | 同时输出匹配行的前、后各NUM行 |

<font color=#0099ff size=3 face="黑体">例</font>：在文件myfile中查找包含字符串mystr的行
   &ensp;&ensp;&ensp; ``` $grep mystr myfile ```
<font color=#0099ff size=3 face="黑体">例</font>：显示myfile中第一个字符为字母的所有行
   &ensp;&ensp;&ensp;``` $grep '^[a-zA-Z]' myfile ```
<font color=#0099ff size=3 face="黑体">例</font>：在myfile中查找首字母不是#的行（过滤注释行）
    &ensp;&ensp;&ensp;``` $grep -v '^#' myfile ```
<br>

- ### sed的工作方式
    介绍：<ul><li> sed是一个流编辑器。它在命令中输入编辑命令、指定被处理的输入文件，在大屏幕上查看输出。
        <li>与vi不同的使sed可以过滤来自管道的输入。
        <li>sed默认不改变输入文件的内容，且标准输出结果，所以可以使用重定向将sed的输出保存到文件中。</ul>
    格式：
        ` sed [选项] [-e] cmd1 [-e] cmd2 ...[input-file] `
         <font color=#00ffff  size=3 face="黑体">注</font>：&nbsp;*可指定多个编辑命令，每个编辑命令前使用-e参数; 
           &ensp;&ensp;&ensp;&ensp; * cmd单引号括起；
         &ensp;&ensp;&ensp;&ensp;  * input-file 若省略，sed将从标准输入中读取输入<br>
    选项：` -r：使用扩展正则表达式进行模式匹配  `
         &ensp;&ensp;&ensp;&ensp;&ensp; `-i：直接对输入文件进行sed的命令操作`<br>
    <font color=#0099ff size=3 face="黑体">例</font>：删除文件中的第一行
      &ensp;&ensp;&ensp;&ensp;``` sed -e '1d'    //没有真正删除，-i 可实现真正删除   ```  
      <br>       

- ### awk    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//文本处理工具
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;命令：
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;` awk '{print $0}' /etc/passwd `  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `注：$0 表示所有参数，一整条记录；'{}'里是脚本；' awk实现取行给脚本 ';  `
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;` awk -F "：" '{print "name="$1 ",id="$6}' /etc/passwd `
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ``` 注：以：分隔，输出第1和6个参数,并按指定格式 ```<br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color=#0099ff size=3 face="黑体">例</font>：查看test.txt文件的20到30个记录的第1、3个字段
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;``` awk -F  ":" '{if(NR>=20 && NR<=30> print "name="$1 ",shell="$3)}' /etc/passwd  ```
    <p>
    <font face="微软雅黑" size=4> &ensp;&ensp;BEGIN和END模块：<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对于每个输入行，awk都会执行每个脚本代码一次。但在很多编程情况中，可能需要awk开始处理文件中的文本之前执行初始化代码，即BEGIN代码；处理输入文件中的所有行之后，可能需要计算打印或输出，即END代码；</font><br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color=#0099ff size=3 face="黑体">例</font>：1. `统计/etc/passwd账户人数`
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`  awk '{count++;} END{print "user conut is "count}' /etc/passwd ` <br>
       &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;2. `统计某文件夹下文件占用的字节数`
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`  ls -l | awk -F " " 'BEGIN {S=0;} {S=S+$5;} END {print "size="s/1024/1024"MB"}' ` 
   </p>

- ### vim编辑器
    三种模式：命令模式、输入模式、底线命令模式
    三种操作：
    1.` 进入文件，：后输入 /ss ，可搜索定位文件中的ss    //底线命令模式 `
    2.` 输入：set number     //显示文件中的更行行号`
    3.`shift+G //定位到最后一行 输入o：在文件最后一行进行输入`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color=#00ffff  size=3 face="黑体">注</font>:安装一个骚气的vim：wget -qO- https://raw.githubusercontent.com/xcracker/vim-deprecated/master/setup.sh | sh -x     
