# MariaDB
상용으로 쓰는 MySQL과 다르게 MariaDB는 무료로 사용이 가능하다.<br/>
## 설치
```shell
vi /etc/yum.repos.d/MariaDB.repo    # MariaDB 10.5 버전을 설치할 예정이다.
```
`MariaDB.repo`
```shell
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.5/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
```shell
yum install -y MariaDB-server MariaDB-client    # 설치
rpm -qa | grep -i mariadb   # 설치 확인
```
![image](./image/mariadb/1.png)<br/>
## 실행
```shell
systemctl start mariadb # db서버 실행
/usr/bin/mysqladmin -u root password    # db 비밀번호 설정
mysql -u root -p    # db서버에 접속
```
```sql
select @@datadir;   --경로 확인
```
![image](./image/mariadb/2.png)<br/>

## MariaDB 저장 경로 바꾸기
```shell
systemctl stop mariadb  # 수정을 위해 잠깐 서버를 끈다.
cp -R /var/lib/mysql /root/mysql_bak    # 원래 데이터 백업
rsync -av /var/lib/mysql /data  # 원래데이터를 /data 디렉터리로 옮겨준다.
chown -R mysql:mysql /data  # 소유자 권한 수정
vi /etc/my.cnf.d/server.cnf # 설정 파일 변경하기
```
```shell
[mariadb-10.5]
datadir=/data
socket=/data/mysql/mysql.sock

[client]
socket=/data/mysql/mysql.sock
```
![image](./image/mariadb/7.png)<br/>

```
vi /usr/lib/systemd/system/mariadb.service  # 마리아db 디렉터리 제한 해제(원래는 지정된 디렉터리만 된다.)
```

![image](./image/mariadb/3.png)<br/>

### 확인
```shell
systemctl restart mariadb   # db서버 실행
mysql -u root -p    # db서버 접속
```
```sql
select @@datadir;
```
![image](./image/mariadb/6.png)<br/>
경로가 성공적으로 변경됐다.<br/>

### 데몬 설정
```shell
systemctl daemon-reload # 데몬을 리로드 해서 재부팅해도 자동으로 켜지게 만든다.
service mariadb start 
```

## 에러
### 실행내용확인
만약 실행이 되지 않았다면 다음 코드로 내역을 확인해본다.<br/>
```shell
cat /var/log/messages
```
### Can`t open and lock privilege tables: Table `mysql,user` doesn`t exist
![image](./image/mariadb/4.png)<br/>
다음과 같은 에러가 발생하면 다음 설정 파일에 다음 코드(`skip-grant-tables`)를 추가한다.<br/>
```shell
vi /etc/my.cnf.d/server.cnf
```
![image](./image/mariadb/5.png)<br/>



