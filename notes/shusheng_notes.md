# 一、Linux基础知识
这部分主要是为了熟悉InternStuido开发机环境，本质是采用Docker 容器构建的linux虚拟机。我对本身比较熟悉，这里主要熟悉开发机的使用，ssh连接，端口映射等。
开发机器里运行python脚本
注意：运行前 安装gradio (pip install gradio==4.29.0)
```python
import socket
import re
import gradio as gr
 
# 获取主机名
def get_hostname():
    hostname = socket.gethostname()
    match = re.search(r'-(\d+)$', hostname)
    name = match.group(1)
    
    return name
 
# 创建 Gradio 界面
with gr.Blocks(gr.themes.Soft()) as demo:
    html_code = f"""
            <p align="center">
            <a href="https://intern-ai.org.cn/home">
                <img src="https://intern-ai.org.cn/assets/headerLogo-4ea34f23.svg" alt="Logo" width="20%" style="border-radius: 5px;">
            </a>
            </p>
            <h1 style="text-align: center;">☁️ Welcome {get_hostname()} user, welcome to the ShuSheng LLM Practical Camp Course!</h1>
            <h2 style="text-align: center;">😀 Let’s go on a journey through ShuSheng Island together.</h2>
            <p align="center">
                <a href="https://github.com/InternLM/Tutorial/blob/camp3">
                    <img src="https://oss.lingkongstudy.com.cn/blog/202406301604074.jpg" alt="Logo" width="20%" style="border-radius: 5px;">
                </a>
            </p>

            """
    gr.Markdown(html_code)

demo.launch()
```

在本地（也就是使用浏览器的机器上）使用powerShell（不需要连接开发机）运行端口转发命令
```shell
ssh -p 48505 root@ssh.intern-ai.org.cn -CNg -L 7860:127.0.0.1:7860 -o StrictHostKeyChecking=no
```

访问网页  [http://127.0.0.1:7860](http://127.0.0.1:7860) 可以看到

![image.png](https://cdn.nlark.com/yuque/0/2024/png/25427778/1720600695854-068bd405-3a6d-49d3-b2de-6e83a847f26f.png#averageHue=%23ecf2f8&clientId=u1baac856-e803-4&from=paste&height=897&id=uea631c92&originHeight=1345&originWidth=2110&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=593452&status=done&style=none&taskId=ufb6ce727-b361-4f9e-817a-51c35a9306a&title=&width=1406.6666666666667)

# 二、python基础知识
要求写一个wordCount程序
需求较为简单，直接使用正则去除标点符号，遍历文本，使用字典统计。
```python
import re

#统计方法
def wordcount(inputText):
    # 转换文本为小写
    inputText = text.lower()
    # 使用正则表达式去除标点符号
    inputText = re.sub(r'[^\w\s]', '', text)
    
    # 分割文本为单词列表
    words = inputText.split()
    # 创建一个字典来存储单词计数
    word_counts = {}
    
    # 遍历单词列表并更新字典中的计数
    for word in words:
        if word in word_counts:
            word_counts[word] += 1
        else:
            word_counts[word] = 1
    return word_counts

# 测试数据
text = """
Got this panda plush toy for my daughter's birthday,
who loves it and takes it everywhere. It's soft and
super cute, and its face has a friendly look. It's
a bit small for what I paid though. I think there
might be other options that are bigger for the
same price. It arrived a day earlier than expected,
so I got to play with it myself before I gave it
to her.
"""

# 打印结果
result = wordcount(text)
print(result)
```
开发机运行无误
![image.png](https://cdn.nlark.com/yuque/0/2024/png/25427778/1721010622402-27300364-b3ed-4faf-903e-7a3ac9adb45d.png#averageHue=%23fbf9f7&clientId=u44ef13df-0f5b-4&from=paste&height=126&id=u6c4aaa2c&originHeight=189&originWidth=1338&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=41375&status=done&style=none&taskId=ua5252041-f678-432b-b069-a8523129b10&title=&width=892)
使用vscode运行，结果无误
![image.png](https://cdn.nlark.com/yuque/0/2024/png/25427778/1721010997027-35822402-7b88-46dc-aec6-113e21a46d0b.png#averageHue=%231e1e1e&clientId=u44ef13df-0f5b-4&from=paste&height=761&id=ude015db8&originHeight=1141&originWidth=2128&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=177567&status=done&style=none&taskId=u7f96891b-97eb-48ca-803a-13c7f202e1a&title=&width=1418.6666666666667)
# 三、Git基础
## 3.1 破冰活动

- **git 安装**
- **Fork 目标项目 **
- **拉取到本地 **
- **切换分支**
- **创建文件**

**上面部分之前就熟悉，很快完成略过**

- **提交更改到分支**

**这里需要先配置账号信息**
```bash
git config user.name ""
git config user.password ""
git config user.email ""

```
上传成功后可以在github看到新增加的文件
![image.png](https://cdn.nlark.com/yuque/0/2024/png/25427778/1721017777608-07d40666-df21-4529-b3c3-3cb12c4eb177.png#averageHue=%23d1ad7d&clientId=u44ef13df-0f5b-4&from=paste&height=581&id=u5ce4a9db&originHeight=871&originWidth=2380&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=214356&status=done&style=none&taskId=u889f2f26-5721-4986-934f-877a2c42d8a&title=&width=1586.6666666666667)

将分支PR到Tutorial，  等待审核
![image.png](https://cdn.nlark.com/yuque/0/2024/png/25427778/1721018782175-d4a0f9f1-a4ec-4c96-b33c-ff327841b115.png#averageHue=%23c5b182&clientId=u44ef13df-0f5b-4&from=paste&height=831&id=ka3TL&originHeight=1246&originWidth=1722&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=221965&status=done&style=none&taskId=u5f5641cb-89bd-4b6e-8dc4-28a2c2fc1df&title=&width=1148)

## 3.2 构建个人项目
github 创建一个仓库 [https://github.com/WMing404/shusheng-demo](https://github.com/WMing404/shusheng-demo)
![image.png](https://cdn.nlark.com/yuque/0/2024/png/25427778/1721019897733-0fbc17d9-2ed7-402d-8b2f-2ecdf52de00c.png#averageHue=%23ccab80&clientId=u44ef13df-0f5b-4&from=paste&height=745&id=u44fa5275&originHeight=1117&originWidth=2193&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=214125&status=done&style=none&taskId=ub0002faf-5cfa-41f5-8278-217062d18e9&title=&width=1462)

上传笔记，笔记链接为：(https://github.com/WMing404/shusheng-demo/blob/main/notes/shusheng_notes.md)


