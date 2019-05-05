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
Options  (Option)
args     (Args)
subcommands (commandTree)

### 工具 
* https://www.json.cn/  json格式化查看