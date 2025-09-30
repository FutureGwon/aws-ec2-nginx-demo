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
✈️ 프로젝트 순서
1) EC 서버 생성 & 보안그룹
   - AMI : Ubuntu 24.04 LTS
   - 인스턴스 타입 : t3.micro (Free Tier) 
   - **보안그룹 인바운드**
     - SSH : TCP **22** (내 IP만 허용)
     - HTTP : TCP **80** (0.0.0.0/0)
     - HTTPS : TCP **443** (0.0.0.0/0)
     - (선택) MYQLS : **3306** (0.0.0.0/0)
   - **보안그룹 아웃바운드**
     - 기본값으로 설정

2) SSH 키 페어
     - 키 페어 생성 후 .pem파일이 있는 폴더로 이동 후, chmod 400 myServerKey.pem 명령어로 400으로 변경
     - 터미널에서 ssh -i "myServerKey.pem" ubuntu@<EC2_PUBLIC_IP>

3) Nginx 설치 & 테스트 페이지 배포
     - EC2 서버에 접속한 터미널에서 git clone
     - '''bash
       sudo apt update
       sudo apt install -y nginx
       sudo systmctl enable --now nginx
      **브라우저 확인**
     http://<EC2_PUBLIC_IP>
     - "Welcome to Nginx" 가 보이면 성공
      **기본 페이지 교체 (느낌표로 오류 나면 작은 따옴표 사용)**
   echo '<h1>Hello Cloud!</h1>' | sudo tee /var/www/html/index.html

4) 기본 교체 후 브라우저 확인
 http://<EC2_PUBLIC_IP>
 - 'Hello Cloud!' 보이면 성공 🎊

  
