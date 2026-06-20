# 하루관리 앱 - PWA 배포 가이드

## 파일 구성
```
daily-life-app/
├── index.html      ← 앱 전체 코드 (이것만 있어도 작동)
├── manifest.json   ← PWA 설정 (앱 이름, 아이콘 등)
├── sw.js           ← 서비스워커 (오프라인 지원)
├── icon-192.png    ← 앱 아이콘 (직접 추가 필요)
├── icon-512.png    ← 앱 아이콘 (직접 추가 필요)
└── README.md       ← 이 파일
```

## 아이콘 만들기
icon-192.png, icon-512.png 파일이 필요합니다.
- https://favicon.io 에서 텍스트로 아이콘 생성 가능
- 또는 원하는 이미지를 192x192, 512x512 크기로 저장

## GitHub 업로드 방법

### 방법 A: 웹에서 직접 (가장 쉬움)
1. https://github.com 로그인 후 [New repository] 클릭
2. Repository name: `daily-life-app` 입력
3. Public 선택 → [Create repository]
4. [uploading an existing file] 클릭
5. 파일 4개(index.html, manifest.json, sw.js, icon 2개) 드래그&드롭
6. [Commit changes] 클릭

### 방법 B: Git 사용
```bash
git clone https://github.com/내아이디/daily-life-app.git
# 파일 복사 후
git add .
git commit -m "첫 배포"
git push
```

## Vercel 배포 (무료)

1. https://vercel.com 접속 → GitHub으로 로그인
2. [Add New Project] → GitHub 저장소 선택
3. [Deploy] 클릭 → 1분 후 완료
4. `https://daily-life-app-내아이디.vercel.app` 주소 생성됨

## 갤럭시 홈 화면에 추가

1. 갤럭시에서 위 Vercel 주소 열기
2. **삼성 인터넷**: 메뉴(≡) → [페이지 추가] → [홈 화면]
3. **크롬**: 메뉴(⋮) → [홈 화면에 추가]
4. 홈 화면에 앱 아이콘이 생기고 전체화면으로 실행됩니다!

## 서비스워커 등록 (index.html에 이미 포함)
index.html 맨 아래 `</body>` 직전에 아래 코드를 추가하세요:

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
  }
</script>
```

## 주요 기능
- ✅ 루틴 관리 (요일별, 체크, 편집, 삭제)
- 📅 일정 관리 (특별/반복 일정)
- 📣 모집 공고 (기관별 추가·삭제, 마감일 표시)
- 💰 가계부 (수입/지출, 메모, 삭제)
- 📝 메모·일기 (날짜별 기록)
- 🤖 AI 생활 코치 (Claude API 연동)
- 🌤 실시간 날씨 (서울 기준)
- 🌙 음력 날짜 표시
- 💾 데이터 자동 저장 (localStorage)
- 📱 모바일 최적화 PWA

## 데이터 저장
모든 데이터는 기기의 localStorage에 저장됩니다.
브라우저 데이터를 삭제하면 초기화되니 주의하세요.
