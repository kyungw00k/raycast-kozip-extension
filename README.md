# KoZip - Raycast용 한국 우편번호 검색

[English](README.en.md) | 한국어

Postcodify API를 사용하여 한국 주소를 검색하는 Raycast 확장입니다. 다양한 형식의 한국 주소를 빠르게 찾고 복사할 수 있으며, 다국어를 지원합니다.

## 주요 기능

- 🔍 **빠른 한국 주소 검색** - 실시간으로 한국 주소 검색 결과 제공
- 🌐 **다국어 지원** - 한국어 및 영어 주소 형식 지원
- 📋 **다양한 복사 옵션** - 여러 형식으로 주소 복사 가능
- 🗺️ **지도 연동** - 카카오맵, 네이버 지도에서 위치 확인
- 🚀 **성능 최적화** - 지능형 캐싱으로 빠른 반복 검색
- 🌍 **국제화** - 동적 로케일 로딩 및 fallback 지원

## 설치

1. [Raycast Store](https://raycast.com/store)에서 확장 설치
2. 또는 로컬 설치:
   ```bash
   git clone <repository-url>
   cd raycast-korea-zipcode-finder
   npm install
   npm run dev
   ```

## 사용법

1. Raycast를 열고 `kz` 또는 "KoZip" 입력
2. 검색어 입력 (한국 주소, 건물명, 또는 우편번호)
3. 결과를 보고 키보드 단축키로 다양한 작업 수행:

### 키보드 단축키

- **Enter**: 한국 도로명 주소 (우편번호 포함) 복사
- **⌘ + C**: 영어 도로명 주소 (우편번호 포함) 복사
- **⌘ + T**: 도로명 주소와 지번 주소 전환
- **⌘ + O**: 카카오맵에서 열기
- **⌘ + ⇧ + O**: 네이버 지도에서 열기

## 주소 형식

확장에서 제공하는 다양한 주소 형식:

### 한국어 형식
- **도로명 주소**: `(12345) 서울특별시 강남구 테헤란로 123`
- **지번 주소**: `(12345) 서울특별시 강남구 역삼동 123-45`

### 영어 형식
- **도로명 주소**: `123 Teheran-ro, Gangnam-gu, Seoul (12345)`
- **지번 주소**: `123-45 Yeoksam-dong, Gangnam-gu, Seoul (12345)`

## 아키텍처

### 프로젝트 구조
```
src/
├── kz.tsx              # 메인 확장 로직
└── locales/            # 국제화
    ├── index.ts        # 로케일 유틸리티
    ├── ko.json         # 한국어 문자열
    └── en.json         # 영어 문자열
```

### 주요 컴포넌트
- **Command()**: 메인 검색 인터페이스 컴포넌트
- **SearchListItem()**: 개별 주소 결과 컴포넌트
- **getLocalizedStrings()**: 동적 로케일 로딩 (fallback 포함)
- **parseFetchResponse()**: API 응답 파서

## 새 언어 추가

새로운 언어 지원을 추가하려면:

1. 새 로케일 파일 생성: `src/locales/{언어코드}.json`
2. `en.json`의 구조를 복사하고 문자열 번역
3. 확장이 자동으로 새 로케일을 감지하고 로드

일본어 예시 (`ja.json`):
```json
{
  "searchPlaceholder": "韓国の住所を検索...",
  "resultsTitle": "検索結果",
  "copyKoreanAddress": "韓国住所をコピー",
  ...
}
```

## API 통합

주소 데이터를 위해 [Postcodify API](https://postcodify.poesis.kr/) 사용:
- **엔드포인트**: `https://api.poesis.kr/post/search.php`
- **기능**: 실시간 검색, 한국어/영어 결과, 건물명 지원
- **캐싱**: 성능 향상을 위한 24시간 로컬 캐시

## 개발

### 설정
```bash
npm install
npm run dev
```

### 명령어
- `npm run dev` - 핫 리로드로 개발 시작
- `npm run build` - 프로덕션 빌드
- `npm run lint` - ESLint 검사 실행
- `npm run fix-lint` - 린트 이슈 자동 수정
- `npm run publish` - Raycast Store에 게시

### 기술 스택
- **Raycast API**: 확장 프레임워크
- **TypeScript**: 타입 안전 개발
- **React Hooks**: 상태 관리
- **Postcodify API**: 주소 데이터 소스

## 캐시 관리

확장에서 구현된 지능형 캐싱:
- **기간**: 검색 쿼리당 24시간
- **저장소**: 자동 정리 기능이 있는 로컬 스토리지
- **이점**: 빠른 반복 검색, API 호출 감소

## 기여

1. 저장소를 fork
2. 기능 브랜치 생성: `git checkout -b feature/새기능`
3. 변경사항 작성 및 테스트 추가
4. 설명적인 커밋 메시지로 커밋
5. Push 후 Pull Request 생성

## 라이선스

MIT License - 자세한 내용은 [LICENSE](LICENSE) 파일 참조.

## 크레딧

- **API**: [Postcodify](https://postcodify.poesis.kr/) by Poesis
- **지도**: 카카오맵, 네이버 지도 연동
- **아이콘**: [한국 우정사업본부 엠블럼](https://ko.m.wikipedia.org/wiki/%ED%8C%8C%EC%9D%BC:Emblem_of_Korea_Post.svg)을 기반으로 제작
- **작성자**: [kyungw00k](https://github.com/kyungw00k)

## 지원

문제가 발생하거나 제안사항이 있으면:
1. 기존 [이슈](https://github.com/your-repo/issues) 확인
2. 상세한 정보와 함께 새 이슈 생성
3. 기능 요청은 enhancement 라벨 사용