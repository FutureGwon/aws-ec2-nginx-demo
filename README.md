# aws-ec2-nginx-demo
EC2에 Nginx 설치 프로젝트
**목표** : AWS EC2(Ubuntu)에 Nginx를 설치하고, 기본페이지를 교체하여 'Hello Cloud!'를 띄우는 미니 프로젝트 
**핵심 포인트** : EC2 생성 → 보안그룹 설정 → SSH 접속 → Nginx 설치/실행 → index.html교체 → 브라우저로 확인 → 결과와 과정을 문서화 
##⚙️사용기술 
- AWS EC2 (Ubuntu 24.04 LTS)
- Nginx
- SSH
- Mermaid 다이어그램
---
📖 프로젝트 개요
AWS EC2 인스턴스(Ubuntu 20.04)에 Nginx를 설치하고, 기본 웹페이지를 수정하여  
**Hello Cloud!** 메시지를 띄우는 실습 프로젝트입니다.  
이를 통해 클라우드 환경에서 서버 생성, 웹 서버 세팅, 보안 그룹 설정 과정을 경험했습니다.

✈️ 프로젝트 순서
1) **EC 서버 생성 & 보안그룹**
   - AMI : Ubuntu 24.04 LTS
   - 인스턴스 타입 : t3.micro (Free Tier) 
   - **보안그룹 인바운드**
     - SSH : TCP **22** (내 IP만 허용)
     - HTTP : TCP **80** (0.0.0.0/0)
     - HTTPS : TCP **443** (0.0.0.0/0)
     - (선택) MYQLS : **3306** (0.0.0.0/0)
   - **보안그룹 아웃바운드**
     - 기본값으로 설정

2) **SSH 키 페어**
     - 키 페어 생성 후 .pem파일이 있는 폴더로 이동 후, chmod 400 myServerKey.pem 명령어로 400으로 변경
     - 터미널에서 ssh -i "myServerKey.pem" ubuntu@<EC2_PUBLIC_IP>

3) **Nginx 설치 & 테스트 페이지 배포**
   - EC2 서버에 접속한 터미널에서 git clone 
   - **'''bash (명령어 직접 진행)**
   1. 패키지 업데이트 : 서버 패키지 목록을 최신으로 갱신합니다. 
      sudo apt update
   2. Nginx 설치
      sudo apt install -y nginx
   3. 서비스 시작
      sudo systmctl start nginx
   4. 부팅 시 자동 실행 설정
      sudo systmctl enable nginx
   5. 실행 상태 확인
      systmctl status nginx
   👉 "active (running)" 이면 정상 실행 중

       **브라우저 확인**
     http://<EC2_PUBLIC_IP>
     - "Welcome to Nginx" 가 보이면 성공
! [Welcome to Ngnix 결과] ([images/Welcome to nginx.png](https://github.com/FutureGwon/aws-ec2-nginx-demo/blob/main/Welcome%20to%20nginx.png))
    
      **기본 페이지 교체 (느낌표로 오류 나면 작은 따옴표 사용)**
   '''echo '<h1>Hello Cloud!</h1>' | sudo tee /var/www/html/index.html'''

4) **기본 교체 후 브라우저 확인**
 http://<EC2_PUBLIC_IP>
 - 'Hello Cloud!' 보이면 성공 🎊
! [Hello Cloud 결과] ([images/Hello cloud!.png](https://github.com/FutureGwon/aws-ec2-nginx-demo/blob/main/Hello%20cloud!.png))
  
