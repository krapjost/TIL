wsl2 go build 환경 구성 스크립트

서버에서 확인해야 할 것들
  1. openssh.server가 설치되어 있는가
  2. 22번 포트 방화벽이 열려 있는가
  3. 클라이언트에서 만든 ssh public 키가 제대로 입력되었는가
  4. 설정 파일 변경 후 sshd를 restart 했는가
  5. 원격에서 접속하려는 유저가 admininistrators 권한을 가지고 있는가 (그럴 경우 administrator_authorized_keys 파일에 키를 넣어야 한다.)
  6. 접속해야할 클라이언트가 여러 대일 경우 해당 클라이언트의 펍키를administrator_authorized_keys 파일에 이어서 넣어준다.
https://gist.github.com/otkrsk/b0ffd4018e8a79b9010c461af298471e
  
클라이언트에서 확인해야 할 것들
  1. ssh-keygen으로 생성한 키 파일이 여러 개는 아닌가 ( 여러 개를 사용할 경우 .ssh/ 디렉터리에 따로 config 파일을 만들어 설정을 해줘야 한다.)
https://yookeun.github.io/tools/2016/06/26/git-multi-ssh/


https://medium.com/dev-genius/set-up-your-ssh-server-in-windows-10-native-way-1aab9021c3a6

https://cloudeveloper.net/windows-10-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%B0%A9%EC%8B%9D%EC%9C%BC%EB%A1%9C-ssh-%EC%84%9C%EB%B2%84-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0-64988d87349

https://www.hanselman.com/blog/how-to-ssh-into-a-windows-10-machine-from-linux-or-windows-or-anywhere

https://docs.microsoft.com/ko-kr/windows-server/administration/openssh/openssh_install_firstuse

Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent

# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False


Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup.
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
