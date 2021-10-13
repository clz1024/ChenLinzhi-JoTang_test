# Python数据分析+Browser初步探索

## 一、前期准备

### 1.题目分析

#### Python数据分析

数据分析是指用适当的统计方法对收集来的大量数据进行分析，将它们加以汇总和理解并消化，以求最大化地开发数据的功能，发挥数据的作用。数据分析是为了提取有用信息和形成结论而对数据加以详细研究和概括总结的过程。而对于这道题目则是以python语言为工具、基础分析得来的海量数据，并通过筛选、分类等操作得到目标数据，最后通过一定的可视化操作将结果清晰、鲜明的展示出来。那么，为什么使用python这门语言呢？我觉得有以下几个原因（1）语法简单，易于学习上手（2）在数据分析和交互、探索性计算以及数据可视化等方面都显得比较活跃，python拥有numpy、matplotlib、scikit-learn、pandas、ipython等工具在科学计算方面十分有优势，尤其是pandas，在处理中型数据方面可以说有着无与伦比的优势。（3）Python具有强大的编程能力、非常强大的数据分析能力，并且还可以利用Python进行爬虫，写游戏，以及自动化运维，能够大大的提高数据分析的效率。

#### Browser初步探索

对于当今电脑的使用者来说，Browser就像一个窗口，联系了电脑前的使用者与电脑窗口后的大千世界，及时的资讯、新闻；前沿的技术、发明；连载的动漫，剧集………各种各样规模、形式的内容都在Browser中为我们呈现。因此对于使用者、体验者的我们，优化Browser使用体验，完善Browser附加功能，了解Browser运行机制就有了其不可替代的重要性与必要性。在本课题中，我学会了多种浏览器插件的下载与使用，如：网页翻译，视频网站去广告，百度文库无粘贴限制，IDE多线程下载（刷网课插件bushi）…………它们都为我的Browser使用提供了莫大的便利，我也相信在以后的Browser使用中我仍会不断探索。

### 2.环境配置

#### python

（之前就已经完成了下载及环境配置，完成此题目时又重新检查了环境变量，更新了最新版的python3.9.7，值得注意的是此次用IDE插件多线程下载使下载速度大大提升）下载完成后，进行自定义安装，之后在环境变量的path选项中对python进行添加，至此完成对python的安装（之前有下过pycharm并完成配置，此题中用的另一编译器则未提及pycharm的安装与配置）

#### Anaconda

包括Conda、Python以及一大堆安装好的工具包（但先前不知道就也单独下载安装了python），这次编写代码主体用的是Anaconda中自带的jupyter notebook，选择使用它的原因有如下几点（1）它是一款开放源代码的 Web 应用程序，它提供了一个环境，可以在其中记录代码，运行代码，查看结果，可视化数据并在查看输出结果。这些特性使其成为一款执行端到端数据科学工作流程的便捷工具 ，可以用于数据清理，统计建模，构建和训练机器学习模型，可视化数据以及许多其他用途。（2）当在构建项目原型时，Jupyter Notebooks  真的特别好用，因为代码是被写入独立的单元中并被单独执行的。这允许用户测试项目中的特定代码块，而无需从脚本的开始执行代码。许多其他的 IDE  环境（Integrated Development Environment， 集成开发环境）虽也能做到这一点，但我认为 Jupyter 的单个单元结构是最好的。（3）Jupyter Notebooks 是非常灵活、可交互和强大的工具。它甚至允许运行除了Python 以外的其他语言，比如 R 、SQL 等。

#### Navicat

由于找到的缓存chrome浏览器历史访问记录的文件是一个数据库文件，为了更清晰地理解这个文件、本道题目，于是我下载了Navicat（破解版）这个数据库管理文件，方便后期数据库内容的学习。

### 3.技术学习

#### python基本语法

由于有C语言的基础，python语言的入门相对容易，通过菜鸟教程及B站的一些教学视频，很快入门并掌握基本语法。重点关注了Python语言中基本的循环语句、列表、字典、元组其中对字典的一些相关操作反复学习、重点要求，为后面数据分析提供坚实的理论知识。

#### 数据库基本知识与操作

主要是通过B站教程观看sqlite数据库入门，掌握了数据库基本的连接，增删查改等操作。

#### python相关工具包的使用

主要通过B站python数据分析教程进行了学习，大致了解了python数据分析中常用的Numpy、Pandas以及Matploblib、pyecharts几个库。同时重点了解os、sqlite3、operator、collections、matploblib几个模块，方便后期完成代码编写时的调用。

#### 简要了解web相关知识（重点在url）

在WWW（World Wide Web，万维网）上，每一信息资源都有统一的且在网上唯一的地址，该地址就叫URL（Uniform Resource Locator,统一资源定位器），它是WWW的统一资源定位标志，就是指网络地址。一个完整的url（https://www.bilibili.com/video/BV1Cx411m7n7?from=search&seid=8941458026121594216）一般包涵以下几个部分：协议（https://），网址（www.bilibili.com），文件地址（/video/BV1Cx411m7n7?from=search&seid=8941458026121594216）。而网址去掉www.剩下如bilibili.com,则这个部分叫做域名，值得注意的是此题中字典的键便是各个网址的域名。其中.com则称为定级域名，其中.com表示商业组织.org表示非营利性组织.gov表示政府机构.edu表示教育及科研机构，另外.cn表中国.us表美国.jp表日本.cc则代表了澳大利亚。有时候公司的子公司会采取二级域名的形式例如腾讯网（qq.com）而子产品QQ邮箱（mail.qq.com）从域名后的第一个'/'开始到最后一个'/'是虚拟目录部分,从最后一个'/'到#为止是文件名部门，#之后就是锚部分。虚拟目录，稳健部门，锚都不是必须的。

### 二、解题过程

#### 文件寻找(任务一)

在通过收集资料并探索寻找后，我终于在'C:\Users\chen sir\AppData\Local\Google\Chrome\User Data\Default'路径找到了名为History的文件，并确定了这是记录谷歌chrome浏览器历史及记录的文件。进一步查阅资料，我知道了这是一个数据库文件。于是下载了数据库处理软件Navicat并学习了python关于数据库的sqlite3模块。

#### 代码编写

##### 第一部分：模块引入  

正式开始着手代码的编写，首先引入该题目所需要的python中的模块。它们分别是：

（1）与数据库操作相关的sqlite3模块 

（2）提供了多数操作系统的功能接口函数的os模块

（3）提供了一套与Python的内置运算符对应的高效率函数的operator模块

（4）collections模块在内置数据类型（dict、list、set、tuple）的基础上，collections模块还提供了几个额外的数据类型：Counter、deque、defaultdict、namedtuple和OrderedDict等。而OrderedDict这种数据类型（排序的字典）是本题我们需要的。

（5）引入matplotlib.pyplot模块，它是使matplotlib像MATLAB一样工作的命令样式函数的集合，其生成可视化效果的速度很快。         

##### 第二部分：通过os模块处理'History'数据库文件路径

（1）一个python文件通常有两种使用方法，第一是作为脚本直接执行，第二是 import 到其他的 python  脚本中被调用（模块重用）执行。因此此处的语句`if __name__ == '__main__': `的作用是控制这两种情况执行代码的过程，在` if __name__ == '__main__'`下的代码只有在第一种情况下（即文件作为脚本直接执行）才会被执行，而 import  到其他脚本中是不会被执行的。

**原理**：每个python模块都包含内置的变量 name，当该模块被直接执行的时候，name 等于文件名（包含后缀 .py ）；如果该模块 import 到其他模块中，则该模块的 name 等于模块名称（不包含后缀.py）。而 “main” 始终指当前执行模块的名称（包含后缀.py）。进而当模块被直接执行时，name == 'main' 结果为真。

（2）声明一个字符串'data_path'储存存有浏览记录的数据库文件'History'的路径，此处的语句`os.path.expanduser('~')`将'~'替换成当前用户的家目录（家目录是在多用户操作系统上包含该系统的特定用户的文件系统目录。此处为C:\Users\Administrator）并返回。加上后面的r"\AppData\Local\Google\Chrome\User Data\Default"，此处通过字符串前面加r实现禁止字符串转义（此处特指'\\'）的功能。通过此语句便将'History'路径完整存入data_path字符串。

（3）语句`os.listdir（data_path）`返回一个由文件名和目录名组成的列表，注意它的接收参数需要时一个绝对路径（绝对路径是指文件在硬盘上真正存在的路径）。

（4）使用`history_db = os.path.join(data_path, 'History')`语句连接两个或更多的路径名组件，从而得到数数据库文件'History'的绝对地址，保存在字符串histor_db中。

##### 第三部分：通过sqlite3模块对目标数据库进行处理

（1）通过`sqlite3.connect()`函数连接目标数据库，返回一个con。不存在，它会被自动创建。 该数据库文件是放在电脑硬盘里的，也可以自定义路径，后续操作产生的所有数据都会保存在该文件中。

（2）建立与数据库的连接后，就可以通过语句`cursor = c.cursor()·`创建一个游标`cursor`对象，该对象的`.execute()`方法可以执行sql命令，让我们能够进行数据操作。

（3）`select_statement = "SELECT urls.url, urls.visit_count FROM urls, visits WHERE urls.id = visits.url;"`\

上面select_statement指的是查询数据库的规则，完整规则如下：

步骤一，从(FROM)表urls（一个数据库文件中有多个表其中就有urls与visits表）中选择(SELECT)出以下字段~~urls.id,~~ urls.url, ~~urls.title~~,  ~~urls.last_visit_time~~,  urls.visit_count。

步骤二，从(FROM)表visits中选择(SELECT)出以下字段~~visits.visit_time,  visits.from_visit, visits.transition,  visits.visit_duration~~。

对步骤1和步骤2的结果进行连接，形成一个表格。然后从中(WHERE)筛选出符合`urls.id =  visits.url`的行。在urls中，id代表的是URL的id，在visits中，url代表的也是URL的id，所以只有当两者相等，才能连接一起，才能保留，否则就要去除这一行。

这里我们列出每个字段代表的意思：urls.id——url的编号，urls.url——url的地址，urls.title——url的标题，urls.last_visit_time——url的最后访问时间，urls.visit_count——url的访问次数，urls.visit_time——url的访问时间，urls.from_visit——从哪里访问到这个url，urls.transition——url的跳转，urls.visit_duration——url的停留时间。

（4）通过`cursor.execute(select_statement)`语句执行select操作，并使用`cursor.fetchall（）`得到的一个由元组（tuple,元组和列表十分类似，只不过元组和字符串一样是不可变的 即你不能修改元组，元组特点：定义元组使用小括号，且逗号隔开隔开各个数据，数据可以是不同的数据类型。）组成的列表results。

查询结果是多条数据，fetchall得到的是由多个元组组成的列表；这就决定了如果需要取元组中的数值，需要使用`cursor.fetchone[0][0]`,即第一个[0]表示列表中的第一个元祖（某一url的id及其访问次数），而第二个[0]则表示第一个元祖中的第一个数据（第一个元祖中第一个表示url的id的数据）

（5）声明一个名为sites_count的空字典，使迭代更加容易实现（如果要迭代key,可以用for key in sites_count如果要迭代value，可以用for value in sites_count.values()，如果要同时迭代key和value，可以用for k, v in sites_count.items()语句）。

##### 第四部分：通过字典、元祖组成列表迭代对收集记录进行处理并排序

（1）使用语句`    for url, count in results:`对fetchall返回元祖组成列表进行遍历。

（2）使用`parse（url）`函数对url进行处理，得到统一url域名形式，方便观察、理解。

（3）判断语句`        if url in sites_count: `	如果该键出现在字典中则相应值即浏览次数加一（`site_count[url] += 1`）；若该字典中还没有相应的键值对，则添加以（url）为键的字典，其初值赋为1。

（4）`sites_count_sorted = OrderedDict(sorted(sites_count.items(), key=operator.itemgetter(1)/key= lambda sites_count: sites_count[1], reverse=True))`

OrderedDict是collections中的一个包，能够记录字典元素插入的顺序，配合 sorted（排序函数）对得到记录访问url及其浏览次数组成的字典按次数进行排序得到有序字典。

此处sorted函数，进行排序的可迭代对象是`sites_count.items()`，即字典site_count的全部键值对。`reverse=True`则表示结果按降序排列，false为升序排列。而对于`key=operator.itemgetter(1)/key= lambda sites_count: sites_count[1]`中的key即是声明排序的依据，这两种方法都可以，第二种使用lambda函数作为参数传递给sorted函数作为标准排序，而第一种`operator.itemgetter(1)`表示一个函数，'1'表示取sites_count里的第二个数，用这个数来进行排序。

（5）由于本题目要求对最常访问的前20个网站进行排序，而我们现在则浏览、排序了所有的历史访问记录，因此，我们需要对结果进行筛选。而`sites_count_sorted`此时是一个有序字典，我们通过`len（sites_count_sorted）`便可以得到字典中键值对的个数，通过`while len(sites_count_sorted)>n:`语句中嵌套`sites_count_sorted.popitem()`不断pop出最后一对键值对，知道数目降到我们需要的20为止。

**第五部分：数据可视化**

首先根据'c'或者'p'指令决定进行网址的罗列还是进行绘图可视化

**（1）列出最常访问的20个网址**

在该脚本路径下打开或创建一个名为'history.txt'的记事本文件。

并在该文本文件中写入最常访问的20个网站的域名

**（2）对最常访问的20个网址做可视化操作**

使用python中matplotlib.pyplot模块中饼图绘制相关函数，以结果中key值为名，访问次数即value值为百分比，并绘制保留两位小数结果的饼图

#### 最终效果图

##### 可视化饼图：

[![5uRX5j.png](https://z3.ax1x.com/2021/10/13/5uRX5j.png)](https://imgtu.com/i/5uRX5j)

##### 文本记录：                  

​                                       [![5uROaQ.png](https://z3.ax1x.com/2021/10/13/5uROaQ.png)](https://imgtu.com/i/5uROaQ)



## 三、问题解决

#### 	Anaconda 安装出现问题

在安装Anaconda过程中我首先去官网进行了下载，配合IDE速度不是特别快，于是后来B站上找了下资源，去清华大学开源软件镜像站下载了最新的版本。安装我遇到了问题在Win10下安装Anaconda3只有Anaconda Prompt没有Anaconda navigator 和jupyter notbook，然后我官网下载，更新win10。之后更换了前一个版本后可正常使用。

#### 	sqlite学习过程中编译不通过

学习数据库相关知识时，有一天晚上在学习基本操作（数据库的连接、增删改），有一个sql语句是增加一条数据，那个句子始终编译不通过，大概debug了半个小时，最后实在顶不住了，就全删了重新打了一遍，竟然就过了，回想起来应该是中英文符号打错了。

#### 	'History'文件大小写问题

在获取数据库文件'History'绝对路径是发生了问题，将文件H写成了小写导致多次编译不通过，在最终通过定位路径发现了问题，修正之后编译通过。

#### 	数据库fetchmany（20）的理解问题

由于本题目的要求是列出最常访问的20个网站，然而最初的方法是获取了数据库文件中所有浏览历史记录，导致了显示了所有访问过得网站。而后我以为`fetchall()`改为`fetchmany（20）`就可以只收齐前20个网址的访问次数，结果可视化出来只有一个网站。经查阅资料明白，`fetchmany（20）`是收集了20条访问记录，而最常访问的网站次数远大于20于是最终只有一个结果。后来改变策略先收集全部数据后，按访问次数排序得到有序字典，而后用`popitem（）`不断删去末尾键值对，直至剩20个为止。

#### 标题中文显示的问题

对饼图完成绘制后，需要为饼图写上一个中文标题，但是直接使用`plt.title`函数后却编译不通过，查阅资料明白是因为matplotlib中缺乏中文字体，于是先下载了需要的中文字体SimHei.ttf ，并放在指定目录`D:\Anaconda\Lib\site-packages\matplotlib\mpl-data\fonts\ttf`下，并修改配置文件matplotlibrc第一步，使用文本编辑器打开matplotlibrc 文件，找到font.family，并将font.family和font.sans-serif两行前的#删除； 第二步，在font.sans-serif后添加中文字体SimHei，其他的不变；第三步可以修改axes.unicode_minus，将True改为False，作用就是解决负号’-'显示为方块的问题。编写代码时加入plt.rcParams['font.sans-serif']=['SimHei']，plt.rcParams['font.family']='sans-serif'  ，plt.rcParams['axes.unicode_minus'] = False之后即可打印中文标题。同时标题默认打印中央但距离未进行设置，查阅资料后通过纵坐标是定将标题上移，不遮盖饼图。

## 四、总结反思

总体来说此题较为简单，一是涉及的知识比较集中，而是网上有较多类似的题目，提供了很多思路。所以完成起来比较顺利，没有特别卡壳的地方。难点主要是python各个函数的使用方式，参数的格式，包括后期可视化中饼图的调整。通过此次项目学习了数据库相关知识，python中数据分析相关的几个库中重要函数的使用以及简单的web基础，同时也提升了对浏览器的理解，探索了许多实用的插件，为今后的学习、生活提供了很大的便利。

当然本次解题中仍然存在很多问题：

（1）编写代码过程中不够细心，存在许多粗心的问题例如字母的大小写，中英符号，导致进程变慢影响进度。

（2）很多模块（Os、Operator）只了解了个别需要的函数，还没有完全掌握其它函数的使用。

（3）对web相关知识了解程度不够深，只涉及对Url格式的了解，如果需要进一步对浏览器分析还需要了解更多相关知识。

（4）部分算法只求达到了需求，没有进行进一步的改进优化，程序仍有很大的进步改良空间。

但不管怎样，完成这个题目让我掌握了许多知识、加深了对浏览器使用的理解。希望以此为契机进一步学习python数据分析，同时通过对浏览器的探索与熟练掌握进一步便利学习与生活。















​		
