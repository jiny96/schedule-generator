# 스케줄 자동 생성기 — 배포 가이드

URL을 아는 팀원 누구나 사용할 수 있는 공유 웹 페이지입니다.

---

## 파일 구성

```
index.html   ← 실제 페이지 (수정 불필요)
config.js    ← ★ 여기만 설정하면 됩니다
README.md    ← 이 파일
```

---

## 배포 순서 (총 10분)

### Step 1 — GitHub Gist 만들기 (공유 DB 역할)

1. https://gist.github.com 접속 (GitHub 로그인 필요)
2. **Filename** 칸에 `schedule_data.json` 입력
3. 내용에 아래 JSON 붙여넣기:
   ```json
   {
     "srl": {
       "tournament": { "last": null, "updatedAt": null },
       "regular":    { "last": null, "updatedAt": null }
     },
     "templates": []
   }
   ```
4. **Create secret gist** 클릭
5. 브라우저 URL에서 Gist ID 복사  
   예: `https://gist.github.com/username/abc123def456` → `abc123def456`

---

### Step 2 — GitHub Token 만들기 (쓰기 권한)

1. https://github.com/settings/tokens 접속
2. **Generate new token (classic)** 클릭
3. Note: `schedule-generator` (임의 입력)
4. Expiration: **No expiration** 또는 원하는 기간
5. 체크박스: **gist** 만 체크 ✓
6. **Generate token** → 생성된 `ghp_xxx...` 값 복사 (다시 볼 수 없음!)

---

### Step 3 — config.js 수정

`config.js` 파일을 열어 두 값을 채웁니다:

```js
window.SCHEDULE_CONFIG = {
  GIST_ID:  'abc123def456',          // Step 1에서 복사한 Gist ID
  GH_TOKEN: 'ghp_xxxxxxxxxxxx',      // Step 2에서 복사한 Token
};
```

---

### Step 4 — GitHub Repository 만들기

1. https://github.com/new 접속
2. Repository name: `schedule-generator` (원하는 이름)
3. **Public** 선택 (GitHub Pages 무료 사용)
4. **Create repository** 클릭
5. `index.html`, `config.js`, `README.md` 세 파일 업로드

---

### Step 5 — GitHub Pages 활성화

1. Repository → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / `/ (root)` 선택 → **Save**
4. 1~2분 후 URL 생성됨:  
   `https://[username].github.io/schedule-generator/`

---

## 완성!

생성된 URL을 팀원들과 공유하면 됩니다.  
모든 팀원이 동일한 SRL 현황과 템플릿을 공유합니다.

---

## 주요 기능

| 기능 | 설명 |
|------|------|
| SRL 현황 바 | 대회/정기 마지막 SRL + 다음 SRL 실시간 표시 |
| SRL 자동 기록 | 미리보기 생성 시 마지막 SRL을 Gist에 자동 저장 |
| 공유 템플릿 | 정기 스케줄 TnmtId 목록을 팀 공유 저장/불러오기 |
| 이어 붙이기 | 기존 엑셀 업로드 후 신규 행만 추가해 다운로드 |
| 정기 날짜 필터 | 시작/종료 날짜+시간 기준으로 템플릿 자동 필터링 |

---

## 보안 참고

- `config.js`에 토큰이 포함되므로 Repository는 **Public**이어도 토큰이 노출됩니다.  
  팀 내부 전용이라면 문제없지만, 외부 공개가 우려되면 Repository를 **Private**으로 설정하고 GitHub Pages는 유료 플랜이 필요합니다.  
- 토큰은 `gist` scope만 있어 다른 GitHub 데이터에는 접근할 수 없습니다.
- 더 안전하게 운영하려면 Gist 대신 Supabase(무료) 전환을 권장합니다.
