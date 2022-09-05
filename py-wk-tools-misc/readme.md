# 基于python的工具包-Pywkmisc
基于python的工具包,包括日期，数据，文件处理，图片处理，字符串
## 获取代码
```shell
git clone https://gitee.com/lovelong1/pywktools
cd py-wk-tools-misc
# 创建虚拟环境
python -m venv .
# liunx mac
source venv/bin/activate
# windows
venv/Scripts/activate.bat
# 编译项目
python3 setup.py build
```

## 打包
```shell
pip3 install wheel

python3 setup.py sdist bdist_wheel
```
## 安装
```shell
pip install Pywkmisc-1.0.1-py3-none-any.whl
```
## 卸载安装
```shell
pip uninstall Pywkmisc-1.0.1-py3-none-any.whl
```

# 代码使用说明
## Config 系统配置
Config 是获取系统参数工具，通过扫描指定cfp `config folder path` 文件夹中的json文件来获取配置项
### 例子
```python
from pywkmisc import Config
# 初始化config参数
config = Config(cfp='../conf/')
# 获取basic.json参数，返回数值
print('base', config.get_basic('f_size'))
# 获取basic.json参数，返回数值
print('base', config.get('base', 'base_url'))
# 获取db.json中参数，返回数值
print('db', config.get('db', 'test'))
# 获取spider.json中参数，返回数组
print('spider', config.gets('spider', 'web_tag_list[*].web_tag'))
```
### 返回结果
```shell
base 0.75
base http://127.0.0.1
db {'host': '127.0.0.1', 'port': '3306', 'username': 'root', 'password': '', 'database': 'test'}
spider ['电商', '贴吧']
```
### JSONPath 表达式教程

JSONPath关键字 | 描述
---- | ----
$ | 表示根元素
@ | 当前元素
. or [] | 子元素
n/a | 父元素
.. | 递归下降，JSONPath是从E4X借鉴的。
* | 通配符，表示所有的元素
n/a | 属性访问字符
[] | 子元素操作符
[,] | 连接操作符在XPath 结果合并其它结点集合。JSONP允许name或者数组索引。
[start:end:step] | 数组分割操作从ES4借鉴。
?() | 应用过滤表示式
() | 脚本表达式，使用在脚本引擎下面。
 n/a	 | Xpath分组

### 例子

| JSONPath例子 | 结果 |
| ---- | ----|
| $.store.book[*].author | 书点所有书的作者|
| $..author | 所有的作者|
| $.store.* | store的所有元素。所有的bookst和bicycle|
| $.store..price | store里面所有东西的price|
| $..book[2] | 第三个书|
| $..book[(@.length-1)] |  最后一本书|
| $..book[0,1]  $..book[:2] | 前面的两本书。|
| $..book[?(@.isbn)] | 过滤出所有的包含isbn的书。|
| $..book[?(@.price<10)] | 过滤出价格低于10的书。|
| $..* | 所有元素。|

## DataUtils 日期时间工具类
### get_first_last_by_month
根据年份，月份获取当月第一天和当月最后一天
### get_first_last_by_day
根据年份和月份和日，获取指定日期的第一秒钟和最后一秒钟
### get_future_mouth_first
获取指定月份下个月第一天
### get_timestamp
获取当前时间戳
### now
获取格式化时间撮当前时间


python -m pip install --user --upgrade setuptools wheel
python -m pip install --user --upgrade twine

python setup.py sdist bdist_wheel

python setup.py check

twine upload dist/*

twine upload --repository-url https://upload.pypi.org/legacy/ dist/*


1.0.4 

增加了获取网页https证书过期不出错的问题。