# 基于python的工具包-Pywkdb
基于python的数据库处理工具包
## 获取代码
```shell
git clone https://gitee.com/lovelong1/pywktools

pip install pywkmisc -i https://pypi.org/simple

cd py-wk-tools-db
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
pip install Pywkdb-1.0.1-py3-none-any.whl
```
## 卸载安装
```shell
pip uninstall Pywkdb-1.0.1-py3-none-any.whl
```

# 代码使用说明
## DBHelper 数据库工具类
```python
from pywkdb import DBHelper
db_config = {
    'host': '127.0.0.1',
    'port': 3306,
    'username': 'root',
    'password': '',
    'database': 'test',
    'charset': 'utf8'
}
#显示需要执行的查询sql
DBHelper('select * from testtable where id = %s', (1,), db_config=db_config).mogrify()
#查询并返回结果
DBHelper('select * from testtable where id = %s', (1,), db_config=db_config).select()
```
## SqlBuilder 创建SQL工具
```python
from pywkdb import SqlBuilder
db_config = {
    'host': '127.0.0.1',
    'port': 3306,
    'username': 'root',
    'password': '',
    'database': 'test',
    'charset': 'utf8'
}
sql = SqlBuilder('testtable')
sql.select_field({'fid', 'fname', 'fstatus'})
sql.put_where('fname', 'zhangsan')
sql.add_where_equals('fstatus', 1)
sql.add_where_between('fcdate', '2020-01-02', '2020-01-31')
#查询SQL
sqlstr, sql_params = sql.build()
print(sqlstr, sql_params)
#初始化
sql.new_pool()
sql.add_where_equals('fid', 8888)
sql.put_data('fstatus', 1)
sql.put_data('fname','lisi')
print(sql.build(SqlBuilder.INSERT_SQL))
print(sql.build(SqlBuilder.UPDATE_SQL))
print(sql.build(SqlBuilder.DELETE_SQL))
```
## DBUtils 创建数据实体操作工具
```python
from pywkdb import DBUtils
from pywkmisc import DataUtils

class Test(DBUtils):
    def __init__(self):
        super(Test, self).__init__('tb_test',db_config={
            'host': '127.0.0.1',
            'port': 3306,
            'username': 'root',
            'password': '',
            'database': 'test',
            'charset': 'utf8'
        })

if __name__ == '__main__':
    test = Test()
    # 插入一条记录
    test.put_data('fname', 'test1')
    test.put_data('fstatus', 1)
    test.put_data('fcdate', DataUtils.now())
    print(test.build(Test.INSERT_SQL))

    test.new_pool()
    test.select_field({'fid', 'fname', 'fstatus'})
    test.put_where('fname', 'test1')
    test.add_where_equals('fstatus', 1)
    sdate,edate = DataUtils.get_first_last_by_month()
    test.add_where_between('fcdate', sdate, edate)
    print(test.build())
    test.new_pool()
    test.put_where('fid', 133)
    print(test.build(test.DELETE_SQL))
    test.new_pool()
    test.put_data('fname', 'test1')
    test.put_data('fstatus', 1)
    test.put_data('fcdate', DataUtils.now())
    test.put_where('fid', 133)
    print(test.build(test.UPDATE_SQL))
```

1.0.6
修复了数据删除自动关闭数据库连接
