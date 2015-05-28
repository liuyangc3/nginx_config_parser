# 介绍 
提供HTTP接口用来添加/删除 Nginx 反向代理的节点

在config.py中指定Nginx Home和upstream配置文件的位置

# 依赖
tornado simplejson ply

# 获取upsteam配置
curl 127.0.0.1:8000/
```
{"ggpt": ["ip_hash", ["10.201.10.124:8080", "1", "10s"], ["10.201.10.224:8080", "1", "10s"]], 
"passport": ["ip_hupstreamash", ["10.201.10.126:8080", "1", "10s"], ["10.201.10.226:8080", "1", "10s"]]}
```
参数pretty可以生成可阅读格式

curl 127.0.0.1:8000/?pretty
```
{
    "ggpt": [
        "ip_hash",
        [
            "10.201.10.124:8080",
            "1",
            "10s"
        ],
        [
            "10.201.10.224:8080",
            "1",
            "10s"
        ]
    ],
    "passport": [
        "ip_hash",
        [
            "10.201.10.126:8080",
            "1",
            "10s"
        ],
        [
            "10.201.10.226:8080",
            "1",
            "10s"
        ]
    ],
}
```

# 列出所有的 upstream name 以及 server的数量
curl 127.0.0.1:8000/list
```
Name:                         Servers:
ggpt                          2
passport                      2
imapi                         2
cas                           2
sh                            2
```

# 查询指定 upstream 
curl 127.0.0.1:8000/pm?pretty
```
[
    [
        "10.201.10.125:8080",
        "1",
        "10s"
    ],
    [
        "10.201.10.225:8080",
        "1",
        "10s"
    ]
]

```
# 给指定 upstream 添加server
curl -XPOST 127.0.0.1:8000/pm?pretty -d '["10.201.10.233:3333", "111", "10s"]'


# 删除server
curl -XDELETE 127.0.0.1:8000/pm?pretty -d '10.201.10.233'