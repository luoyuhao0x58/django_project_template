# Django项目模版

配置这个模版主要是为了减少重复劳动

## 和官方模版差异

1. 直接包含Git工程基本文件
2. pipenv和setup.py结合
3. Django的setting.py作为开发环境和生产环境的公共部分，并已经配置好中国的语言和时区
4. 开发配置使用local\_settings.py，此文件直接在.gitignore排除
5. 生产环境的配置通过环境变量EXTRA\_CONFIG\_FILE变更
6. 版本号通过VERSION文件管理

## 用法

### 初始化

安装依赖

```shell
export PROJECT_NAME=demo  # 假设项目名为demo
mkdir $PROJECT_NAME && cd $PROJECT_NAME
pipenv install --python 3.6 --three Django  # 实际开发时候，此处应该指定Django版本
pipenv install -d ipython pylint autopep8 wheel
```

初始化项目

```shell
pipenv shell
django-admin startproject --template https://codeload.github.com/Haujilo/django_project_template/zip/master $PROJECT_NAME .
```

修改local\_settings.py，添加本地的开发库同步即可

```shell
pipenv shell
python manage.py migrate
```

### 日常开发

标准的Django开发流，在开发环境也能准确读取到版本号

```shell
pipenv shell
python manage.py runserver
```

### 打包

```shell
pipenv shell
./setup.py clean -a && ./setup.py bdist_wheel
```
