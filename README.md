# care-ai-web · 온돌

돌봄 담당자가 대상자 정보를 살펴보고 방문 우선순위를 검토하는 **프론트엔드 시연**입니다. 현재 버전 2.0.0.

## 바로 실행
저장소를 내려받고 루트 `index.html`을 최신 Edge 또는 Chrome에서 엽니다. `style.css`, `script.js`를 같은 폴더에 두세요. 서버·인터넷·Node.js가 필요하지 않습니다. PC와 모바일 폭에 반응하지만 설치형 네이티브 앱은 아닙니다.

## 개발·검증
Node.js 22 이상, npm, Git이 필요합니다. 검증 환경은 Node 24.14.0입니다.

```sh
git clone https://github.com/CardiRed/care-ai-web.git
cd care-ai-web
npm ci
npx playwright install chromium
npm run check
npm test
npm run package
```

설치된 Edge로 검사하려면 PowerShell에서 `$env:BROWSER_CHANNEL='msedge'` 후 `npm test`를 실행합니다. 기본값은 Playwright Chromium입니다. 제한된 환경의 npm 캐시는 `npm ci --cache <쓰기 가능한 경로>`로 지정할 수 있습니다. Linux에서 브라우저 시스템 라이브러리가 필요하면 공식 Playwright 설치 절차에 따라 `npx playwright install --with-deps chromium`을 사용합니다.

## 기능
- 대시보드, 검색·필터·정렬, 프로필 등록·수정, 사진 업로드
- 100점 만점 돌봄 확인 점수, 자동 설명, 관리자 한줄 평
- 막대·방사형 그래프, 유형 분포, 오늘 방문 제안·완료 기록
- 로컬 저장, 저장 실패 시 입력 보존, 미저장 이동 확인, 브라우저 탐색 이력

점수·분류·방문 기준은 검증된 의료 판단이 아닌 시연 규칙입니다. 관리자·조회자 전환은 실제 인증이 아닙니다. 실제 개인정보를 입력하지 마세요. 저장은 브라우저 localStorage에만 이루어지고 다른 기기와 공유되지 않습니다.

## 이어서 작업
[AGENTS.md](AGENTS.md) → [PROJECT_STATUS.md](PROJECT_STATUS.md) → [TEST-RESULTS.md](TEST-RESULTS.md)를 읽으세요. 구조·계산식은 [설계 문서](docs/ARCHITECTURE.md), 결정 이유는 [DECISIONS](docs/DECISIONS.md)에 있습니다. GitHub가 공유 기준이며 이전 대화나 PC 경로는 필요하지 않습니다.
