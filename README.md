# GitHub 실습 저장소

## 소개

이 저장소는 오늘 강의에서 배운 **clone → commit → push**, 그리고 **branch → merge → Pull Request**의 흐름을 직접 손으로 연습해보기 위한 실습용 저장소입니다.

`unit-101.md`, `unit-102.md`, `unit-103.md` 세 개의 파일은 아파트 101호, 102호, 103호의 **등기부 등본**을 흉내 낸 문서입니다. 실제 등기부 등본이 소유권 변동(매매), 근저당권 설정 등의 이력을 순서대로 기록하듯이, 이 실습에서는 git commit으로 파일의 변경 이력을 남기고, branch와 Pull Request로 여러 사람이 동시에 작업할 때 벌어지는 일(충돌 포함)을 체험합니다.

아래 순서를 그대로 따라오시면 실습이 끝납니다. 각 단계는 **"지금 무엇을 하는지 → 실행할 명령어 → 확인할 것"** 순서로 되어 있습니다.

---

## 1단계: 내 저장소로 복제하기 (Use this template)

**지금 하는 일**: 이 저장소를 원본 그대로 두고, 내 계정(또는 소속 조직) 아래에 나만의 사본을 만듭니다.

1. 이 저장소 페이지 상단, `Code` 버튼 왼쪽에 있는 초록색 **"Use this template"** 버튼을 클릭합니다.
2. 드롭다운에서 **"Create a new repository"** 를 선택합니다.
3. Owner(소유자)를 본인 계정 또는 실습용 조직으로 선택하고, Repository name(저장소 이름)을 자유롭게 정합니다. (예: `github-course-practice`)
4. Visibility는 Public/Private 아무 것이나 선택해도 됩니다.
5. **"Create repository"** 버튼을 눌러 생성합니다.

**확인할 것**

- 새로 생성된 저장소 페이지 주소가 `내계정/내가정한이름` 형태로 되어 있는지 확인합니다. (예: `https://github.com/iamjinseok/github-course-practice`)
- `README.md`, `unit-101.md`, `unit-102.md`, `unit-103.md` 4개 파일이 그대로 보이는지 확인합니다.

---

## 2단계: 내 컴퓨터로 가져오기 (clone)

**지금 하는 일**: 방금 만든 나만의 저장소를 로컬 컴퓨터로 내려받습니다.

1. 방금 만든 저장소 페이지에서 초록색 **"Code"** 버튼을 눌러 주소(URL)를 복사합니다.
2. 터미널에서 원하는 작업 폴더로 이동한 뒤 아래 명령어를 실행합니다.

```bash
git clone <복사한 저장소 주소>
cd <저장소 이름>
```

**확인할 것**

- 아래 명령어로 폴더 안에 4개 파일(`README.md`, `unit-101.md`, `unit-102.md`, `unit-103.md`)이 있는지 확인합니다.

```bash
# macOS / Linux
ls

# Windows (PowerShell)
dir
```

---

## 3단계: 파일 수정하고 기록 남기기 (commit)

**지금 하는 일**: `unit-101.md`의 갑구(소유권 이력)에 "내가 이 집을 매매로 산다"는 내용을 한 줄 추가하고, 그 변경을 commit으로 기록합니다.

1. `unit-101.md` 파일을 에디터로 엽니다.
2. 갑구 표의 마지막 줄 아래에, 본인 이름으로 자유롭게 한 줄을 추가합니다.

```markdown
| 2 | 소유권이전 | 2026-09-11 | 매매 | (본인 이름) |
```

3. 파일을 저장한 뒤, 아래 명령어로 변경 사항을 기록합니다.

```bash
git add unit-101.md
git commit -m "101호 소유권 이전 등기 추가"
```

> **`git add`란?**: 수정한 파일을 바로 commit에 담을 수는 없습니다. `git add`는 "이번 commit에 포함시킬 변경 사항"을 미리 담아두는 대기 장소(staging area)에 파일을 올리는 명령어입니다. 등기소에 비유하면, 서류를 접수창구에 제출(add)해야 그 다음에 등기(commit)가 이루어지는 것과 같습니다. `git add` 없이 바로 `git commit`을 실행하면 "커밋할 변경 사항이 없다"는 메시지만 나오고 아무 것도 기록되지 않습니다.

> **커밋 메시지 작성 팁**: "무엇을 왜 바꿨는지"가 드러나게 씁니다. 등기부 등본에 비유하면, 등기원인(매매, 상속 등)을 적듯이 "무슨 변경인지"를 한 줄로 요약합니다.

**확인할 것**

- `git log --oneline` 명령어로 방금 만든 커밋이 목록에 보이는지 확인합니다.

---

## 4단계: 원격 저장소에 반영하기 (push)

**지금 하는 일**: 3단계에서 `unit-101.md`에 남긴 커밋을 GitHub 원격 저장소로 올립니다.

```bash
git push
```

**확인할 것**

- GitHub 웹사이트에서 내 저장소 페이지(예: `https://github.com/iamjinseok/github-course-practice`)를 새로고침하여 `unit-101.md`를 열어보고, 방금 추가한 갑구 2번째 줄이 실제로 반영되었는지 확인합니다.
- `Commits` 탭에서 방금 만든 커밋 메시지도 확인해봅니다.

---

## 5단계: branch 만들어서 작업하기

**지금 하는 일**: main 브랜치를 건드리지 않고, 별도의 작업 공간(branch)을 만들어 `unit-102.md`에 근저당권 설정 내용을 추가합니다.

> **branch 이름 규칙**: branch 이름은 영어로, 공백 없이 하이픈(`-`)으로 연결합니다. (예: `feature/my-change`, `add-mortgage`)

```bash
git checkout -b bank-a-102
```

1. `unit-102.md` 파일을 열어 을구 표에 아래처럼 근저당권 설정 내용을 한 줄 추가합니다.

```markdown
| 1 | 근저당권설정 | 2026-09-11 | 설정계약 | A은행, 채권최고액 1,000,000원 |
```

2. 변경 사항을 commit 합니다.

```bash
git add unit-102.md
git commit -m "102호 근저당권 설정 추가"
```

**확인할 것**

- `git branch` 명령어로 현재 `bank-a-102` 브랜치에 있는지(`*` 표시) 확인합니다.

---

## 6단계: Pull Request 만들어보기

**지금 하는 일**: 방금 만든 branch의 변경 사항을 main 브랜치에 합쳐달라고 요청(Pull Request)합니다. GitHub 공식 CLI 도구인 `gh` 명령어로 진행합니다.

1. 먼저 현재 branch를 원격 저장소에 push 합니다.

```bash
git push -u origin bank-a-102
```

2. Pull Request를 만듭니다. `--title`은 제목, `--body`는 설명입니다.

```bash
gh pr create --base main --head bank-a-102 --title "102호 근저당권 설정 추가" --body "102호 을구에 근저당권 설정 실습"
```

> **PR 설명(`--body`) 작성 팁**: "무엇을 바꿨는지"(102호 을구에 근저당권 설정 추가)와 "왜 바꿨는지"(실습 목적)를 간단히 적습니다.

3. 명령어를 실행하면 만들어진 PR 주소가 출력됩니다. 그 주소를 웹 브라우저로 열어 내용을 한번 확인해봅니다.
4. 문제없으면 아래 명령어로 main에 merge 합니다.

```bash
gh pr merge --merge
```

> **웹 화면으로 하고 싶다면**: GitHub 저장소 페이지로 이동하면 방금 push한 branch에 대해 **"Compare & pull request"** 버튼이 노란 배너로 나타납니다. 이 버튼을 클릭 → 제목/설명 작성 → **"Create pull request"** → **"Merge pull request"** → **"Confirm merge"** 순서로 동일하게 진행할 수 있습니다.

**확인할 것**

- main 브랜치의 `unit-102.md`를 열어 근저당권 설정 줄이 반영되었는지 확인합니다.

---

## 7단계: 충돌(conflict) 직접 만들어보기

**지금 하는 일**: 실제 협업에서는 A은행 담당자와 B은행 담당자가 각자 자기 컴퓨터에서 작업합니다. 이를 그대로 재현하기 위해, **같은 저장소를 폴더 2개에 각각 clone** 해서 "A은행"과 "B은행"인 것처럼 나눠서 작업합니다. 두 사람 모두 `unit-103.md`의 **같은 줄(을구 1행)**을 서로 다른 내용으로 고친 뒤, 먼저 반영된 쪽부터 순서대로 merge를 시도하면 어떤 일이 벌어지는지 직접 체험하고 해결합니다.

### 7-1. "두 사람"을 위한 폴더 2개 준비하기

지금 작업하던 폴더에서 한 단계 위로 나온 뒤, 같은 저장소 주소로 두 번 clone 합니다.

```bash
cd ..
git clone <내 저장소 주소> bank-a
git clone <내 저장소 주소> bank-b
```

**확인할 것**

- `bank-a`, `bank-b` 두 폴더가 각각 독립적으로 생성되었고, 둘 다 6단계에서 merge된 최신 `main` 상태(근저당권이 반영된 `unit-102.md` 포함)를 가지고 있는지 확인합니다.

### 7-2. A은행 작업 (`bank-a` 폴더)

```bash
cd bank-a
git checkout -b bank-a-103
```

`unit-103.md`의 을구 1행을 아래 내용으로 수정합니다.

```markdown
| 1 | 근저당권설정 | 2026-09-11 | 설정계약 | A은행, 채권최고액 3,000,000원 |
```

```bash
git add unit-103.md
git commit -m "103호 근저당권을 A은행 조건으로 설정"
git push -u origin bank-a-103
```

### 7-3. B은행 작업 (`bank-b` 폴더)

> 이 폴더는 A은행 작업과 전혀 무관하게, 처음 clone 받았을 때의 main 상태에서 새로 branch를 만듭니다.

```bash
cd ../bank-b
git checkout -b bank-b-103
```

`unit-103.md`의 **같은 을구 1행**을 이번엔 아래 내용으로 수정합니다.

```markdown
| 1 | 근저당권설정 | 2026-09-11 | 설정계약 | B은행, 채권최고액 2,500,000원 |
```

```bash
git add unit-103.md
git commit -m "103호 근저당권을 B은행 조건으로 설정"
git push -u origin bank-b-103
```

**확인할 것**

- `git log --oneline -1`을 `bank-a`, `bank-b` 양쪽에서 각각 실행해, 서로 다른 커밋 메시지가 남아있는지 확인합니다.

### 7-4. 첫 번째 PR(A은행) 먼저 merge 하기

`bank-a` 폴더 안에서 아래 명령어로 PR을 만들고 merge 합니다.

```bash
gh pr create --base main --head bank-a-103 --title "103호 근저당권을 A은행 조건으로 설정" --body "103호 을구 근저당권 설정 실습 (A은행)"
gh pr merge --merge
```

> **웹 화면으로 하고 싶다면**: `bank-a` 폴더에서 push까지 마친 뒤 GitHub 웹으로 이동해 `bank-a-103` → `main` Pull Request를 만들고 merge 합니다. (6단계와 동일한 방법)

이 PR은 문제없이 merge됩니다.

### 7-5. 두 번째 PR(B은행)에서 conflict 확인하기

이어서 `bank-b` 폴더 안에서 아래 명령어로 PR을 만들어봅니다. (conflict가 있어도 PR 생성 자체는 가능합니다.)

```bash
gh pr create --base main --head bank-b-103 --title "103호 근저당권을 B은행 조건으로 설정" --body "103호 을구 근저당권 설정 실습 (B은행)"
```

이 상태에서 `gh pr merge`를 시도하면 conflict 때문에 merge가 거부되는 것을 명령줄에서 확인할 수 있습니다.

> **웹 화면으로 하고 싶다면**: `bank-b-103` → `main` Pull Request를 GitHub 웹에서 만들면, **"This branch has conflicts that must be resolved"** 라는 빨간 경고를 확인할 수 있습니다.

이것이 바로 conflict입니다. 같은 파일의 같은 줄을 두 사람(A은행, B은행)이 서로 다르게 고쳤기 때문에, git이 어느 쪽을 반영해야 할지 스스로 판단하지 못하는 상태입니다.

### 7-6. B은행 폴더에서 conflict 해결하기

B은행 입장에서, 자기 branch를 main의 최신 상태(A은행 내용이 이미 반영된 상태)와 합쳐봅니다.

```bash
cd bank-b
git pull origin main
```

이 명령을 실행하면 `unit-103.md`에 아래와 같은 conflict 표시가 나타납니다.

```
<<<<<<< HEAD
| 1 | 근저당권설정 | 2026-09-11 | 설정계약 | B은행, 채권최고액 2,500,000원 |
=======
| 1 | 근저당권설정 | 2026-09-11 | 설정계약 | A은행, 채권최고액 3,000,000원 |
>>>>>>> main
```

- `<<<<<<< HEAD` 부터 `=======` 까지: 지금 이 컴퓨터(B은행)의 내용
- `=======` 부터 `>>>>>>> main` 까지: main에 이미 merge된 내용(A은행)

**해결 방법**: 두 내용 중 하나를 선택하거나, 둘 다 살리는 방식(예: 순위를 1, 2로 나눠 둘 다 남기기)으로 직접 파일을 수정하고, `<<<<<<<`, `=======`, `>>>>>>>` 표시는 모두 지웁니다. 예를 들어 두 근저당권을 순위만 나눠 모두 남기려면:

```markdown
| 1 | 근저당권설정 | 2026-09-11 | 설정계약 | A은행, 채권최고액 3,000,000원 |
| 2 | 근저당권설정 | 2026-09-11 | 설정계약 | B은행, 채권최고액 2,500,000원 |
```

수정이 끝나면 아래처럼 마무리합니다.

```bash
git add unit-103.md
git commit -m "conflict 해결: A은행, B은행 근저당권 모두 반영"
git push
```

**확인할 것**

- 다시 GitHub의 해당 Pull Request 페이지(예: `https://github.com/iamjinseok/github-course-practice/pull/2`)로 가보면 conflict 경고가 사라지고 merge할 수 있는 상태로 바뀌어 있습니다.
- 이제 **"Merge pull request"** 로 마무리합니다. (명령어로는 `bank-b` 폴더에서 `gh pr merge --merge`)

---

## 막히면

- 오늘 강의에서 배포된 강의자료를 다시 참고해보세요.
- 실습 중 파일이 꼬이거나 되돌리기 어려운 상태가 되어도 괜찮습니다. 이 저장소는 언제든 다시 **"Use this template"** 버튼으로 처음부터 새로 시작할 수 있습니다.
