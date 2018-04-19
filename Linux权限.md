## Linux基本权限<br>
文件/目录权限：

        r--读
        w--写
        x--执行
        '-' --没有权限
三类用户：

        user  文件所属用户    
        group 文件所属组      
        other 其他用户        

### 与权限相关的命令
     查看目录/文件的权限：ls -l 
    
- chmod <br>
    改变文件或目录的权限
    命令：

        chmod 777 test //设置文件权限（8进制）
        getfacl test/  //查看三类用户对文件所有的权限
        chmod o+x test //给其他用户添加执行权限
        chmod -R 777 home/ //将home文件夹的权限设为777
        注：-R表示对目录中的所有文件或子目录进行递归操作
        

- chown <br>
    改变文件或目录的属主（所有者） <br>
       ` chown eagle test//将test文件所属的主改为eagle`
       <br>

- chgrp <br>
    改变文件或目录所属的组 <br>
       ` chgrp eagle test//将test文件所属的组改为eagle `
       <br>

- umask

            设置文件权限的缺省生成掩码
            *新建目录的访问权限最大为777，新建文件的访问权限最大为666     

        例： umask -S 022 work //设置work目录下所要新建文件的权限
    格式：`umask u1u2u3`

            * u1:表示不允许属主的权限；
            * u2:表示不允许同组人有的权限；
            * u3:表示不允许其他人有的权限；
    设置umask的方法：
        
        *RHEL/CentOS默认在/etc/bashrc中设置；
        *用户可在~/.bashrc中重新设置；
        *在/etc/fstab的文件系统挂装参数中指定；         
       
### setfacl命令          &emsp;&emsp;&emsp;&emsp;&emsp;&emsp; //set file acl权限

            相比于chmod，setfacl可以使用一条命令设置多个权限。
      语法：
            setfacl [-R] {-m|-x} <rules> <files or directory>

      说明：

            -R选项用于对文件递归操作
            -m表示修改acl权限    
            -x选项表示删除acl权限
            rules为要设置的acl权限

         例： setfacl -m u:xiaohong:rx,u:xiaozhang:rx,o::r-- showip 
        //对于showip文件，xiaohong和xiaozhang可读可执行，其他用户只可读，确保了安全性 
                               
