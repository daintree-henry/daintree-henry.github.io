---
layout: post
title:  "Linux maven 설치"
date:   2021-11-28 00:57:00 +0900
comments: true
nav_order: 2
---

### Linux maven 설치
```shell

# wget 패키지가 없으면 설치
yum install wget -y

# maven 패키지 다운로드
# 링크가 없는 경우 http://mirror.navercorp.com/apache/maven/maven-3에 접속하여 적절한 링크로 수정
wget https://mirror.navercorp.com/apache/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz

# /opt 폴더에 압축 해제 및 기존 파일 삭제
tar xf apache-maven-3.8.4-bin.tar.gz -C /opt
rm -f apache-maven-3.8.4-bin.tar.gz

# 명령어 수행을 위한 링크 생성
ln -s /opt/apache-maven-3.8.4 /opt/maven
ln -s /opt/apache-maven-3.8.4 /usr/local/maven

# 환경 변수 지정
vi ~/.bash_profile

###1. 아래 내용 추가
###export MAVEN_HOME=/opt/maven
###2. 기존 PATH의 내용 아래와 같이수정
###export PATH=$PATH:$HOME/bin:$MAVEN_HOME/bin

# ~/.bash_profile 예시 
cat ~/.bash_profile
########### 출력 시작 ###########
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

export MAVEN_HOME=/opt/maven
export PATH=$PATH:$HOME/bin:$MAVEN_HOME/bin
############ 출력 끝 ############

source ~/.bash_profile

# maven 버전 확인
mvn --version
```