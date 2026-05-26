[README.md](https://github.com/user-attachments/files/28253139/README.md)
# 스케줄 자동 생성기 — 배포 가이드 (Google Sheets 버전)

토큰 불필요! Google Sheets + Apps Script로 안전하게 운영합니다.

---

## 파일 구성

```
index.html   ← 실제 페이지 (수정 불필요)
config.js    ← Apps Script URL 한 줄만 입력
Code.gs      ← Google Apps Script에 붙여넣는 코드
README.md    ← 이 파일
```

---

## 배포 순서

### Step 1 — Google Sheets 만들기

1. https://sheets.google.com 에서 새 스프레드시트 생성
2. 이름: `스케줄 생성기 DB` (임의)
3. 그냥 빈 채로 두면 됩니다 (시트는 앱스크립트가 자동 생성)

---

### Step 2 — Apps Script 설정

1. 스프레드시트 상단 메뉴: **확장 프로그램 → Apps Script**
2. 기본으로 있는 코드 전체 삭제
3. `Code.gs` 파일 내용을 전체 복사해서 붙여넣기
4. 💾 저장 (Ctrl+S)

---

### Step 3 — 웹앱으로 배포

1. 우측 상단 **배포 → 새 배포** 클릭
2. 유형 선택: **웹 앱**
3. 설정:
   - 설명: `schedule-generator`
   - 다음 사용자로 실행: **나**
   - 액세스 권한: **모든 사용자(익명 포함)**
4. **배포** 클릭
5. 권한 요청 팝업 → **액세스 허용**
6. 생성된 URL 복사  
   형식: `https://script.google.com/macros/s/XXXXXX/exec`

---

### Step 4 — config.js 수정

```js
window.SCHEDULE_CONFIG = {
  APPS_SCRIPT_URL: 'https://script.google.com/macros/s/XXXXXX/exec',
};
```

---

### Step 5 — GitHub에 업로드

1. GitHub 저장소에서 기존 `config.js` 클릭 → 연필 아이콘 → 수정 → Commit
2. `index.html`도 새 파일로 교체 (Add file → Upload files)
3. 1~2분 후 페이지 새로고침

---

## 완성!

`https://[username].github.io/schedule-generator/`

Google Sheets에 자동으로 **SRL현황**, **템플릿** 두 시트가 생기고  
모든 팀원이 동일한 데이터를 공유합니다.

---

## 주요 기능

| 기능 | 설명 |
|------|------|
| SRL 현황 바 | 대회/정기 마지막·다음 SRL 실시간 표시 |
| SRL 자동 기록 | 미리보기 생성 시 Google Sheets에 자동 저장 |
| 공유 템플릿 | 정기 TnmtId 목록 팀 공유 저장/불러오기/삭제 |
| 이어 붙이기 | 기존 엑셀에 신규 행만 추가 |
| 정기 날짜 필터 | 시작/종료 날짜+시간 기준 자동 필터링 |
