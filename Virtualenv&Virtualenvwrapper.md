## Virtualenv&Virtualenvwrapper

virtualenv是一个python虚拟环境，能够和系统环境相隔离，保持环境的纯净。

virtualenvwrapper可以方便的管理虚拟环境。

#### 安装

```shell
pip install virtualenv
easy_install virtualenvwrapper
```

#### 配置

```shell
# vim ~/.bash_profile
export WORKON_HOME=$HOME/virtualenvs
export VIRTUALENVWRAPPER_SCRIPT=/Library/Frameworks/Python.framework/Versions/3.6/bin/virtualenvwrapper.sh
export VIRTUALENVWRAPPER_PYTHON=/Library/Frameworks/Python.framework/Versions/3.6/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=/Library/Frameworks/Python.framework/Versions/3.6/bin/virtualenv
source /Library/Frameworks/Python.framework/Versions/3.6/bin/virtualenvwrapper.sh
```

#### 使用virtualenv

```
virtualenv virenv1
```

#### 使用virtualenvwrapper

```shell
mkvirtualenv env1  # 默认创建
mkvirtualenv --python=/usr/bin/python2.7 env  # 创建 --python可以指定python
lsvirtualenv -b # 列出虚拟环境
workon env1 # 切换虚拟环境
cpvirtualenv env1 env3  # 复制虚拟环境
deactivate # 退出虚拟环境
rmvirtualenv env1 # 删除虚拟环境
```

