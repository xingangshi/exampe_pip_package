[![](https://img.shields.io/pypi/pyversions/dict.svg?longCache=True)](https://pypi.org/project/exampe-pip-package/)
[![](https://img.shields.io/pypi/v/dict.svg?maxAge=3600)](https://pypi.org/project/exampe-pip-package/)
[![Travis](https://api.travis-ci.org/XingangShi/exampe_pip_package.svg?branch=master)](https://travis-ci.org/XingangShi/exampe_pip_package)

#### Installation
```bash
$ [sudo] pip install exampe_pip_package
```

#### Features
* **example for add a new pip package.**
* add some doc about learn how to release a pip package.
* **compatible with 2.7 and 3.X.X** .

#### Classes
class|`__doc__`
-|-
`exampe_pip_package.pip_test` |

#### Examples
```python
>>> from exampe_pip_package import pip_test

>>> example = pip_test()

>>> example.get_info()
Hello, this is just a pip package example.
Package name is exampe_pip_package

```
---

#### PIP 包生成发布使用学习文档

##### 源代码项目结构

```python
│  LICENSE                               // 证书，可以任选一个的
│  README.md                             // 说明文档
│  setup.py                              // 安装包
│
├─exampe_pip_package                     // 源代码目录
│      __init__.py                       // 源代码文件
│
└─tests-exampe_pip_package-examples      // 测试源代码的目录
    └─pip_test.get_info                  // 按照类来进行测试子目录的命名
            pip_test.get_info            // 按照方法来命名测试类文件
```

##### 安装必要的软件
> 安装生成归档文件的软件
```python
python -m pip install --user --upgrade setuptools wheel
```

> 安装发布上传包
```python
python -m pip install --user --upgrade twine
```

##### 注册 PYPI 账号
> [测试账号注册地址，用于测试版本](https://test.pypi.org/manage/projects/)。
>
> [正式账号注册地址，用于正式版本发布](https://pypi.org/manage/projects/)。
>
> **Note： 测试账号和正式账号注册一次就可以的，但是要分别去认证可发布的邮箱。**


##### 打包和发布
> 生成发布包（生成归档文件）
```python
python setup.py sdist bdist_wheel
```

> 注册包
```Python
twine register dist/exampe_pip_package.whl
```

> 发布
>
>> 发布到测试环境
```python
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```
>>
>> 发布到正式环境
```python
twine upload --repository-url https://upload.pypi.org/legacy/ dist/*
```
>>
>> 发布说明
```python
E:\selfDatas\exampe_pip_package>twine upload --repository-url https://test.pypi.
org/legacy/ dist/*
Enter your username:  输入用户名，不是邮箱
Enter your password:  输入密码
Uploading distributions to https://test.pypi.org/legacy/
……

```

> 包管理
>> 包已经上传成功的话，可以登录 [PyPI 网站](https://pypi.org/) 可以在右侧导航栏看到管理入口。
>> 点击包名进去后你可以对你的包进行管理。

##### 发布成功后安装（pip install 方式）
> 测试包的安装
```python
pip install -i https://test.pypi.org/simple/ exampe-pip-package
```

> 正式版本的安装
```python
pip install exampe-pip-package
```

> 更新包，可以使用 `--upgrade` 参数来更新
```python
pip install exampe-pip-package --upgrade
```

###### 安装包后的使用
> import 方式使用
```python
>>> from exampe_pip_package import pip_test

>>> example = pip_test()

>>> example.get_info()
Hello, this is just a pip package example.
Package name is exampe_pip_package

```

##### 发布成功后安装（requirements 方式使用）
>> 目录结构
```python
E:.
    main.py             # 需要使用包的代码
    requirements.txt    # 需要使用到包的包名
    run.sh              # 安装包并执行文件
```
>> [详见 requirements 方式使用](/test-requirements_type-example)

##### 免授权方式发布
> 在 Home 目录下创建文件 `~/.pypirc`，内容如下
``` python
[distutils]
index-servers = pypi

[pypi]
repository: https://pypi.python.org/pypi
username: <username>
password: <pass>  # 不设置的话，发布时会提示手动输入的
```

##### 可能遇到的错误
> 错误的用户验证信息，你需要创建一个用户验证文件 ~/.pypirc。请参阅上文。
```python
Upload failed (403): Invalid or non-existent authentication information.
```

> 你需要先注册你的包才可以开始上传，运行注册命令：`python setup.py register`
```python
Upload failed (403): You are not allowed to edit 'xxx' package information
```

> 你的 PyPI 账户还没完成邮箱验证，你需要去注册邮箱找到一封验证邮件完成验证后再重试失败的步骤。
```python
Server response (401): Incomplete registration; check your email
```

> 你的 setup.py 文件中的 classifier 信息有误，请按官网的正确分类书写classifier.
```python
Server response (400): Invalid classifier "Topic :: Software Development :: Utilities"
```

> 你还没打包就开始了上传命令，建议打包和上传的操作放在一起做，比如：`twine upload dist/*`
```python
error: No dist file created in earlier command
```

> 网络问题，请再次尝试
```python
error: Upload failed (499): Client Disconnected
```

> 每次必须使用不同的版本号，所以建议先在测试版测试好了，再在正式版发布的。
```python
Upload failed (400): File already exists
```

##### 更多相关信息，见[官方文档](https://packaging.python.org/)。
<p align="left">
    <a href="https://github.com/xingangshi">More info</a>
</p>
