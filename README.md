# GGM-Network `.github` 저장소

이 저장소는 코드가 아니라 **조직의 "얼굴"** 을 관리합니다. GitHub 조직 프로필 페이지([github.com/GGM-Network](https://github.com/GGM-Network))에 표시되는 내용을 담고 있습니다.

이 문서는 **프로필 README를 어떤 방식으로 만들었고, 무엇이 들어갔으며, 나중에 어떻게 업데이트하는지**를 정리한 유지보수 가이드입니다.

---

## 1. 핵심 동작 — 프로필 페이지는 어떻게 렌더링되나

- 조직 프로필 페이지에 보이는 본문은 **이 저장소의 [`profile/README.md`](profile/README.md)** 파일이다.
- 이 `.github` 저장소가 **public** 일 때만 프로필 페이지에 렌더링된다. (코드 저장소 4개 — Client / Admin / Server / Discord — 는 private 유지)
- `profile/README.md` 를 수정해서 `main` 에 커밋하면 프로필 페이지가 **즉시** 갱신된다.
- 저장소 루트의 이 `README.md`(지금 읽고 있는 파일)는 프로필 페이지에는 나오지 않고, `.github` 저장소를 직접 열었을 때만 보인다.

| 파일 | 역할 |
|------|------|
| `profile/README.md` | 조직 프로필 페이지에 렌더링되는 공개 본문 |
| `README.md` (루트, 이 파일) | 유지보수자용 가이드 (프로필 페이지에는 안 보임) |

> 개발 PC에는 같은 `profile/README.md` 사본이 프로젝트 폴더 아래 `.github/profile/README.md` 로도 보관되어 있다.

---

## 2. 어떤 방식으로 제작했나

프로필 README는 즉흥 작성이 아니라 **검증 → 다안 설계 → 심사 → 합성** 단계를 거쳐 만들었다 (Claude Code 멀티 에이전트 워크플로 활용). 업데이트할 때도 같은 원칙을 따르면 품질이 유지된다.

1. **검증(Research)** — 추측을 배제하기 위해 실제 소스에서 사실만 수집했다.
   - 4개 패키지의 `package.json`(client / admin / server / discord)에서 **정확한 의존성 버전**을 추출 → 배지 버전의 근거.
   - `client/src/app` 디렉터리를 훑어 **실제로 존재하는 라우트**만 확인 → 없는 기능/라우트는 홍보하지 않음.
2. **다안 설계(Draft)** — 서로 다른 3가지 스타일(엘레강트 미니멀 / 대시보드 / 스토리텔링)로 README 초안을 각각 작성.
3. **심사(Judge)** — 정확성 · 시각 · 한국어 톤 · 완성도 · **공개 안전(민감정보 누출 여부)** 5축으로 채점. 스토리텔링형이 최고점.
4. **합성(Synthesize)** — 우승안을 토대로 대시보드형의 표 · mermaid 다이어그램을 합쳐 최종본 완성.

마지막에 **게시 전 검증**을 한 번 더 했다: 배지 버전이 실제 `package.json` 과 일치하는지, 광고한 라우트가 모두 실재하는지, 운영 민감정보(도메인 디테일 · 포트 · env 이름 · 비밀번호 · 내부 경로)가 새지 않았는지.

---

## 3. 무엇이 들어갔나 — 섹션 구조와 출처

`profile/README.md` 는 아래 순서로 구성된다. 각 섹션을 수정할 때 **"근거(Source of truth)"** 열을 함께 확인해야 사실과 어긋나지 않는다.

| 섹션 | 내용 | 근거(Source of truth) |
|------|------|------------------------|
| 헤더 + 배지 | 제품명, 태그라인, 스택/상태 shields 배지 | 각 패키지 `package.json` 의 버전 |
| 우리가 이걸 만든 이유 | 마이스터 졸업생의 커리어 리듬에 맞춘 내러티브 인트로 | 제품 방향(휴면 회원 비차단 정책 등) |
| 무엇을 제공하나 | 공개/회원 경계 + 도메인 한눈에 보기 표 + 기능 그룹(발견·커뮤니티·커리어·회원·인증·Discord) | `client/src/app` 라우트 + 제품 정책 |
| 접근 권한 모델 | 비회원 / `PENDING` / `APPROVED` 단계별 기능 표 | 서버 접근 정책 (클라이언트는 서버 응답·잠금 사유를 따름) |
| 아키텍처 | 4-앱 mermaid 다이어그램 + 역할/스택 표 + 설계 메모(이중 토큰·outbox·권한 게이트) | 모노레포 4앱 구조 |
| 기술 스택 | 프런트/백엔드 정확한 버전 표 | 각 패키지 `package.json` |
| 참여하기 + 저장소 | 동문/기여자 안내 + 코드 저장소 4개 링크 | 조직 저장소 목록 |

**동기화 주의 항목**
- 헤더의 `feature_domains-NN` 배지 숫자는 "16개 기능 도메인 상세" 표의 **행 수와 일치**시킨다.
- 기술 스택 표와 헤더 배지의 버전은 항상 같은 값으로 맞춘다.
- 새 기능/라우트를 추가하면 "도메인 한눈에 보기", "상세 도메인 표", "접근 권한 모델"을 함께 갱신한다.

---

## 4. 업데이트하는 법

### 방법 A — GitHub 웹에서 바로 편집 (가장 쉬움)

1. [`profile/README.md`](profile/README.md) 를 연다.
2. 오른쪽 위 연필(✏️) 아이콘 → 편집.
3. 아래로 내려 **Commit changes** 로 `main` 에 바로 커밋.
4. [github.com/GGM-Network](https://github.com/GGM-Network) 새로고침 → 반영 확인.

### 방법 B — `gh` CLI로 로컬 편집 후 재게시

로컬 사본(`profile/README.md`)을 수정한 뒤, 기존 파일을 갱신하려면 **현재 `sha` 가 필요**하다 (Windows PowerShell 기준).

```powershell
$path = "C:\GGM_Network\.github\profile\README.md"   # 로컬 사본 경로
$sha  = gh api repos/GGM-Network/.github/contents/profile/README.md --jq .sha
$b64  = [Convert]::ToBase64String([IO.File]::ReadAllBytes($path))
@{ message = "docs : 조직 프로필 README 업데이트"; content = $b64; sha = $sha; branch = "main" } |
  ConvertTo-Json -Compress |
  gh api --method PUT repos/GGM-Network/.github/contents/profile/README.md --input -
```

> `sha` 없이 PUT 하면 "이미 존재함" 오류가 난다. 새 파일을 만들 때만 `sha` 를 생략한다.

### 조직 프로필 텍스트 필드(소개·웹사이트·위치·이메일) 변경

프로필 페이지 사이드바에 표시되는 값이다. **`admin:org` scope** 가 있는 토큰 + 조직 owner 권한이 필요하다.

```powershell
gh api --method PATCH orgs/GGM-Network `
  -f name="GGM Network" `
  -f description="..." `
  -f blog="https://ggm.leaderpark.net" `
  -f location="대한민국 경기" `
  -f email="..."
```

scope가 없으면 먼저: `gh auth refresh -h github.com -s admin:org`

**현재 적용된 값**

| 필드 | 값 |
|------|-----|
| 표시 이름(name) | GGM Network |
| 소개(description) | 경기게임마이스터고 동문 네트워크 — 게임·IT를 배운 동문이 작품·커리어·모임으로 다시 연결되는 커뮤니티 플랫폼 |
| 위치(location) | 대한민국 경기 |
| 웹사이트(blog) | https://ggm.leaderpark.net |
| 공개 이메일(email) | dkdleldjqkr976@gmail.com |

---

## 5. 갱신 시 체크리스트

- [ ] **공개 안전** — `profile/README.md` 는 누구나 본다. 운영 도메인 디테일·포트 번호·env 이름·비밀번호/토큰·DB 연결값·내부 인프라 경로를 본문에 넣지 않는다. (단, 조직 프로필 **website 필드**의 공개 사이트 URL은 의도적으로 노출하기로 한 값이다.)
- [ ] **버전 동기화** — 배지/스택 표의 버전을 실제 `package.json` 과 맞춘다.
- [ ] **라우트 실재 확인** — 새로 홍보하는 라우트가 `client/src/app` 에 실제로 존재하는지 확인한다.
- [ ] **도메인 카운트** — `feature_domains-NN` 배지와 상세 표 행 수를 일치시킨다.
- [ ] **제품 톤 유지** — 공개/회원 권한 경계, 이중 토큰 정책(라이트 `paper-panel` / 다크 `dev-panel`) 등 제품 원칙과 모순되지 않게 쓴다.
- [ ] **렌더 확인** — 커밋 후 [github.com/GGM-Network](https://github.com/GGM-Network) 에서 mermaid 다이어그램·표·배지가 깨지지 않는지 본다.

---

## 6. API로는 안 되는 것 (웹 UI 전용)

- **조직 로고(아바타) 이미지** — REST API 미지원. `Settings → General → Profile picture → Upload a photo`
  (또는 https://github.com/organizations/GGM-Network/settings/profile)
- 여러 개의 소셜 링크, 인증 도메인(verified domain), 프로필 핀 고정 — 사실상 웹 UI에서 관리한다.

---

<sub>이 문서는 조직 프로필 유지보수용 내부 가이드입니다. 프로필 페이지 본문은 <a href="profile/README.md"><code>profile/README.md</code></a> 입니다.</sub>
