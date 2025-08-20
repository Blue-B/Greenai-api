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

## 배포 구조

- **포트**: 8000 (컨테이너 내부), 80 (외부 노출)
- **정적 파일**: `/static` 경로로 제공
- **응답 형태**: HTML
