# 基于python的工具包-Pywkpypeteer
基于python的工具包,网页自动化工具
## 获取代码
```shell
git clone https://gitee.com/lovelong1/pywktools
cd py-wk-tools-pypeteer
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
python3 setup.py sdist bdist_wheel
```
## 安装
```shell
pip install Pywkpypeteer-1.0.1-py3-none-any.whl
```
## 卸载安装
```shell
pip uninstall Pywkpypeteer-1.0.1-py3-none-any.whl
```

# 代码使用说明
## PypeteerUtils 
```python
from pywkpypeteer import PypeteerUtils
import asyncio

async def main():
    _config = PypeteerUtils.default_config()
    _config['ismobile'] = True
    browser = await PypeteerUtils.browder(_config)
    page = await PypeteerUtils.page(browser)
    await PypeteerUtils.open(page, 'http://www.qq.com')
    await PypeteerUtils.screenshotFile(page)
    await PypeteerUtils.close(browser)

if __name__ == '__main__':
    asyncio.get_event_loop().run_until_complete(main())

```