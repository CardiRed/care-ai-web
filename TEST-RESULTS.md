# 검증 결과

2026-09-14 UTC · 초기 이관 작업 트리 기준. 소스는 전달된 v2 index.html/style.css/script.js와 동일하며 테스트 경로만 저장소 상대 경로로 일반화했다.

환경: Windows, Node.js 24.14.0, npm 11.9.0, Playwright 1.62.1, 설치된 Edge(headless). Git 2.53.0.windows.1. 기본 Chromium 실행은 이번 환경에서 미실행.

- npm run check: 통과.
- BROWSER_CHANNEL=msedge npm test: 통과. PowerShell 설정 문법은 README 참조.
- 점수 0/93 예시, 사진 업로드·저장, 관리자 평, 방문 기록, 등록·새로고침 유지, 취소/조회 모드: 통과.
- 5개 화면 × 6개 폭(320/390/600/768/1024/1440px)의 문서 가로 넘침 검사: 통과.
- 강제 저장 실패 후 입력 유지, 음수 거부, 뒤로가기 검색 복원, 미저장 뒤로가기 취소, 200% CSS 확대: 통과.
- npm run package: 실행 폴더 생성 통과. 패키지에서 별도 브라우저 실행은 아래 후속 기록 확인.

초기 테스트 이식 시 작은 PNG fixture가 브라우저에서 해석되지 않아 사진 대기 검사 실패. 현재는 테스트 자체가 생성한 정상 PNG를 입력으로 사용하며 전체 재검사 통과. 제품 코드 변경 없음.

미검증: 실제 iOS/Android와 가상 키보드, 스크린리더 전체 경로, 고대비/전체 대비 감사, 장시간/대량 데이터, 모든 브라우저·실제 배율, 실제 사용자 의료 판단, 보안 인증. CSS 확대는 실제 브라우저 확대 전 범위 검증을 뜻하지 않는다.

## 원격 신규 사본 재개 확인 · 2026-09-14 04:45 UTC

검증한 원격 main 코드 SHA: e8d87626bb7d26596a9c8de3b5bdd280e18229e8. GitHub에서 새로운 폴더로 clone한 사본에서 저장소의 AGENTS/README 절차로 실행했다. 원본 첨부나 작업용 파일을 테스트 입력으로 사용하지 않았다. 이전 npm 다운로드 캐시와 설치된 Edge는 재사용하므로 새 OS 전체 설치 검증과는 구분한다.

- npm ci --offline --cache <기존 다운로드 캐시>: 잠금 파일 설치 통과.
- npm run check / BROWSER_CHANNEL=msedge npm test / npm run package: 모두 통과.
- dist/care-ai-web-v2.0.0/index.html을 별도 브라우저 페이지로 열어 대시보드 및 분석 화면 이동: 통과.
- GitHub 원격 HEAD가 main이며 위 코드 SHA와 일치함을 ls-remote로 확인.
- 이 검증 이후 변경은 PROJECT_STATUS 및 TEST-RESULTS 문서뿐이다.

환경 복구: sandbox Git 인증 호출이 실패하여 기존 사용자 인증 환경에서 한정된 safe.directory 명령 옵션으로 push 성공. Windows schannel 오류는 해당 로컬 저장소의 sslBackend=openssl로 해결했고 TLS 검증은 비활성화하지 않았다. gh가 없어도 기존 Git 인증으로 완료했다. 전역 보안 설정이나 토큰 파일은 저장소에 추가하지 않았다.
