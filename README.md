# 마롱뉴데이CC 예약현황 대시보드 - Vercel 배포

## 폴더 구성

```
vercel_deploy/
├── index.html        ← 선용님 대시보드 (메인, 블루 테마)
├── ceo.html          ← 대표님 개인 회원권 대시보드 (에메랄드+골드 테마)
├── vercel.json       ← Vercel 설정 (캐시·헤더)
└── README.md         ← 이 문서
```

배포 후 URL:
- `https://[프로젝트명].vercel.app/` → 선용님 대시보드
- `https://[프로젝트명].vercel.app/ceo` → 대표님 대시보드 (cleanUrls)
- `https://[프로젝트명].vercel.app/ceo.html` 도 동일하게 동작

## 배포 방법 1 — Vercel 웹 UI (Drag & Drop, 가장 간단)

1. https://vercel.com 접속 후 GitHub/Google 등으로 로그인
2. 대시보드 우상단 **"Add New..."** → **"Project"** 클릭
3. **"Import Third-Party Git Repository"** 옆의 **"Deploy"** 아래 작은 **"Browse"** 또는 화면 빈 곳으로 이 `vercel_deploy` 폴더 자체를 드래그 앤 드롭
4. 프로젝트 이름 입력 → **Deploy** 클릭
5. 1~2분 뒤 발급된 URL로 접속

(만약 드래그 옵션이 보이지 않으면 → 아래 CLI 방법을 사용)

## 배포 방법 2 — Vercel CLI

```bash
# 1. CLI 설치 (한 번만)
npm install -g vercel

# 2. 이 폴더로 이동
cd "C:\Users\Administrator\Desktop\마론뉴데이\vercel_deploy"

# 3. 첫 배포 (안내에 따라 로그인 + 프로젝트 연결)
vercel

# 4. 프로덕션 배포
vercel --prod
```

## 업데이트 흐름

대시보드 데이터가 바뀌면(예약 추가/취소/완료):

1. 사용자: "내 대시보드 업데이트해줘" 라고 채팅으로 요청
2. Claude가 마롱뉴데이 사이트 크롤링 후 `index.html`/`ceo.html` 갱신
3. 갱신된 파일을 `vercel_deploy/` 폴더로 복사
4. Vercel에 다시 배포:
   - 웹 UI: 새 폴더 다시 업로드
   - CLI: `vercel --prod`

자동화하려면:
- GitHub 리포지토리에 연결 → push 시 자동 배포
- 또는 GitHub Action / 스케줄러로 주기적 redeploy 트리거

## 주의 사항

⚠️ **공개 URL입니다**
- 대시보드에 실명(대표님, 안준영 이사, 이선용 팀장, 염지훈 팀장)과 예약 일정이 포함되어 있습니다.
- URL을 아는 사람은 누구나 접근 가능합니다.
- 비공개로 운영하려면:
  - Vercel Pro($20/월)의 Password Protection 사용
  - 또는 기본인증(basic auth) Edge Function 추가
  - 또는 URL을 추측 어렵게 만들기 (예: `apple-banana-2026.vercel.app`)

⚠️ **데이터는 baked-in 정적 HTML**
- 페이지 자체에 예약 정보가 박혀있습니다.
- 실시간 동기화가 아니므로 업데이트 후 반드시 재배포 필요합니다.

## 도메인 연결 (선택)

직접 보유한 도메인을 쓰려면:
1. Vercel 프로젝트 → Settings → Domains
2. 도메인 입력 → 표시되는 DNS 레코드를 도메인 등록업체에 등록
3. 검증 완료 후 자동으로 SSL 인증서 발급

---

문의: 마론컨트리클럽 프론트 041-623-5500 / 예약실 041-623-5555
