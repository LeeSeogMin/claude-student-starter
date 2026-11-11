# claude-student-starter

AI 코딩 도구(**Claude Code · GitHub Copilot · OpenAI Codex**), **VS Code**, **GitHub**를 처음 쓰는 학생이
**개인과제**를 하기 위한 시작 템플릿이다. 설치 안내 문서와, 세 AI 도구가 함께 쓰는 기본 설정(하네스)이 들어 있다.

## 시작하기
1. 위쪽 초록색 **Use this template** → **Create a new repository** → 이름을 정하고 **Private** 선택 → 생성
2. [docs/01-설치.md](docs/01-설치.md)를 따라 Git·VS Code·AI 도구를 설치한다.
3. [docs/04-GitHub-과제-흐름.md](docs/04-GitHub-과제-흐름.md)를 따라 내 레포를 컴퓨터로 가져온다(clone).
4. `assignments/` 폴더에서 과제를 시작한다.

## 문서 읽는 순서
| 번호 | 문서 | 내용 |
|------|------|------|
| 01 | [설치](docs/01-설치.md) | Windows·Mac별 Git, GitHub, VS Code, Claude Code·Copilot·Codex 설치 |
| 02 | [채팅창과 VS Code의 차이](docs/02-채팅창과-VSCode-차이.md) | 웹 채팅창과 VS Code 속 AI가 할 수 있는 일 비교 |
| 03 | [VS Code에서 AI 쓰기](docs/03-VSCode-AI-사용법.md) | 채팅 창 열기, 파일 지정, 허락 창, plan 모드, 되돌리기 |
| 04 | [GitHub로 과제 관리](docs/04-GitHub-과제-흐름.md) | 템플릿 → clone → commit → push |
| 05 | [하네스·MCP·스킬](docs/05-하네스-MCP-스킬.md) | 뜻과 이 템플릿에 넣은 설정 설명 |
| 06 | [과제 활용 예시와 주의](docs/06-과제-활용-예시와-주의.md) | 보고서·코딩 과제 예시, 학업 윤리, 개인정보 |

## 폴더 구조
```
AGENTS.md              세 AI 도구가 함께 읽는 공통 규칙 (규칙은 여기만 고친다)
CLAUDE.md              Claude Code용 — AGENTS.md를 불러온다
AI-사용기록.md          AI를 어디에 썼는지 적는 표
assignments/           과제 파일
docs/                  안내 문서
.agents/skills/        공통 스킬 원본 (Codex·Copilot)
.claude/settings.json  Claude Code 권한 설정 (허용·질문·금지)
.claude/skills/        스킬 복사본 (Claude Code)
.codex/config.toml     Codex 승인·격리 설정
.vscode/settings.json  VS Code·Copilot 설정
*.example              MCP 연결 예시 (이름에서 .example을 지우면 켜짐)
```

## 주의
- 수업마다 AI 허용 범위가 다르다. 강의계획서를 먼저 확인하고, 사용 내역을 `AI-사용기록.md`에 적는다.
- 요금제·설치 방법은 2026년 11월 기준이다. 각 회사가 바꿀 수 있으므로 공식 문서를 함께 확인한다.
