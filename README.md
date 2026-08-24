# livehermoment.com — 배포 가이드

폴더 안 파일 전부(`index.html`, `CNAME`, 로고·파비콘 png, `robots.txt`, `sitemap.xml`)를 그대로 올리면 됩니다. 서버도, 빌드도 필요 없어요.

---

## 1단계 — 미리 보기 (맥북에서)

`index.html`을 더블클릭하면 크롬에서 바로 열립니다. 여기서 먼저 확인하세요.

## 2단계 — GitHub에 올리기

1. github.com → 우측 상단 `+` → **New repository**
2. Repository name: `livehermoment` / **Public** 선택 / 나머지는 그대로 → **Create repository**
3. 다음 화면에서 **uploading an existing file** 링크 클릭
4. 이 폴더의 **파일 7개를 전부 드래그**해서 올림 (폴더째로 말고 파일만)
5. 아래 **Commit changes** 버튼 클릭

## 3단계 — GitHub Pages 켜기

1. 저장소 상단 **Settings** → 왼쪽 메뉴 **Pages**
2. Source: **Deploy from a branch**, Branch: **main** / **/(root)** → **Save**
3. 1~2분 뒤 새로고침하면 주소가 뜹니다. `CNAME` 파일 덕분에 Custom domain 칸에 `livehermoment.com`이 자동으로 채워져 있을 거예요. (비어 있으면 직접 입력 후 Save)

## 4단계 — 가비아에서 도메인 연결

가비아 → My가비아 → 도메인 → `livehermoment.com` → **DNS 정보 → DNS 관리**

아래 레코드를 **추가**합니다.

| 타입 | 호스트 | 값 | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | 3600 |
| A | @ | 185.199.109.153 | 3600 |
| A | @ | 185.199.110.153 | 3600 |
| A | @ | 185.199.111.153 | 3600 |
| CNAME | www | `본인깃허브아이디.github.io.` | 3600 |

> ⚠️ **MX 레코드는 절대 건드리지 마세요.** 네이버웍스 메일(kate@livehermoment.com)이 그 레코드로 돌아갑니다. A/CNAME만 추가하면 메일에는 영향이 없습니다.

DNS 반영은 보통 10분~1시간, 길면 하루까지 걸립니다.

## 5단계 — HTTPS 켜기

DNS가 반영되면 Settings → Pages에 **Enforce HTTPS** 체크박스가 활성화됩니다. 체크하면 자물쇠(https://) 완료. (체크박스가 회색이면 아직 DNS 반영 전이니 조금 기다렸다 다시 오세요.)

---

## 나중에 내용 수정하려면

`index.html` 하나만 고치면 됩니다. 텍스트는 이런 형태로 들어 있어요.

```html
<h3 data-ko="퍼포먼스 마케팅" data-en="Performance marketing">퍼포먼스 마케팅</h3>
```

- `data-ko` = 한국어 버전, `data-en` = 영어 버전 (우측 상단 EN 버튼으로 전환)
- **태그 사이의 글자와 `data-ko` 값, 두 군데를 똑같이 고쳐야 합니다**
- 줄바꿈은 `|` 기호로 넣습니다 (예: `data-ko="첫 줄|둘째 줄"`)

마켓(시계) 목록은 `<script>` 안 `MARKETS` 배열에서 추가·삭제할 수 있습니다.

수정한 `index.html`은 GitHub 저장소에서 파일 클릭 → 연필 아이콘 → 수정 → Commit 하면 1분 안에 사이트에 반영됩니다.

---

## 파일 설명

| 파일 | 역할 |
|---|---|
| `index.html` | 사이트 전체 (내용·디자인·기능 전부 여기에) |
| `CNAME` | GitHub에 "이 사이트 주소는 livehermoment.com" 이라고 알려주는 파일 |
| `logo-wide.png` / `logo-square.png` | 배경 투명 처리한 로고 |
| `favicon.png` / `apple-touch-icon.png` | 브라우저 탭·홈화면 아이콘 |
| `robots.txt` / `sitemap.xml` | 구글 검색 노출용 |
