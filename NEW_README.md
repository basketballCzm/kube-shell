## hw-shell .json文档设计 
### 使用样例example 
* msgsend --pid=9876 funcname agr1=value1 arg2=value2 
* funcname --pid=9876 agr1=value1 arg2=value2  
上面两种的使用样例都能通过更改配置文件来实现 
#### example 
msgsend --pid=9876 registerUser username=czm password=123456  
对应的json文件为: (args也可以放在subcommand选项中)
```c
{
    "msgsend":{
        "options":{
            "--pid":{
                "name": "--pid",
                "value": 9876 
            }
        },
        "args":{
            "username":{
                "name": "username",
                "value": "czm"
            },
            "password":{
                "name": "password",
                "value": "123456"
            }
        },
        "subcommands":["registerUser"]
    }
}
```

### 数据结构分析 
commandTree节点  
command  (str)  
help     (str)  
usage    (str)  
Options  (Option)  
args     (Args)   
subcommands (commandTree)  

### 要求的格式 

格式                |     意义
----------          | ----------------------------
粗体	            |  命令行关键字（命令中保持不变、必须照输的部分）采用加粗字体表示。
斜体	            |  命令行参数（命令中必须由实际值进行替代的部分）采用斜体表示。
[ ]	                |  表示用“[ ]”括起来的部分在命令配置时是可选的。
{ x \| y \| ... }	    |  表示从两个或多个选项中选取一个。
[ x \| y \| ... ]	    |  表示从两个或多个选项中选取一个或者不选。
{ x \| y \| ... }*    |  表示从两个或多个选项中选取多个，最少选取一个，最多选取所有选项。
[ x \| y \| ... ]*    |  表示从两个或多个选项中选取多个或者不选。
&<1-n>	            |  表示符号&前面的参数可以重复1～n次。
\#                   |  由“#”开始的行表示为注释行。  
上面的要求可以通过提示信息显示   
msgsend --pid=9876 registerUser --usage 显示提示信息usage:   
msgsend --pid=9876 registerUser --help  显示提示信息help: 

### 运行 
pip install prompt_toolkit   
pip install Pygments   
pip install fuzzyfinder   


### 工具 
* [json格式化查看](https://www.json.cn/)