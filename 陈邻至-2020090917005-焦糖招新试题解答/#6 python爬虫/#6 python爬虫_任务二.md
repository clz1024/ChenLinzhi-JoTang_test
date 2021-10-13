# 一、前期准备

## 1.题目分析

### 数据库设计

数据库是存放数据的仓库。它的存储空间很大，可以存放百万条、千万条、上亿条数据。但是数据库并不是随意地将数据进行存放，是有一定的规则的，否则查询的效率会很低。当今世界是一个充满着数据的互联网世界，充斥着大量的数据。即这个互联网世界就是数据世界。数据的来源有很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、音乐、声音都是数据。在这个题目中，我选用MySQL作为数据库，SQLyog作为数据库管理系统。

## 2.环境配置

### MySQL与SQLyog

MySQL是一个关系型数据库管理系统,是Oracle 旗下产品.MySQL是最好的 RDBMS (Relational Database Management System，关系数据库管理系统) 应用软件之一。它具有体积小、速度快、总体拥有成本低等优点。MySQL的安装较为复杂，需要配置环境变量，创建“my.ini”文件并在cmd中启动，连接电脑，设置用户名及密码，按CSDN上的教程完成顺利安装而SQLyog 是一个快速而简洁的图形化管理MYSQL数据库的工具，它能够在任何地点有效地管理你的数据库，由业界著名的Webyog公司出品。使用SQLyog可以快速直观地从世界的任何角落通过网络来维护远端的MySQL数据库。说白了就是为了方便操作MySQL数据库而开发的一种图形化管理工具！

## 3.技术学习

#### 数据库基本知识与操作

主要是通过B站教程观看sqlite数据库入门，掌握了数据库基本的连接，增删查改等操作。

# 二、解题过程

## 爬取过程

### 1.寻找端口

动态网页无法直接找到源代码，查询资料后得知每页评论都有端口。查询得到b站评论端口后进入，即得到包含评论内容的源代码。

### 2.爬取每条评论的内容

 首先通过一次正则表达式定位到包含所有评论的源代码，第二次正则解析出包含文本、链接、点赞数、时间等所有需要爬取的信息的单条评论的源代码。接下来开始爬取我们需要的信息：

```python
# 爬取评论内容
            obj2 = re.compile(r'"message":"(?P<commend>.*?)","plat"', re.S)
            result2 = obj2.finditer(page)
            for i in result2:
                commend = i.group('commend')
                commend = commend.replace('\\n', '\n')
                commend = commend.replace('\\u0026#34;', ' ')
```

```python
# 爬取作者名字
            obj3 = re.compile(r'"uname":"(?P<name>.*?)","sex', re.S)
            result3 = obj3.search(page)
            name = it3.group('name')
```

```python
# 爬取时间
            obj4 = re.compile(r'"ctime":(?P<time>.*?),"rp', re.S)
            result4 = obj4.search(page)
            ctime = it4.group('time')
            newtime = time.localtime(int(ctime))
                baizhuntime = time.strftime("%Y-%m-%d %H:%M:%S", newtime)
```

```python
# 爬取点赞数
            obj5 = re.compile(r'"like":(?P<like>.*?),"action"', re.S)
            result5 = obj5.search(page)
             like = it5.group('like')             
```

```python
# 爬取链接
            obj6 = re.compile(r'"rpid_str":"(?P<link>.*?)","', re.S)
            result6 = obj6.search(page)
            link = it6.group('link')
            link = 'https://t.bilibili.com/560233713032161611/#reply' + linkite('链接:'+link+'\n')
                # links.append(link)


```

```python
# 爬取作者空间链接
            obj8 = re.compile(r'"mid":"(?P<link2>.*?)","un', re.S)
            result8 = obj8.search(page)
            kongjianlink = it8.group('link2')
            kongjianlink = 'https://space.bilibili.com/' + kongjianlink + '?spm_id_from=444.42.0.0'
            kongjianlink_path = f'C:/Users/LuoSa/Desktop/休对故人思故国/2021焦糖招新-赖子秋/#5-赖子秋/任务二/评论{code}/作者空间链接.txt'
                # with open(kongjianlink_path, mode="w") as li_f:
                    # li_f.write(kongjianlink_path)
```

```python
# 爬取作者头像
            obj7 = re.compile(r'"avatar":"(?P<img>.*?)","', re.S)
            result7 = obj7.search(page)
            img_content = it7.group('img')
            img_content = requests.get(img)
            img_path = f'C:/Users/LuoSa/Desktop/休对故人思故国/2021焦糖招新-赖子秋/#5-赖子秋/任务二/评论{code}/头像.jpg'
                with open(img_path, mode="rb") as img_f:
                    img_content = img_f.read()
                    # img_f.write(img.content)
```

其中爬取评论内容、作者、点赞数、作者头像、评论链接和空间链接较为简单，基本和任务一类似。爬取时间时需要将爬取到的时间戳转化为标准格式的时间后，再写入数据库中。

## 数据库设计

### 1.创建储存爬取内容的表

使用pymysql库中的connect函数连接到我们创建好的数据库。然后利用游标cursor以及sql基本语句创建库。

```python
db = pymysql.connect(host='localhost', user='root', password='111111', port=3306)
cursor = db.cursor()
cursor.execute("CREATE DATABASE IF NOT EXISTS spider")

db = pymysql.connect(host='localhost', user='root', password='111111', port=3306, db='spider')
cursor = db.cursor()
sql1 = 'DROP TABLE IF EXISTS 评论详情;'
sql2 = 'CREATE TABLE 评论详情 (' \
       '评论 TEXT,' \
       '评论链接 VARCHAR(255),' \
       '作者 VARCHAR(255),' \
       '发布时间 VARCHAR(255),' \
       '点赞数 VARCHAR(255),' \
       '空间链接 VARCHAR(255),' \
       '头像图片 Blob)' \
```

其中文本为TEXT类型，头像为BLOB类型，其余都是varchar类型。

### 2.向表中插入数据

```python
				   sql3 = 'INSERT INTO 评论详情(评论内容, 链接, 作者, 发布时间, 点赞数, 空间链接, 头像图片) VALUES(%s, %s, %s, %s, %s, %s, %s)'
                    xinxi = (commend, link, name, otherStyleTime, like, link2, img)
                    cursor.execute(sql3, xinxi)
                    db.commit()
                    print('OK,', code)
```

## 最终效果图

### 存储评论者获赞、头像、链接及名称的数据库

[![5uxmrD.png](https://z3.ax1x.com/2021/10/13/5uxmrD.png)](https://imgtu.com/i/5uxmrD)

### 评论者头像

[![5uxnqe.png](https://z3.ax1x.com/2021/10/13/5uxnqe.png)](https://imgtu.com/i/5uxnqe)

# 四、遇到的问题及解决方法

## 1.不了解时间戳

刚刚拿到评论端口时，除时间以外的其他数据都能够直接找到，而ctime处是一串整型数字。通过查询资料后，了解到了时间戳，以及利用time库中的strfttime函数将时间戳转化为标准格式时间的方法。

## 2.爬取评论内容时出现乱码

通过正则解析出的评论内容中，换行符和空格被转换为\n、\u0026#34，通过查阅资料了解到Python中的replace函数，可以直接将这些字符去除。

## 3.图片无法直接写入数据库

由于刚刚开始接触数据库，对数据库内部结构不太了解，直接将图片内容写入数据库中，导致出现一串乱码。经过优化后，首先将图片存到本地，然后从本地读取数据内容存到数据库中。

# 四、总结反思

完成这个题目让我掌握了许多知识、加深了对浏览器使用的理解。希望以此为契机进一步学习python数据分析，同时通过对浏览器的探索与熟练掌握进一步便利学习与生活。

