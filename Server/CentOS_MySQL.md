## 설치
CentOS 7 부터는 데이터베이스가 MariaDB로 변경되어 직접 설치를 해야 합니다.

```
yum -y install http://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
```
```
yum -y install mysql-community-server
```
```
systemctl start mysqld
systemctl enable mysqld
```
```
mysql -uroot -p
```

---

mysql 설치후 root 비밀번호는 임시로 자동 생성됩니다.<br>
자동 생성된 비밀번호는 /var/log/mysqld.log 에서 확인 가능합니다.
```
A temporary password is generated for root@localhost: password
```

---

비밀번호 변경
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH MYSQL_NATIVE_PASSWORD BY '변경할 비밀번호';
FLUSH PRIVILEGES;   //변경사항을 저장하기 위함
```

비밀번호를 간단한 형식으로 변경하고 싶으면 보안 정책을 LOW로 변경해야 합니다. (기본값: 중간)
```
SET GLOBAL validate_password.policy=LOW;
```

## MySQL WorkBench 연동

* SSH Hostname  : (연동할 서버 ip 주소) SSH니까 ```SERVER_IP:22``` 로 작성
* SSH Username  : (서버 user name) 우리는 root
* SSH Password  : (서버 password)
* SSH Key File  : (키 파일) 안넣어도 됨.
* MySQL Hostname : 127.0.0.1  
* MySQL Server Port  : 3306
* Username : (설정한 usename) 대부분 root
* Password  : (MySQL 비밀번호)
* Default Schema : 없으니까 X

***
## 외부 접속 허용
* 외부에서 접속해야 할 경우(보안상 새로운 유저를 만드는 것이 좋습니다.)
```
CREATE USER 'User_Name'@'Host_Name' IDENTIFIED BY 'password'
* 모든 호스트에 접근하게 하려면 Host_Name 을 % 로 지정
``` 
```
GRANT ALL PRIVILEGES ON DATABASE_NAME.* TO 'User_Name'@'Host_Name';
* Database_Name 에 * 을 넣으면 모든 데이터베이스에 모든 권한 획득
```
```
* 적용 확인
SELECT User, Host
FROM mysql.user;
```
