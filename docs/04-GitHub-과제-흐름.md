# 04. GitHub로 과제 관리하기

## 용어 세 개
- **Git**: 내 컴퓨터에서 파일의 변경 이력을 저장하는 프로그램이다. "언제 무엇을 바꿨는지"를 기록한다.
- **GitHub**: Git 기록을 인터넷에 올려 두는 웹사이트다. 컴퓨터가 고장 나도 과제가 남는다.
- **레포(repository, 저장소)**: 과제 폴더 하나를 GitHub에 올린 단위다.

| 동작 | 뜻 | 비유 |
|------|----|------|
| commit (커밋) | 지금 상태를 이력에 한 번 저장 | 게임의 세이브 |
| push (푸시) | 내 컴퓨터의 커밋을 GitHub에 올림 | 세이브 파일을 클라우드에 업로드 |
| pull (풀) | GitHub의 최신 상태를 내 컴퓨터로 받음 | 클라우드 세이브를 내려받기 |
| clone (클론) | GitHub 레포를 내 컴퓨터에 처음 복사 | 처음 한 번 내려받기 |

## 1단계 — 이 템플릿으로 내 레포 만들기 (처음 한 번)
1. https://github.com/LeeSeogMin/claude-student-starter 에 접속한다.
2. 초록색 **Use this template** 버튼 → **Create a new repository**를 누른다.
3. Repository name에 예: `2026-1-과목명-과제`를 적는다.
4. **Private**(비공개)을 고른다. 과제는 다른 학생이 베끼지 못하게 비공개로 둔다.
5. **Create repository**를 누른다.

## 2단계 — 내 컴퓨터로 가져오기 (clone)
**VS Code 화면으로**
1. VS Code를 열고 `Ctrl+Shift+P`(Mac: `Cmd+Shift+P`) → `Git: Clone` 입력.
2. **Clone from GitHub** → GitHub 로그인 창이 뜨면 허용한다.
3. 1단계에서 만든 레포를 고르고, 저장할 폴더(예: `문서/과제`)를 고른다.
4. "Open" 을 눌러 폴더를 연다.

**터미널 명령으로** (같은 결과)
```bash
git clone https://github.com/내아이디/2026-1-과목명-과제.git
cd 2026-1-과목명-과제
code .
```

## 3단계 — 과제하고 저장하기 (매번 반복)
1. `assignments/` 안에서 과제 파일을 만들고 고친다. Claude에게 도움을 받아도 된다.
2. 왼쪽 막대의 **소스 제어** 아이콘(가지 모양)을 누른다. 바뀐 파일 목록이 보인다.
3. 위쪽 메시지 칸에 무엇을 했는지 적는다. 예: `1주차 보고서 서론 작성`
4. **Commit** 버튼을 누른다. ("변경 내용을 스테이징할까요?" 창이 뜨면 **Yes**/**Always**)
5. **Sync Changes**(또는 Push) 버튼을 눌러 GitHub에 올린다.

**터미널 명령으로**
```bash
git add .
git commit -m "1주차 보고서 서론 작성"
git push
```

**Claude에게 맡기기**: Claude 창에 "지금까지 바꾼 내용을 커밋해 줘"라고 쓰면 Claude가 메시지를 만들어 커밋한다.
이 레포 설정상 커밋·푸시 전에는 **반드시 허락 창이 뜬다**(05번 문서의 권한 설정).

## 4단계 — 다른 컴퓨터에서 이어서 하기
학교 컴퓨터에서 작업했다면 집에서 VS Code를 열고 **Sync Changes**(또는 `git pull`)를 먼저 누른다.

## 자주 나는 오류
| 메시지 | 원인 | 해결 |
|--------|------|------|
| `Please tell me who you are` | Git에 내 이름·이메일을 등록하지 않았다 | 01번 문서의 `git config` 두 줄을 실행한다 |
| `rejected ... fetch first` | GitHub에 내 컴퓨터에 없는 커밋이 있다 | 먼저 Sync(pull)한 뒤 다시 push 한다 |
| `Authentication failed` | GitHub 로그인이 풀렸다 | VS Code 왼쪽 아래 계정 아이콘에서 GitHub 다시 로그인 |

## 확인 체크
- [ ] 내 GitHub에 Private 레포가 생겼다.
- [ ] 파일 하나를 고쳐 commit·push 했고, GitHub 웹페이지에서 바뀐 내용이 보인다.
