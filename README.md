# Dev Workstation Mission

## 1. 프로젝트 개요이 프로젝트는 터미널, Docker, Git/GitHub를 사용하여 재현 가능한 개발 워크스테이션을 구축하는 과제입니다.

주요 목표:- 터미널 기본 조작 실습
- 파일/디렉토리 권한 실습- Docker 설치 및 점검
- 컨테이너 실행 및 관리- Dockerfile 기반 커스텀 이미지 제작
- 포트 매핑, 바인드 마운트, 볼륨 영속성 검증
- Git/GitHub/VSCode 연동

## 2. 실행 환경
- OS: macOS- Terminal: Terminal
- Editor: VSCode- Docker Environment: OrbStack
- Shell: zsh

## 3. 수행 항목 체크리스트
- [ ] 터미널 조작 로그 기록
- [ ] 권한 변경 실습
- [ ] Docker 버전 및 동작 확인
- [ ] hello-world 실행
- [ ] ubuntu 컨테이너 진입
- [ ] Dockerfile 작성
- [ ] 커스텀 이미지 빌드
- [ ] 포트 매핑 접속 확인
- [ ] 바인드 마운트 검증
- [ ] Docker 볼륨 영속성 검증
- [ ] Git 설정 및 GitHub 연동
- [ ] 트러블슈팅 2건 작성

## 4. 프로젝트 구조
dev-workstation/
├── app/
│   └── index.html
├── docs/
│   └── screenshots/
│       ├── terminal-basic.png
│       ├── permission-before-after.png
│       ├── docker-version.png
│       ├── docker-info.png
│       ├── docker-ops.png
│       ├── hello-world.png
│       ├── ubuntu-container.png
│       ├── docker-build.png
│       ├── docker-run.png
│       ├── port-mapping.png
│       ├── bind-run.png
│       ├── bind-before.png
│       ├── bind-after.png
│       ├── volume-create.png
│       ├── volume-before-delete.png
│       ├── volume-after-delete.png
│       ├── git-config.png
│       ├── github-repo.png
│       └── github-vscode-login.png
├── Dockerfile
└── README.md

## 5. 터미널 조작 로그
5-1. 실습 목적
터미널 기본 명령을 사용하여 현재 위치 확인, 파일/디렉토리 생성, 복사, 이동, 이름 변경, 삭제, 파일 내용 확인을 수행하였다. 

5-2. 실행 명령
pwd
ls
ls -la
mkdir practice
cd practice
touch empty.txt
echo "hello" > note.txt
cat note.txt
cp note.txt copy.txt
mv copy.txt renamed.txt
mkdir subdir
mv renamed.txt subdir/
ls -la
rm empty.txt
cd ..
rm -r practice

5-3. 확인 내용
- `pwd`로 현재 작업 디렉토리를 확인하였다.
- `ls -la`로 숨김 파일을 포함한 전체 목록을 확인하였다.
- `touch`로 빈 파일을 생성하였다.
- `cat`으로 파일 내용을 확인하였다.
- `cp`, `mv`, `rm` 명령으로 복사, 이동/이름 변경, 삭제를 수행하였다.

-5-4. 증거
터미널 실행 화면: docs/screenshots/terminal-basic.png
/Users/rlawlsdn01196597/dev-workstation/docs/screenshots/terminal-basic.jpeg

##  6. 권한 실습
6-1. 실습 목적
파일과 디렉토리의 권한을 확인하고 변경하면서 r, w, x 권한과 644, 755 표기의 의미를 확인하였다.

6-2. 실행 명령
touch permission_file.txt
mkdir permission_dir
ls -ㅣ
chmod 644 permission_file.txt
chmod 755 permission_dir
ls -l

6-3. 결과 해석
- `r`은 read, `w`는 write, `x`는 execute 권한을 의미한다.
- `644`는 소유자에게 읽기/쓰기 권한, 그룹과 기타 사용자에게 읽기 권한만 부여한다.
- `755`는 소유자에게 읽기/쓰기/실행 권한, 그룹과 기타 사용자에게 읽기/실행 권한을 부여한다.
- 디렉토리에서 `x` 권한은 해당 디렉토리에 접근하거나 내부로 이동할 수 있다는 의미를 가진다.

6-4. 중거
권한 변경 전/후 화면: docs/screenshots/permission-before-after.png

## 7. Docker 설치 및 기본 점검
7-1. 실습 목적
Docker CLI가 정상적으로 동작하는지 확인하고, Docker 엔진이 실행 중인지 점검하였다. iMac 환경에서는 OrbStack을 통해 Docker를 사용하였다.

7-2. 실행 명령
docker --version
docker info

7-3. 확인 내용
- `docker --version`으로 설치된 Docker 버전을 확인하였다.
- `docker info`로 Docker 엔진이 정상적으로 실행 중임을 확인하였다.
- OrbStack 실행 후 터미널에서 일반 `docker` 명령을 사용할 수 있음을 확인하였다.

7-4. 증거
- Docker 버전 확인 화면: `docs/screenshots/docker-version.png`
- Docker info 확인 화면: `docs/screenshots/docker-info.png`

## 8. Docker 운영 명령 기록
8-1. 실습 목적
Docker 이미지, 컨테이너 상태, 로그, 리소스 사용 현황을 확인하는 기본 운영 명령을 실습하였다.

8-2. 실행 명령
docker images
docker ps
docker ps -a
docker logs my-nginx-container
docker stats --no-stream

8-3. 확인 내용
- `docker images`로 현재 로컬에 존재하는 이미지 목록을 확인하였다.
- `docker ps`와 `docker ps -a`로 실행 중인 컨테이너와 전체 컨테이너 목록을 확인하였다.
- `docker logs`로 컨테이너 실행 로그를 확인하였다.
- `docker stats --no-stream`으로 컨테이너 리소스 사용량을 확인하였다.

8-4. 증거
운영 명령 실행 화면: docs/screenshots/docker-ops.png

## 9. 컨테이너 실행 실습
9-1. hello-world 실행
Docker 설치가 정상적으로 완료되었는지 확인하기 위해 hello-world 이미지를 실행하였다.

9-2. ubuntu 컨테이너 내부 진입
Ubuntu 컨테이너를 실행한 후 내부로 진입하여 간단한 명령을 수행하였다.

docker run-it--name my-ubuntu ubuntubash

컨테이너 내부에서 다음 명령을 실행하였다.

ls
echo "inside container"
exit

9-3. attach / exec 관찰
실행 중인 컨테이너에 대해 `exec`를 사용하면 별도의 셸을 열 수 있다는 점을 확인하였다.

docker start my-ubuntu
docker exec -it my-ubuntu bash

9-4. 확인 내용
- `hello-world` 실행을 통해 Docker가 정상 동작함을 확인하였다.
- Ubuntu 컨테이너 내부에서 기본 Linux 명령이 동작함을 확인하였다.
- `exec`는 실행 중인 컨테이너 내부에 새 프로세스로 접속하는 방식이라는 점을 확인하였다.

9-5. 증거
- hello-world 실행 화면: `docs/screenshots/hello-world.png`
- Ubuntu 컨테이너 실행 화면: `docs/screenshots/ubuntu-container.png`

### 10. 커스텀 이미지 제작
10-1. 선택한 베이스 이미지
기존 베이스 이미지로 `nginx:alpine`을 선택하였다. 정적 웹 페이지를 빠르게 서비스하기에 적합하고, 과제에서 요구하는 웹 서버 컨테이너 구현에 적절하다고 판단하였다.

10-2. 커스텀 포인트
- 기본 NGINX welcome 페이지 대신 내가 만든 `index.html`을 사용하였다.
- 정적 콘텐츠를 포함한 커스텀 이미지를 직접 빌드하는 것을 목표로 하였다.

10-3. Dockerfile

FROM nginx:alpine
COPY app/index.html /usr/share/nginx/html/index.html


10-4. app/index.html

<!DOCTYPE html>
<htmllang="ko">
<head>
<metacharset="UTF-8">
<title>Dev Workstation</title>
</head>
<body>
<h1>Docker Custom Web Server</h1>
<p>이 페이지는 iMac 환경에서 제작한 과제용 웹 서버 페이지입니다.</p>
</body>
</html>


10-5. 빌드 및 실행 명령

docker build-t my-nginx-app .
docker run -d --name my-nginx-container-p8080:80 my-nginx-app

10-6. 확인 내용
- `docker build`를 통해 커스텀 이미지 생성에 성공하였다.
- `docker run`을 통해 컨테이너 실행에 성공하였다.
- 이후 브라우저 접속을 통해 웹 서버가 정상 동작함을 확인하였다.

10-7. 증거
- Docker build 화면: `docs/screenshots/docker-build.png`
- 컨테이너 실행 화면: `docs/screenshots/docker-run.png`

### 11. 포트 매핑 접속 증거

11-1. 실행 명령

호스트의 8080 포트를 컨테이너의 80 포트와 연결하여 웹 서버에 접근할 수 있도록 설정하였다.

docker run -d --name my-nginx-container-p8080:80 my-nginx-app


11-2. 확인 방법

브라우저에서 아래 주소로 접속하였다.

http://localhost:8080


11-3. 확인 내용

포트 매핑은 호스트 시스템에서 컨테이너 내부 서비스에 접근하기 위해 필요하다. 이번 실습에서는 호스트의 8080 포트를 통해 컨테이너 내부의 NGINX 80 포트에 접속하였다.

11-4. 증거

- 브라우저 접속 캡처(주소창 포함): `docs/screenshots/port-mapping.png`

### 12. 바인드 마운트 실험

12-1. 실습 목적

호스트 디렉토리를 컨테이너 내부 경로와 연결하여, 호스트 파일 수정이 컨테이너 결과에 즉시 반영되는지 확인하였다.

12-2. 실행 명령

docker run -d --name my-nginx-bind \
-p8081:80 \ # 호스트의 8081 포트를 컨테이너의 80 포트에 연결
-v "$(pwd)/app:/usr/share/nginx/html" \ #app 디렉토리를 컨테이너 안의 /usr/share/nginx/html 와 연결
  nginx:alpine

12-3. 실습 절차

1. `http://localhost:8081`에 접속하여 초기 화면을 확인하였다.
2. 호스트의 `app/index.html` 내용을 수정하였다.
3. 브라우저를 새로고침하여 수정 내용이 반영되는지 확인하였다.

12-4. 확인 내용

바인드 마운트를 사용하면 호스트 디렉토리와 컨테이너 내부 디렉토리가 직접 연결되기 때문에, 컨테이너를 다시 빌드하지 않아도 파일 변경이 즉시 반영된다.

12-5. 증거

- 실행 명령 화면: `docs/screenshots/bind-run.png`
- 수정 전 화면: `docs/screenshots/bind-before.png`
- 수정 후 화면: `docs/screenshots/bind-after.png`

### 13. Docker 볼륨 영속성 검증
13-1. 실습 목적
Docker 볼륨을 사용하여 컨테이너 삭제 후에도 데이터가 유지되는지 확인하였다.

13-2. 실행 명령

docker volume create mydata
docker run-it--name volume-test-v mydata:/data ubuntubash

컨테이너 내부에서:
echo"persistent data" > /data/test.txt
cat /data/test.txt
exit

컨테이너 삭제 후 다시 확인:
dockerrm-f volume-test
docker run-it--name volume-test-2-v mydata:/data ubuntubash
cat /data/test.txt
exit

13-3. 확인 내용
- Docker 볼륨 `mydata`를 생성하였다.
- 첫 번째 컨테이너에서 `/data/test.txt` 파일을 생성하였다.
- 첫 번째 컨테이너를 삭제한 뒤, 같은 볼륨을 연결한 새 컨테이너에서 동일한 파일이 유지됨을 확인하였다.
- 이를 통해 볼륨이 컨테이너 생명주기와 분리된 영속 스토리지 역할을 한다는 점을 확인하였다.

13-4. 증거
- 볼륨 생성 화면: `docs/screenshots/volume-create.png`
- 삭제 전 데이터 확인: `docs/screenshots/volume-before-delete.png`
- 삭제 후 데이터 확인: `docs/screenshots/volume-after-delete.png`

### 14. Git/GitHub/VSCode 연동

14-1. Git 설정
Git 사용자 정보와 기본 브랜치를 설정하였다.

git config--global user.name"내 이름"
git config--global user.email"내 이메일"
git config--global init.defaultBranch main
git config--list

14-2. 저장소 연결 및 업로드

git add .
git commit-m"Initial mission setup"
git branch-M main
git remote add origin https://github.com/내아이디/dev-workstation.git
git push-u origin main

14-3. 확인 내용
- `git config --list`를 통해 Git 사용자 설정이 적용되었음을 확인하였다.
- 로컬 저장소를 GitHub 원격 저장소와 연결하고 push를 완료하였다.
- VSCode에서 GitHub 로그인 및 Source Control 연동 상태를 확인하였다.
- Git은 로컬 버전 관리 도구이고, GitHub는 원격 저장소 및 협업 플랫폼이라는 점을 확인하였다.

14-4. 증거
- git config 결과: `docs/screenshots/git-config.png`
- GitHub 저장소 화면: `docs/screenshots/github-repo.png`
- VSCode GitHub 연동 화면: `docs/screenshots/github-vscode-login.png`

