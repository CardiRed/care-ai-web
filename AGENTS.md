# 프로젝트 작업 규칙

## 시작 순서
AGENTS.md → README.md → PROJECT_STATUS.md → TEST-RESULTS.md → docs/ARCHITECTURE.md → docs/DECISIONS.md → CHANGELOG.md를 읽고 실제 Git 상태를 대조한다.

- 저장소: https://github.com/CardiRed/care-ai-web.git
- 초기 원격은 비어 있었고 clone의 기준 브랜치는 main이었다. 재개 시 remote HEAD와 브랜치를 다시 확인한다.
- 현재 제품 버전 2.0.0. 동작 추가는 minor, 호환 수정은 patch, 호환 파괴는 major. 문서만 바꾸면 제품 버전을 올리지 않는다.
- 시간대 UTC. 커밋 제목 `v<version>_YYYYMMDD HH:MM_<짧은 작업 내용>`.
- 일반적인 승인된 작업은 main에 fast-forward push. 보호 규칙이 있거나 거부되면 작업 브랜치·PR로 진행하며 우회하지 않는다.

## 환경·동기화
Git/Node/npm 버전, remote, status, branch, HEAD를 확인한다. gh는 선택 도구이며 없더라도 Git 인증으로 작업할 수 있다. 인증 필요 시 사용자가 브라우저에서 로그인하도록 안내하고 토큰을 대화에 요구하지 않는다. 신원은 기존 Git 설정을 확인해 사용하고 임의로 다른 사람을 사칭하지 않는다.

미커밋·미추적 작업을 먼저 보존한 후 fetch한다. 양쪽 이력을 비교하고 원격만 앞설 때 pull --ff-only. 분기되면 변경을 보존해 병합 또는 명시된 정책을 따른다. 강제 push, reset --hard, clean -fd, 무분별한 파일 삭제 금지.

## 구현과 검증
앱은 루트 index.html/style.css/script.js 세 파일로 유지한다. 런타임 외부 의존성·백엔드·프레임워크 교체를 임의 도입하지 않는다. localStorage 키와 기존 데이터 호환성을 보존한다. 시연 점수를 실제 AI/위험 확률로 표현하지 않는다.

bootstrap: npm ci, npx playwright install chromium. 필수 검사: npm run check, npm test, npm run package. Windows Edge 대체 경로는 README 참조. 브라우저 기본 흐름·점수·방문·저장·사진·취소·오류·반응형을 확인하며 실제 실행한 범위만 기록한다. 생성 결과는 dist/, 테스트 캡처는 test-results/이며 추적하지 않는다.

## 마감
상태·테스트·설계·변경 이력을 갱신한다. 명시적 파일 stage 후 staged diff와 비밀값·개인정보·불필요한 산출물 포함 여부를 확인한다. commit 후 fetch, 허용된 브랜치 push, HEAD와 ls-remote 브랜치 SHA 일치까지 확인한다. 미푸시 상태를 원격 완료로 쓰지 않는다.

Release/태그/Drive 업로드는 일반 push와 별도 작업이며 이번 초기 이관에는 해당 없음. 릴리스가 요청되면 annotated tag의 원격 커밋, 패키지, SHA256, 게시 위치를 확인한다. Drive 경로는 미지정이며 임의 생성·업로드하지 않는다.

원격 실패가 지속되면 안전한 변경을 로컬 커밋하고 작업 트리 밖에 git bundle --all, 선별 소스 ZIP, SHA256, 복구 README를 보존한다. bundle verify로 검사하고 실패·미검증·미푸시 SHA·백업 위치를 알린다. LFS/submodule/외부 데이터·비밀값은 현재 사용하지 않는다.
