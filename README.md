# 🛡️ Sentinel AI Platform

**AI 기반 실시간 보안 분석 및 위협 탐지 플랫폼**

차세대 Security Operations Dashboard - 보안 연구자 및 개발자를 위한 통합 분석 환경

---

## 📋 프로젝트 개요

Sentinel AI Platform은 실시간 로그 분석, 위협 인텔리전스 조회, 행동 기반 이상 탐지 및 AI 기반 자동 대응을 지원하는 통합 보안 분석 플랫폼입니다.

### 주요 특징

- 🔴 **실시간 로그 스트리밍** - WebSocket 기반 실시간 이벤트 처리
- 🤖 **AI 보안 어시스턴트** - 자연어 기반 위협 분석 및 보안 가이드
- 📊 **실시간 대시보드** - 이벤트 수집량, 위험도, 시스템 상태 모니터링
- 🔍 **위협 인텔리전스** - VirusTotal, AbuseIPDB, ThreatFox API 기반 IOC 분석
- 🎯 **이상 행위 탐지** - 행동 기반 분석 및 이벤트 상관관계 분석
- 🔐 **인증 보안 분석** - 세션 무결성 검증 및 비정상 접근 패턴 탐지
- ⚙️ **사용자 승인 기반 대응** - 차단 정책 추천 및 승인 기반 방어 워크플로우

---

## 🏗️ 기술 스택

### Frontend
- **React 18** + **Vite** (초고속 개발 환경)
- **TypeScript** (타입 안전성)
- **TailwindCSS** (유틸리티 기반 스타일링)
- **Socket.IO Client** (실시간 통신)
- **Recharts** (데이터 시각화)
- **Dark Theme UI** (다크모드 기본)

### Backend
- **Python 3.11+**
- **FastAPI** (고성능 비동기 API)
- **WebSocket** (실시간 양방향 통신)
- **Uvicorn** (ASGI 서버)
- **AsyncIO** (비동기 이벤트 처리)
- **Pydantic** (데이터 검증)

### AI Engine
- **Ollama** (로컬 LLM)
- **LangChain** (LLM 통합)
- **OpenAI Compatible API** (호환 가능한 API)

### Database & Cache
- **Redis** (실시간 캐시 및 메시지 큐)
- **PostgreSQL** (메타데이터 및 분석 결과 저장, 선택사항)

### Security Stack
- **YARA** (악성코드 탐지)
- **Sigma Rules** (로그 분석 규칙)
- **VirusTotal API** (파일 및 URL 위협 분석)
- **AbuseIPDB API** (IP 평판 조회)
- **ThreatFox API** (IOC 위협 정보)

### Deployment
- **Docker** & **Docker Compose** (컨테이너화)
- **VSCode 최적화**

---

## 📁 프로젝트 구조

```
sentinel-ai-platform/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py                 # FastAPI 메인 애플리케이션
│   │   ├── api/
│   │   │   ├── routes/             # API 엔드포인트
│   │   │   │   ├── logs.py
│   │   │   │   ├── intelligence.py
│   │   │   │   ├── analysis.py
│   │   │   │   └── alerts.py
│   │   │   └── websocket.py        # WebSocket 핸들러
│   │   ├── engines/
│   │   │   ├── __init__.py
│   │   │   ├── detection.py        # 이상 탐지 엔진
│   │   │   ├── intelligence.py     # 위협 인텔리전스 엔진
│   │   │   ├── ai_analyzer.py      # AI 분석 엔진
│   │   │   └── auth_analyzer.py    # 인증 분석 모듈
│   │   ├── models/
│   │   │   ├── schemas.py          # Pydantic 스키마
│   │   │   └── database.py         # DB 모델 (선택사항)
│   │   ├── services/
│   │   │   ├── threat_intel.py     # 위협 인텔리전스 서비스
│   │   │   ├── event_stream.py     # 이벤트 스트리밍
│   │   │   └── cache.py            # Redis 캐시
│   │   ├── utils/
│   │   │   ├── logger.py           # 로깅 설정
│   │   │   ├── validators.py       # 데이터 검증
│   │   │   └── helpers.py          # 유틸리티 함수
│   │   └── config/
│   │       └── settings.py         # 환경 설정
│   ├── tests/
│   │   └── test_*.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── main.tsx                # 엔트리 포인트
│   │   ├── App.tsx
│   │   ├── components/
│   │   │   ├── Dashboard/          # 대시보드
│   │   │   ├── Console/            # 실시간 콘솔
│   │   │   ├── Chat/               # AI 채팅
│   │   │   ├── ThreatIntel/        # 위협 인텔
│   │   │   ├── Alerts/             # 알림 센터
│   │   │   ├── SessionMonitor/     # 세션 모니터
│   │   │   ├── NetworkActivity/    # 네트워크 활동
│   │   │   └── Common/             # 공통 컴포넌트
│   │   ├── pages/
│   │   │   ├── Home.tsx
│   │   │   ├── Analysis.tsx
│   │   │   └── Settings.tsx
│   │   ├── services/
│   │   │   ├── api.ts              # API 클라이언트
│   │   │   └── websocket.ts        # WebSocket 연결
│   │   ├── hooks/
│   │   │   ├── useWebSocket.ts
│   │   │   └── useApi.ts
│   │   ├── types/
│   │   │   └── index.ts            # TypeScript 타입
│   │   ├── utils/
│   │   │   └── formatters.ts
│   │   ├── styles/
│   │   │   └── globals.css
│   │   └── assets/
│   ├── public/
│   ├── package.json
│   ├── vite.config.ts
│   ├── tsconfig.json
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   └── Dockerfile
├── docs/
│   ├── architecture.md             # 아키텍처 설명
│   ├── api.md                      # API 문서
│   ├── setup.md                    # 설치 가이드
│   └── guides/
│       ├── threat_intel.md
│       ├── ai_chat.md
│       └── deployment.md
├── docker-compose.yml
├── .gitignore
├── .dockerignore
└── LICENSE
```

---

## 🚀 빠른 시작

### 사전 요구사항
- Docker & Docker Compose
- Node.js 18+
- Python 3.11+
- Ollama (선택사항, 로컬 LLM용)

### 개발 환경 설정

```bash
# 저장소 클론
git clone https://github.com/bigad2007/sentinel-ai-platform.git
cd sentinel-ai-platform

# Docker Compose로 실행
docker-compose up -d

# 또는 로컬 개발 모드

# Backend 설정
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
python -m uvicorn app.main:app --reload

# 새 터미널에서 Frontend 설정
cd frontend
npm install
npm run dev
```

### 접속
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8000
- **API 문서**: http://localhost:8000/docs

---

## 📖 주요 기능 가이드

### 1. 실시간 로그 스트리밍
- WebSocket을 통한 실시간 이벤트 수신
- 자동 필터링 및 분류
- 다양한 로그 소스 지원

### 2. AI 보안 채팅
- 자연어 기반 질의응답
- 위협 설명 및 분석
- 코드 취약점 분석
- 방어 전략 제안

### 3. 위협 인텔리전스
- IP/URL 평판 조회
- IOC(Indicators of Compromise) 분석
- 공개 위협 정보 통합
- 실시간 위협 상관관계

### 4. 이상 행위 탐지
- 행동 기반 분석
- 이벤트 상관관계 분석
- 실시간 위험 이벤트 탐지
- 맥락 기반 점수 산정

### 5. 인증 보안 분석
- 세션 무결성 검증
- 비정상 접근 패턴 탐지
- 인증 흐름 분석
- 이상 인증 이벤트 경고

### 6. 사용자 승인 기반 대응
- 자동화 정책 제안
- 사용자 승인 워크플로우
- 방어 정책 실행 이력
- 감사 로그 기록

---

## 🔒 보안 고려사항

- ✅ 로컬 환경 우선 처리
- ✅ 민감한 데이터 암호화
- ✅ API 키 환경변수 관리
- ✅ HTTPS/WSS 지원 (프로덕션)
- ✅ 사용자 승인 기반 자동화
- ✅ 감사 로그 기록
- ✅ 권한 기반 접근 제어 (선택사항)

---

## 📚 문서

- [아키텍처 가이드](docs/architecture.md)
- [API 문서](docs/api.md)
- [설치 가이드](docs/setup.md)
- [위협 인텔리전스 가이드](docs/guides/threat_intel.md)
- [AI 채팅 가이드](docs/guides/ai_chat.md)
- [배포 가이드](docs/guides/deployment.md)

---

## 🛠️ 개발 로드맵

### Phase 1: 기본 인프라 (현재)
- [x] 프로젝트 구조 설정
- [ ] FastAPI 기본 서버
- [ ] React Vite 프론트엔드
- [ ] WebSocket 양방향 통신
- [ ] 기본 대시보드 UI

### Phase 2: 핵심 기능
- [ ] 실시간 로그 스트리밍
- [ ] AI 채팅 통합
- [ ] 위협 인텔리전스 API
- [ ] 이상 탐지 엔진
- [ ] 인증 분석 모듈

### Phase 3: 고급 기능
- [ ] 자동화 대응 시스템
- [ ] 포렌식 분석 도구
- [ ] 플러그인 시스템
- [ ] 통계 분석
- [ ] 보고서 생성

### Phase 4: 최적화 & 배포
- [ ] 성능 최적화
- [ ] 규모 확장성
- [ ] Kubernetes 배포
- [ ] 모니터링 & 로깅
- [ ] CI/CD 파이프라인

---

## 🤝 기여 가이드

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. [LICENSE](LICENSE) 참조

---

## 📞 연락 & 지원

- 📧 Issues: GitHub Issues 사용
- 💬 Discussions: GitHub Discussions 사용
- 🔗 Repository: https://github.com/bigad2007/sentinel-ai-platform

---

**Made with 🛡️ for Security Researchers & Developers**
