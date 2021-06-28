# os 버전 확인
 > cat /etc/os-release

# 유저 권한 수정
 > sudo vim /etc/sudoers
	> %sudo all=nopasswd: /usr/bin/mkdir
	> mkdir 프로그램 비밀번호 없이 실행할 수 있게 권한 설정
  linux user root 권한 설정

visudo
vi  /etc/passwd

linux router ip 찾기
netstat -rn
route -n
ip -r

linux chown 파일/디렉터리 소유권

drwxr-xr-x  2  root  root  4096 Apr 22 16:59 conory

파일Type 퍼미션정보 링크수 소유자 소유그룹 용량 생성날짜 파일이름

확인
ls -al
소유권 변경
chown {소유권자}:{그룹식별자} {변경할 파일}
chown aaa:bbb test.sh

하위 디렉터리까지 모두 소유권 변경
chown -R {소유권자}:{그룹식별자} {디렉터리}
chown -R aaa:bbb /home/test

# 명령어 binary 위치
 > /usr/bin/
 > /usr/sbin/

# 네트워크 설정
 > /etc/sysconfig/network-scripts/
 > ls
 > vim ifcfg-*
 > systemctl start networkmanager
 > nmcli networking off
 > nmcli networking on

# broken pipe
 [참조](https://may0301.tistory.com/10)

# 메일 보내기
 [참조](https://www.lesstif.com/lpt/send-mail-from-linux-command-line-24445045.html)
 [참조](https://sehoi.github.io/2014-10-17/linux-sendmail/)

 ### 파일첨부
 > $ mail -s "메일 테스트" -a test.pdf user@example.com <<< '메일 본문입니다'

# 네트워크 패킷 확인
 ## tcpdump - 패킷 가로채기

#### 189에서 157로 오는 패킷 가로채기
> tcpdump -eni ens33 host 192.168.200.157 and host 192.168.40.189

# 사용중인 머신 열려있는 포트 확인하기
 > netstat -nlpt

# iptables 적용 상태 확인
 > iptables -nvl

# mv
 > 파일 / 디렉터리 이동
# cp
 > 파일 / 디렉터리 카피
# scp
 > 파일 / 디렉터리 ssh를 통해 다른 서버로 카피
 > scp [file] [username]@[ip_address]:[path_to_copy]
# wget / curl
 > url로 파일 다운로드

