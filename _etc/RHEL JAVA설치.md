---
layout: post
title:  "RHEL 자바 설치"
date:   2021-11-28 00:57:00 +0900
comments: true
---

### RHEL JAVA 1.8 설치 
```shell

# 기존 설치되어 있는 자바 확인
java -version

# 패키지 업데이트 및 설치 가능한 자바 확인
yum update -y
yum list java*

# jdk 1.8 설치
# yum install java-1.8.0-openjdk.x86_64  (JRE만 설치 시)
yum install java-1.8.0-openjdk-devel.x86_64 -y

# 설치된 패키지 확인
rpm -qa java*
###출력
###java-1.8.0-openjdk-headless-1.8.0.302.b08-0.el7_9.x86_64
###javapackages-tools-3.4.1-11.el7.noarch
###java-1.8.0-openjdk-1.8.0.302.b08-0.el7_9.x86_64

# (Optional)자바 버전 확인 명령어 수행
java -version
javac -version
###출력
###openjdk version "1.8.0_302"
###OpenJDK Runtime Environment (build 1.8.0_302-b08)
###OpenJDK 64-Bit Server VM (build 25.302-b08, mixed mode)
###javac 1.8.0_302

# java가 설치된 폴더 확인
JAVA_HOME=$(readlink -f /usr/bin/javac)
###출력
###/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.302.b08-0.el7_9.x86_64/bin/javac

# JAVA_HOME 환경변수 추가
cat <<EOF >> /etc/profile
export JAVA_HOME=${JAVA_HOME}
EOF

source /etc/profile
```