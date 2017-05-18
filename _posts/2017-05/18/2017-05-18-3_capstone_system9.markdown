---

layout: post
title: "(캡스톤) 캡스톤[5.18]"
category: PYTHON

---

### 오늘 할일(5월 18일)
> 오늘의 목표다.

* EC2 서버를 테스트로 구축하면서 실제로 구축할 때 필요한 명령어들을 모아보자
* 먼저 EC2 instance를 만들었다고 치고! terminal에서 pem키를 가지고 접속하는 것부터 시작해보려 한다.

1. 우선 pem키의 이름은 hello-test로 했습니다. 해당 경로에(/path) pem키를 위치했고 권한을 400으로 바꿔줬습니다.
2. 그리고 ssh를 이용하여 EC2 서버에 접속해 보겠습니다.(ssh -i 컴키 ubuntu@주소, 우분투 16.04 서버여서)

```sh
$ sudo chmod 400 /path/hello-test.pem
$ ssh -i /path/hello-test.pem ubuntu@ec2-13-124-74-53.ap-northeast-2.compute.amazonaws.com
```

3. 일단 파이썬3, pip3을 깔고 필요한 모듈부터 깔아주겠습니다.

```sh
$ sudo apt-get update
$ sudo apt-get install python3
$ sudo apt-get install python3-pip
$ sudo pip3 install --upgrade pip

$ sudo pip3 install boto3
$ sudo apt-get install python3-mysql.connector
$ sudo pip3 install pymongo
$ sudo pip3 install beautifulsoup4
```

4. mysql도 깔아주고, mongoDB도 깔아주고(ubuntu 16.04)

```sh
$ sudo apt-get install mysql-server
$ sudo mysql_secure_installation

$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
$ echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get install -y mongodb-org
# 한 후에 vim으로 켜서
$ sudo vim /etc/systemd/system/mongodb.service
# 이 내용 그대로 복사해서 넣고 수정 끝
# [Unit]
# Description=High-performance, schema-free document-oriented database
# After=network.target
#
# [Service]
# User=mongodb
# ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf
#
# [Install]
# WantedBy=multi-user.target
# 그리고 run
$ sudo systemctl start mongodb
```

5. 그리고 코드와 import 해야하는 sql 파일도 받아와서 임포트 시키면 일단 끝!(https://github.com/hanjungv/recommend)

```sh
$ mysql -uroot -p1234 inhatime < /home/ubuntu/recommend/inhatime_2017-04-27.sql
```

<img src = '/post_img/201705/18/res.png'/>

6. 크롤링이 잘 되는지 테스트 해보면<br/>
<img src = '/post_img/201705/18/res2.png'/>

* 이제 실제 SQS가 잘 되는지 봐야한다. 하지만 일본에 다녀와서 시작하려 한다~

<br/><br/>
