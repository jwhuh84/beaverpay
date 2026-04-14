# BeaverPay Next - 프로젝트 지침

## 프로젝트 목적
차세대 비버페이 앱 개발을 위한 **테스트 앱** 프로젝트.
모바일에서 실제 앱처럼 동작하는 **PWA(Progressive Web App)** 기반 모바일웹으로 구현.

## 핵심 원칙

### 1. 모바일 우선 (Mobile First)
- 모든 UI/UX는 모바일 화면(375px~430px 기준) 기준으로 설계
- 터치 인터랙션, 스와이프, 탭 등 모바일 제스처 고려
- iOS Safari, Android Chrome 호환성 확인

### 2. PWA 필수 요건
- `manifest.json` 유지 및 관리
- Service Worker(`sw.js`) 통한 오프라인 지원
- 홈 화면 추가(Add to Home Screen) 지원
- `display: standalone` 모드로 앱처럼 동작

### 3. 정책서 우선 확인
**개발 전 반드시 비버페이 차세대 정책서를 확인한다.**
- Confluence 정책서: https://beaverworks.atlassian.net/wiki/spaces/bpnew/pages/104660993/v6.0
- 해당 페이지 하위 문서들을 포함한 전체 정책 내용 참조
- 정책서에 정의된 기능 흐름, UX 규칙, 비즈니스 로직을 코드에 반영

### 4. 이미지·리소스 내재화 필수
**index.html 단일 파일로 팀원과 공유하기 때문에, 모든 이미지와 리소스는 반드시 파일 안에 내재화한다.**
- 이미지는 외부 파일 경로(`url('card-blue.png')`) 사용 금지
- 반드시 base64로 인코딩하여 CSS/HTML 내부에 직접 삽입
- 신규 이미지 추가 시: `node -e "require('fs').readFileSync('파일명').toString('base64')"` 로 변환 후 삽입
- 외부 CDN, 외부 URL 이미지도 동일하게 금지

## 기술 스택
- 현재: Vanilla HTML/CSS/JS (단일 파일 구조)
- PWA: manifest.json + sw.js 구성
- 향후 프레임워크 전환 시 이 파일 업데이트 필요

## 파일 구조
```
beaverpay-next/
├── index.html        # 메인 앱
├── manifest.json     # PWA 설정
├── sw.js             # Service Worker
├── icon-192.png      # PWA 아이콘
├── icon-512.png      # PWA 아이콘
├── card-blue.png     # 카드 이미지
├── card-purple.png   # 카드 이미지
└── card-yellow.png   # 카드 이미지
```

## 개발 시 체크리스트
- [ ] 정책서 해당 기능 항목 확인
- [ ] 모바일 뷰포트에서 레이아웃 검증
- [ ] PWA 기능(오프라인, 설치) 영향 여부 확인
- [ ] 터치 이벤트 및 모바일 인터랙션 테스트
