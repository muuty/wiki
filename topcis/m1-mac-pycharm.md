---
description: M1 mac
---

# M1 Mac Pycharm 설정 방법

##  M1 맥북 + Pycharm + python2.7

docker는 설치되어 있는 것으로 가정한다.


### 1. Docker image 생성


```
$ docker run -d -P --name python_pycharm rastasheep/ubuntu-sshd:16.04
$ docker port python_pycharm 22
0.0.0.0:55000

$ ssh root@localhost -p 55000
# The password is 'root'
root@python_pycharm $ 
```


### 2. python2.7 설치 및 venv 설치

```
# python2.7 설치
$ apt-get update
$ apt-get -y install python2.7
$ apt-get -y install gcc python-pip python-dev python-setuptools libpq-dev libgmp3-dev

# venv
$ apt-get python3-pip
$ pip3 install --upgrade pip3==20.2.1
$ pip3 install virtualenv pbr
$ virtualenv buzzad
$ source buzzad/bin/activate


```

### 3. Pycharm에 세팅하기

1. Preference - Project - Python Intepreter에서 Add 클릭, ssh interpreter를 클릭해서 인터프리터를 설정해준다. usr/bin/python을 그대로 사용하면 된다.

2. Preference - Tools - ssh configuration 에서 + 버튼을 눌러서 ssh 설정을 추가해준다. 


