# 리눅스
## 1. 설치
### 1.1. 버추얼박스 설치
- 버추얼박스 설치전에 C++ 2019를 설치해야 한다.
- [C++ 2019 다운](https://aka.ms/vs/17/release/vc_redist.x86.exe)
- [버추얼 박스 다운](https://download.virtualbox.org/virtualbox/7.0.4/VirtualBox-7.0.4-154605-Win.exe)
- 버추얼박스 탈출 키 셋팅<br/>
    ![image](./image/linux/1.png)<br/>


### 1.2. CentOs7 설치하기
- [CentOS7 다운](http://mirror.navercorp.com/centos/7.9.2009/isos/x86_64/CentOS-7-x86_64-Minimal-2009.iso)<br/>
- 가상머신 만들기<br/>
    ![image](./image/linux/2.png)<br/>
    ![image](./image/linux/3.png)<br/>
    메모리 2GB에 CPU 1코어인 가상머신으로 설정<br/>
    ![image](./image/linux/4.png)<br/>
    용량은 20GB로 설정 후 가상머신 생성<br/>
    ![image](./image/linux/5.png)<br/>
    다음과 같이 `도구` 밑에 가상머신이 생성됐다.<br/>
- 생성된 가상머신 실행해서 초기 설정을 해준다.<br/>
    ![image](./image/linux/11.png)<br/>
    ![image](./image/linux/10.png)<br/>
    ![image](./image/linux/12.png)<br/>
    ![image](./image/linux/13.png)<br/>
    ![image](./image/linux/14.png)<br/>
    ![image](./image/linux/7.png)<br/>
    ![image](./image/linux/8.png)<br/>
    비밀번호와 유저를 생성해주고 기다리다보면 Reboot 버튼이 나오고 누르면 기본 셋팅이 끝난다.<br/>
- 접속 확인<br/>
    ![image](./image/linux/9.png)<br/>
    만들어 놨던 user 아이디와 비밀번호를 입력해 CentOS에 접속한다.<br/>




## 2. 리눅스명령어
### 2.1. 기본 명령어
|명령어|내용|
|---|---|
|ls|현재 위치 파일 목록 조회|
|cd|디렉토리 이동|
|pwd|현재 사용자가 있는 경로 출력|
|touch|0바이트의 파일 생성|
|mkdir|디렉터리 생성|
|cp|파일 복사|
|mv|파일 이동|
|rm|파일 삭제|
|cat|파일 내용을 화면에 출력, 리다이렉션 기호('>')를 사용하여 새로운 파일 생성|
|alias|자주 사용하는 명령러들을 별명으로 쉽게 사용할 수 있도록 설정|
|find|특정 파일이나 디렉토리를 검색|
|ps|실행중인 프로세스를 출력|

### 2.2. 명령어 상세 설명
- ls(List segments) : 현재 위치의 파일 목록 조회<br/>
    |명령어|내용|
    |---|---|
    |ls -l|파일의 상세 정보|
    |ls -a|숨김 파일 표시|
    |ls -t|파일들을 생성시간순(최신)으로 표시|
    |ls -rt|파일들을 생성시간순(오래된)으로 표시|
    |ls -f| 파일 표시 시 마지막 유형에 나타내는 파일명을 끝에 표시('/' : 디렉터리, '*' : 실행파일, '@' : 링크 등등...)|

- cd(Change directory) : 디렉터리 이동<br/>
    |명령어|내용|
    |---|---|
    |cd 디렉터리 경로|이동하려는 디랙터리로 이동|
    |cd ~|홈디렉터리로 이동|
    |cd /|최상위 디렉터리로 이동|
    |cd .|현재 디렉토리|
    |cd ..|상위 디렉터리로 이동|
    |cd -|이전 경로로 이동|
- mkdir(Make directory) : 디렉터리 생성<br/>
    |명령어|내용|
    |---|---|
    |mkdir name|name이라는 디렉터리 생성|
    |mkdir dir1 dir2|한 번에 여러개(dir1, dir2)의 디렉터리 생성|
    |mkdir -p name/sub_name|name이라는 디렉터리를 생성하고 그 디렉터리 내부에 sub_name이라는 디렉토리 생성|
    |mkdir -m 700 name|특정 권한을 가지는 디렉터리 생성|
    - 권한 예시<br/>
        |8진수|2진수|권한|의미|
        |---|---|---|---|
        |0|000|-|아무 권한 없음|
        |1|001|-x|실행권한만 있음|
        |2|010|-w-|쓰기권한만 있음|
        |3|011|-wx|쓰기, 실행 권한 있음|
        |4|100|r-|읽기 권한만 있음|
        |5|101|r-x|쓰기, 실행 권한 있음|
        |6|110|rw-|읽기, 쓰기 권한 있음|
        |7|111|rwx|모든 권한 있음|

        권한은 파일소유자, 소유 그룹, 일반 사용자로 나누어져 777권한을 주고 싶으면 rwxrwxrwx와 같이 세 부분으로 표현이 된다. 해당 자리에 권한을 따로 줘야 한다.<br/>

- cp(Copy) : 파일 복사<br/>
    |명령어|내용|
    |---|---|
    |cp file1 file2|file1을 file2라는 이름으로 복사|
    |cp -f file1 file2|강제 복사(file2라는 파일이 이미 있을 경우 강제로 기존 file2를 지우고 복사 진행)|
    |cp -r dir1 dir2 |디렉터리 복사. 폴더 안의 모든 하위 경로와 파일들을 복사|

- mv(Move) : 파일 이동<br/>
    |명령어|내용|
    |---|---|
    |mv file1 file2|file1 파일을 file2 파일로 변경|
    |mv file1 /dir|파일을 dir 디렉터리로 이동|
    |mv file1 file2/dir|여러개의 파일을 dir 디렉터리로 이동|
    |mv /dir1/dir2|dir1 디렉터리를 dir2 디렉터리로 이름 변경|

- rm(Remove) : 파일 삭제<br/>
    |명령어|내용|
    |---|---|
    |rm file1|file1을 삭제|
    |rm -f file1|file1을 강제로 삭제|
    |rm -r dir|디렉터리 삭제(디렉터리는 -r 없이 삭제 불가)|   

- cat(Catenate) : 파일 내용을 화면에 출력<br/>
    |명령어|내용|
    |---|---|
    |cat file1 firle2 > file3|file1, file2의 명령 결과를 합쳐서 file3라는 파일에 저장|
    |cat file4|file3에 file4의 내용 추가|

- ps(Process status) : 실행중인 프로세스 목록과 상태를 출력<br/>
    |명령어|내용|
    |---|---|
    |ps -e|현재 사용자뿐만 아니라 다른 사용자의 프로세스까지 출력|
    |ps -f|더 상세한 정보 출력|
    |ps -l|-f 보다 더 상세한 정보 출력|    
