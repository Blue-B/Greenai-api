# GreenAI FastAPI Application

FastAPI 기반 간단 API 서버 + 정적 웹페이지

## 로컬 실행 방법

### 1. 가상환경 설정
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate
```

### 2. 의존성 설치
```bash
pip install -r requirements.txt
```

### 3. 애플리케이션 실행
```bash
python app.py
```

또는

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

브라우저에서 http://localhost:8000 접속

## Docker 실행 방법

### 1. Docker 이미지 빌드
```bash
docker build -t greenai-app .
```

### 2. Docker 컨테이너 실행
```bash
docker run -p 80:8000 greenai-app
```

브라우저에서 http://localhost 접속

## API 엔드포인트

- `GET /` - "Hello GreenAI" 메시지 반환 (HTML)
- `GET /static/` - 정적 파일 서빙
- `GET /static/index.html` - 정적 웹페이지

## AWS Lightsail 배포 방법

### 1. Lightsail 인스턴스 생성
- AWS 콘솔 → Lightsail → "Create instance"
- Platform: Linux/Unix → Ubuntu 20.04 LTS
- Instance plan: 최소 플랜 선택
- Instance name: greenai-server

### 2. Static IP 및 방화벽 설정
- Networking 탭 → "Attach static IP" 
- Firewall: HTTP (Port 80) 추가

### 3. 서버에 배포

#### Python으로 직접 실행
```bash
# SSH 접속 후 기본 패키지 설치
sudo apt update
sudo apt install python3 python3-pip git -y

# 프로젝트 클론
git clone https://github.com/Blue-B/Greenai-api.git
cd Greenai-api

# 의존성 설치 및 실행
pip3 install -r requirements.txt
python3 app.py
```

#### Docker로 실행 (권장)
```bash
# SSH 접속 후 Docker 설치
sudo apt update
sudo apt install docker.io git -y
sudo systemctl start docker
sudo usermod -aG docker ubuntu
newgrp docker

# 프로젝트 클론 및 Docker 실행
git clone https://github.com/Blue-B/Greenai-api.git
cd Greenai-api
docker build -t greenai-app .
docker run -d -p 80:8000 --name greenai greenai-app
```

### 4. 도메인 연결
DuckDNS를 사용하여 Static IP로 연결

## 파일 구조

```
.
├── app.py              # FastAPI 애플리케이션
├── requirements.txt    # Python 의존성
├── Dockerfile         # Docker 설정
├── static/
│   └── index.html     # 정적 웹페이지
└── README.md          # 이 파일
```

## 배포 구조

- **포트**: 8000 (컨테이너 내부), 80 (외부 노출)
- **정적 파일**: `/static` 경로로 제공
- **응답 형태**: HTML
