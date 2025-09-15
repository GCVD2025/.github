# GCVD2025 - 디자이너 게스트 포트폴리오 프로젝트

GCVD2025는 디자이너 게스트의 포트폴리오 및 방명록 시스템을 구현한 풀스택 웹 애플리케이션입니다. 사용자들이 포트폴리오를 확인하고 방명록을 작성할 수 있는 인터랙티브한 플랫폼을 제공합니다.

## 📋 프로젝트 개요

이 프로젝트는 세 개의 주요 저장소로 구성되어 있습니다:

- **GCVD-Frontend**: Next.js 기반의 프론트엔드 애플리케이션
- **GCVD-Backend**: Spring Boot 기반의 백엔드 API 서버
- **.github**: GitHub 조직 설정 및 문서

## 🏗️ 시스템 아키텍처

```
┌─────────────────┐    HTTP/REST API    ┌─────────────────┐    Redis    ┌─────────────────┐
│   Next.js       │◄──────────────────►│  Spring Boot    │◄───────────►│     Redis       │
│   Frontend      │                     │    Backend      │             │    Database     │
│                 │                     │                 │             │                 │
│ - TypeScript    │                     │ - Kotlin        │             │ - 방명록 데이터  │
│ - Framer Motion │                     │ - JPA/Hibernate │             │ - 세션 관리     │
│ - Tailwind CSS  │                     │ - Swagger/OpenAPI│             │                 │
└─────────────────┘                     └─────────────────┘             └─────────────────┘
```

## 🚀 기술 스택

### Frontend (GCVD-Frontend)
- **Framework**: Next.js 15.5.3 (App Router)
- **Language**: TypeScript 5.x
- **Styling**: Tailwind CSS 4.x
- **Animation**: Framer Motion 12.x
- **UI Components**: React 19.x
- **Build Tool**: Turbopack
- **Package Manager**: Yarn

### Backend (GCVD-Backend)
- **Framework**: Spring Boot 3.5.5
- **Language**: Kotlin 1.9.25
- **Database**: Redis (in-memory)
- **ORM**: Spring Data Redis
- **Documentation**: Swagger/OpenAPI 3 (springdoc-openapi)
- **Build Tool**: Gradle 8
- **Java Version**: JDK 17
- **Containerization**: Docker

## 📁 프로젝트 구조

### Frontend 구조
```
src/
├── app/                    # Next.js App Router
│   ├── layout.tsx         # 루트 레이아웃
│   ├── page.tsx           # 홈페이지
│   └── globals.css        # 글로벌 스타일
├── components/            # 재사용 가능한 컴포넌트
│   ├── AnimatedButton.tsx # 애니메이션 버튼
│   ├── AnimatedCard.tsx   # 애니메이션 카드
│   ├── FadeInText.tsx     # 페이드인 텍스트
│   ├── Navigation.tsx     # 내비게이션 바
│   └── index.ts          # 컴포넌트 익스포트
```

### Backend 구조
```
src/main/kotlin/com/gcvd/
├── Gcvd2025Application.kt  # 메인 애플리케이션 클래스
├── api/                    # API 인터페이스 정의
│   └── GuestBookApi.kt    # 방명록 API 스펙
├── controller/            # REST 컨트롤러
│   └── GuestBookController.kt
├── service/               # 비즈니스 로직
│   └── GuestBookService.kt
├── repository/            # 데이터 접근 계층
│   └── GuestBookRepository.kt
├── entity/                # 도메인 엔티티
│   └── GuestBook.kt
└── dto/                   # 데이터 전송 객체
    └── GuestBookDTO.kt
```

## 🎯 주요 기능

### Frontend 기능
- **반응형 디자인**: 모바일, 태블릿, 데스크톱 지원
- **인터랙티브 애니메이션**: Framer Motion을 활용한 부드러운 UI/UX
- **내비게이션**: 홈, 포트폴리오, 프로젝트, 연락처 페이지
- **다크모드 지원**: 시스템 설정에 따른 자동 테마 변경
- **성능 최적화**: Next.js의 이미지 최적화 및 폰트 최적화

### Backend 기능
- **방명록 시스템**: 
  - 방명록 작성 (`POST /api/guestbook`)
  - 방명록 목록 조회 (`GET /api/guestbook`)
- **데이터 검증**: 
  - 작성자명: 1-50자 제한
  - 내용: 1-300자 제한
- **API 문서화**: Swagger UI 제공
- **로깅**: 요청 처리 시간 및 IP 추적
- **에러 핸들링**: 상세한 검증 오류 메시지

## 🗃️ 데이터 모델

### GuestBook Entity
```kotlin
@RedisHash("guestbook")
data class GuestBook(
    val author: String,      // 작성자 (1-50자)
    val content: String,     // 내용 (1-300자)
    val id: String,          // UUID
    val createdAt: LocalDateTime // 작성 시간
)
```

## 🔧 개발 환경 설정

### 사전 요구사항
- Node.js 18+ 
- Yarn
- JDK 17+
- Redis Server
- Docker (선택사항)

### Frontend 설정
```bash
# 저장소 클론
git clone https://github.com/GCVD2025/GCVD-Frontend.git
cd GCVD-Frontend

# 의존성 설치
yarn install

# 개발 서버 실행
yarn dev

# 프로덕션 빌드
yarn build
```

### Backend 설정
```bash
# 저장소 클론
git clone https://github.com/GCVD2025/GCVD-Backend.git
cd GCVD-Backend

# 환경 변수 설정
export REDIS_HOST=localhost:6379
export REDIS_PASSWORD=your_password
export SWAGGER_PATH=/swagger-ui.html
export API_DOCS_PATH=/v3/api-docs

# 애플리케이션 실행
./gradlew bootRun

# 프로덕션 빌드
./gradlew build
```

### Docker로 Backend 실행
```bash
# Docker 이미지 빌드
docker build -t gcvd-backend .

# 컨테이너 실행
docker run -p 8080:8080 \
  -e REDIS_HOST=your-redis-host \
  -e REDIS_PASSWORD=your-redis-password \
  gcvd-backend
```

## 📡 API 엔드포인트

### 방명록 API

| Method | Endpoint | Description | 
|--------|----------|-------------|
| GET    | `/api/guestbook` | 방명록 목록 조회 (최신순) |
| POST   | `/api/guestbook` | 새 방명록 작성 |

### API 요청/응답 예시

**방명록 작성 요청:**
```json
POST /api/guestbook
Content-Type: application/json

{
  "author": "홍길동",
  "content": "안녕하세요! 멋진 포트폴리오네요."
}
```

**방명록 조회 응답:**
```json
GET /api/guestbook

[
  {
    "author": "홍길동",
    "content": "안녕하세요! 멋진 포트폴리오네요.",
    "createdAt": "2025-09-15T14:30:00"
  }
]
```

## 📚 API 문서

백엔드 서버 실행 후 Swagger UI에서 상세한 API 문서를 확인할 수 있습니다:
- URL: `http://localhost:8080/swagger-ui.html`
- API Docs: `http://localhost:8080/v3/api-docs`

## 🔍 주요 컴포넌트 설명

### Frontend 컴포넌트

1. **Navigation.tsx**: 고정 내비게이션 바
   - 반응형 메뉴
   - 현재 페이지 하이라이트
   - 부드러운 애니메이션 효과

2. **AnimatedCard.tsx**: 호버 및 클릭 애니메이션이 있는 카드
   - 스케일 애니메이션
   - 커스터마이즈 가능한 지연시간

3. **FadeInText.tsx**: 페이드인 효과가 있는 텍스트
   - 스크롤 기반 애니메이션
   - 부드러운 등장 효과

### Backend 아키텍처

1. **Controller Layer**: REST API 엔드포인트 제공
2. **Service Layer**: 비즈니스 로직 처리
3. **Repository Layer**: 데이터 접근 및 Redis 연동
4. **DTO Pattern**: 계층 간 데이터 전송 최적화

## 🚀 배포

### Frontend 배포 (Vercel 권장)
```bash
# Vercel CLI 설치
npm i -g vercel

# 배포
vercel --prod
```

### Backend 배포 (Docker)
```bash
# 이미지 빌드
docker build -t gcvd-backend .

# 컨테이너 레지스트리에 푸시
docker tag gcvd-backend your-registry/gcvd-backend
docker push your-registry/gcvd-backend
```

## 🤝 기여 방법

1. 이 저장소를 포크합니다
2. 새로운 기능 브랜치를 생성합니다 (`git checkout -b feature/amazing-feature`)
3. 변경사항을 커밋합니다 (`git commit -m 'Add some amazing feature'`)
4. 브랜치에 푸시합니다 (`git push origin feature/amazing-feature`)
5. Pull Request를 생성합니다

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](https://github.com/GCVD2025/GCVD-Backend/blob/main/LICENSE) 파일을 참조하세요.

## 🐛 문제 보고

버그를 발견하거나 기능 요청이 있다면 다음 저장소의 Issues 섹션을 이용해주세요:
- Frontend 이슈: [GCVD-Frontend Issues](https://github.com/GCVD2025/GCVD-Frontend/issues)
- Backend 이슈: [GCVD-Backend Issues](https://github.com/GCVD2025/GCVD-Backend/issues)

## 👥 개발팀

- **프론트엔드 개발**: TypeScript, Next.js, Framer Motion
- **백엔드 개발**: Kotlin, Spring Boot, Redis
- **DevOps**: Docker, GitHub Actions

---

*이 프로젝트는 디자이너 게스트의 포트폴리오 및 방명록 시스템을 위해 개발되었습니다.*