# 一、前期准备

## 1.题目分析

### 初识爬虫

经过学习，我对爬虫有了初步的了解：爬虫就是让程序代替人去浏览网页，从而快速高效地达成我们的一些要求。爬虫在生活中的应用很广泛：如爬取大量新闻信息、购物节秒杀、脚本刷网课（bushi。而这道题则是使用了Python这门脚本语言，通过爬取网页源代码，进而解析出我们所需要的信息。

那么，为什么要使用Python这门语言呢？我觉得有一下几个原因（1）语法简单，易于学习上手（2）在浏览网页、解析数据等方面都显得比较活跃，python拥有numpy、re、bs4、lxml等工具在科学计算方面十分有优势。（3）Python具有强大的编程能力、非常强大的数据分析能力，并且还可以利用Python进行爬虫，写游戏，以及自动化运维，能够大大的提高数据分析的效率。

## 2.环境配置

### Python

（之前就已经完成了下载及环境配置，完成此题目时又重新检查了环境变量，更新了最新版的python3.9.7，值得注意的是此次用IDE插件多线程下载使下载速度大大提升）下载完成后，进行自定义安装，之后在环境变量的path选项中对python进行添加，至此完成对python的安装。

## 3.技术学习

#### python基本语法

由于有C语言的基础，python语言的入门相对容易，通过菜鸟教程及B站的一些教学视频，很快入门并掌握基本语法。重点关注了Python语言中基本的循环语句、列表、字典、元组其中对字典的一些相关操作反复学习、重点要求，为后面数据分析提供坚实的理论知识。

#### python相关工具包的使用

主要通过B站python数据分析教程进行了学习，大致了解了python数据分析中常用的Numpy、bs4以及re、lxml几个库。同时重点了解requests、re、bs4几个模块，方便后期完成代码编写时的调用。

#### 简要了解web相关知识（重点在url）

在WWW（World Wide Web，万维网）上，每一信息资源都有统一的且在网上唯一的地址，该地址就叫URL（Uniform Resource Locator,统一资源定位器），它是WWW的统一资源定位标志，就是指网络地址。一个完整的url（https://www.bilibili.com/video/BV1Cx411m7n7?from=search&seid=8941458026121594216）一般包涵以下几个部分：协议（https://），网址（www.bilibili.com），文件地址（/video/BV1Cx411m7n7?from=search&seid=8941458026121594216）。而网址去掉www.剩下如bilibili.com,则这个部分叫做域名，值得注意的是此题中字典的键便是各个网址的域名。其中.com则称为定级域名，其中.com表示商业组织.org表示非营利性组织.gov表示政府机构.edu表示教育及科研机构，另外.cn表中国.us表美国.jp表日本.cc则代表了澳大利亚。有时候公司的子公司会采取二级域名的形式例如腾讯网（qq.com）而子产品QQ邮箱（mail.qq.com）从域名后的第一个'/'开始到最后一个'/'是虚拟目录部分,从最后一个'/'到#为止是文件名部门，#之后就是锚部分。虚拟目录，稳健部门，锚都不是必须的。

# 二、解题过程

## 第一部分：模块引入

正式开始着手代码的编写，首先引入该题目所需要的python中的模块。它们分别是：

```python
import requests  # 用于请求网页源代码
import re        #主要利用其中的re.compile对目标内容用正则表达式进行匹配
from lxml import etree         #etree.HTML()可以用来解析字符串格式的HTML文档对象，将传进去的字符串转变成_Element对象。
from bs4 import BeautifulSoup  # 以上三个用于解析出我们需要的信息
import numpy as np             #主要用于程序中的数学/科学计算
import os        # 用于创建我们需要的文件夹
```

## 第二部分：进入新闻主页，并拿到所有的新闻的网址

每页新闻的网址有一定规律：第一页网址为https://sise.uestc.edu.cn/xwtz/tzgg/yb.htm，剩余网页的网址为在yb后加上由4递减的数字。拿到网页源代码后，找到每条新闻的超链接，通过正则解析洗出后存储到链表中。

``` python
page_content = ""
url_list2 = []
headers = {
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36'
}
while page < 6:
    if page == 1:
        url = "https://sise.uestc.edu.cn/xwtz/tzgg/yb.htm"
    else:
        code = 6-page
        url = f"https://sise.uestc.edu.cn/xwtz/tzgg/yb/{code}.htm"
    resp = requests.get(url)
    resp.encoding = "UTF-8"
    # session = requests.Session()
    # resp = session.get(url=url, headers=headers).text.encode('latin1')
    page_content += resp.text
    # print(resp.text)

    obj1 = re.compile(r'/system/resource/js/ajax.js">(?P<news>.*?)<link rel="stylesheet" Content-type="text/css" ', re.S)
    result1 = obj1.finditer(page_content)
    # print(result1)
    for it in result1:
        news = it.group('news')
        # print(ul)
        if page == 1:
            obj2 = re.compile(r'<a href="../../(?P<url>.*?)">', re.S)
        else:
            obj2 = re.compile(r'<a href="../../../(?P<url>.*?)">', re.S)
        result2 = obj2.finditer(news)
        # print(result2)
        for itt in result2:
            url ='https://sise.uestc.edu.cn/' + itt.group('url')
            # print(url)
            url_list2.append(url)

    page += 1
    # 去重
    url_list = []
    for i in url_list2:
        if not i in url_list:
            url_list.append(i)
```

## 第三部分：通过os模块创建每个新闻对应的文件夹

这一步较为简单，主要是熟悉os模块的使用。首先为了给文件夹命名，应该先拿到每条新闻的标题，为方便后面使用，我们将其存放在列表中。最后通过调用os库的mkdir来创建文件夹。

``` python
for r in url_list:
    # print(r)
    resp = requests.get(r)
    resp.encoding = "UTF-8"
    child_page_content = resp.text
    # print(child_page_content)
    obj3 = re.compile(r'<title>(?P<titles>.*?)-', re.S)
    result3 = obj3.finditer(child_page_content)

    for title in result3:
        title = title.group('titles')
        # print(title)
        titles.append(title)

renamed_titles = rename_duplicate(titles, False)

for tt in renamed_titles:
    # print(tt)
    os.mkdir(f'D:/Anaconda3/软网爬虫/任务一/{tt}')
```

## 第四部分：爬取标题、内容、时间

这几项内容爬取方法类似，这里使用了xpath来进行解析，爬取到内容后写入到txt文件，并放入文件夹中。

```python
for r in url_list:
    # print(r)
    txt_path = f'D:/Anaconda3/软网爬虫/任务一/{renamed_titles[code]}/标题，时间，文本.txt'
    code += 1
    f = open(txt_path, 'a', encoding='utf-8')

    resp = requests.get(r)
    resp.encoding = "UTF-8"
    child_page_content = resp.text
    obj3 = re.compile(r'<title>(?P<titles>.*?)-', re.S)
    result3 = obj3.finditer(child_page_content)

    for title in result3:
        title = title.group('titles')
        # print(title)
        f.write(title+'   ')
    obj4 = re.compile(r'<p class="content-tip"> (?P<times>.*?) 作者', re.S)
    result4 = obj4.finditer(child_page_content)
    for time in result4:
        time = time.group('times')
        # print(time)
        f.write(time+'\n')
    session = requests.Session()
    resp = session.get(url=r, headers=headers).text.encode('latin1')
    tree = etree.HTML(resp)
    links = tree.xpath(
        '/html/body/div[@class="news-list-content"]/div[2]/div[2]/div[1]/div/p|//*[@id="vsb_content"]/div/table|/html/body/div[2]/div[2]/div[2]/div[1]/div/form'
         )
    if not links:
        f.write('无正文')
        break
    for li in links:
        page_list_li = li.xpath('.//text()')
        f.writelines(page_list_li)

f.close()
print('TXT OVER!')
```

## 第五部分：爬取图片、附件

这两项内容较为类似，都是以二进制形式写入文件。

图片：这里使用re解析拿到图片的网址，并以二进制形式保存为jpg文件。

附件：使用re解析拿到附件的下载地址，通过两次选择语句去除无用的网址。处理完后将附件放入文件夹中。

```python
for r in url_list:

    resp = requests.get(r)
    resp.encoding = "UTF-8"
    child_page_content = BeautifulSoup(resp.text, "html.parser")
    img_list = child_page_content.find("div", class_="v_news_content").find_all("img")
    # print(img_list)

    # 处理重复文件名
    img_list = rename_duplicate(str(img_list), False)

    for li in img_list:
        obj5 = re.compile(r'<img src="(?P<src>.*?)"/>',re.S)
        result5 = obj5.search(li)
        if not result5:
            break
        src = result5.group('src')

        img_url = "https://sise.uestc.edu.cn" + src
        img = requests.get(img_url)
        # print(img)
        img_name = src.split("/")[-1]
        img_name = img_name.split('?')[0]
        # print(img_name)

        img_path = f'D:/Anaconda3/软网爬虫/任务一/{renamed_titles[code]}/{renamed_titles[code]}' + img_name
        code += 1
        with open(img_path, mode="wb") as img_f:
            img_f.write(img.content)

print('IMG OVER!')
# 爬取附件放入相应文件夹
code = 0

for r in url_list:
    resp = requests.get(r)
    resp.encoding = "UTF-8"
    child_page_content = BeautifulSoup(resp.text, "html.parser")
    href_list = child_page_content.find("div", class_="v_news_content").find_all("a")

    for lii in href_list:
        href = lii.get('href')
        # print(href)

        # 判断是否为空
        if not href:
            break
        
        # 区别不同网址
        # try:
        text1 = href.split(".")[0]
        # except AttributeError:
            # print(href)
            # break
        if text1 == 'https://www':
            href_url = href
        else:
            href_url = "https://sise.uestc.edu.cn" + href

        # 去除杂质
        text2 = href + '@'
        text2 = text2.split("@")[1]
        if text2 == 'uestc.edu.cn':
            break
        text3 = href.split(".")[0]
        if text3 == 'http://uestc' or text3 == 'http://sose':
            break

        href_name = href.split("/")[-1]
        href_name = href_name.split('?')[0]
        # print(href_name)
        fail_name = "ERROR " + href_name
        href_path = f'D:/Anaconda3/软网爬虫/任务一/{renamed_titles[code]}/' + href_name
        fail_path = f'D:/Anaconda3/软网爬虫/任务一/{renamed_titles[code]}/' + fail_name + '.txt'
        code += 1

        try:
            href_content = requests.get(href_url).content
        except requests.exceptions.ConnectionError:
            with open(fail_path, mode="w") as h_f:
                h_f.write('附件失效')
        else:
            with open(href_path, mode="wb") as h_f:
                h_f.write(href_content)
```

## 第六部分：最终效果图

### 爬取的所有新闻标题列表

​                         [![5uxVxK.md.png](https://z3.ax1x.com/2021/10/13/5uxVxK.md.png)](https://imgtu.com/i/5uxVxK)

### 每则新闻的标题、时间及文本

[![5uxE26.png](https://z3.ax1x.com/2021/10/13/5uxE26.png)](https://imgtu.com/i/5uxE26)

# 三、问题解决

## 1.创建文件夹时出现问题

在为不同的新闻创建文件夹时，第一次进行测试时程序可以正常运行，但当第二次运行时，因为原有的文件夹已经存在，导致程序报错无法正常运行。通过查资料后，我了解到os库中有isExists函数，可以判断文件夹是否存在，因此可以先进行判断，而后创建文件夹。

## 2.存储图片、附件时出错

在将图片，附件保存到本地时，没有使用二进制写入，导致得到的文件无法打开。经查询资料后，了解到Python中wb表示以二进制写入文件，优化代码后得到了正常的jpg文件。

## 3、附件失效问题

爬取过程中发现部分附件失效，无法进行下载，导致程序运行报错。解决办法：进行异常处理，对于无法正常下载的文件，在其文件名前加上ERROR，将附件格式改为txt形式，并写入‘附件失效’。

# 四、总结反思

总体来说这道题比较简单，算是爬虫入门级的题目，但是对于我这种刚刚学习爬虫的同学来说，在学习过程中还是遇到了很多困难，通过网课的学习以及网上查询各种资料，我克服了写代码中的许多困难，给予了自己解决问题的信心。

另外，通过这个爬虫程序的编写，加深了我对Python语言的理解，了解到了这门语言的强大，激发了我深入学习的兴趣。

当然本次解题中仍然存在很多问题：

（1）编写代码过程中不够细心，存在许多粗心的问题例如字母的大小写，中英符号，导致进程变慢影响进度。

（2）很多模块（Os、requests）只了解了个别需要的函数，还没有完全掌握其它函数的使用。

（3）对web相关知识了解程度不够深，只涉及对Url格式的了解，如果需要进一步对浏览器分析还需要了解更多相关知识。

（4）部分算法只求达到了需求，没有进行进一步的改进优化，程序仍有很大的进步改良空间。