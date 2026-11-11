# 05. 하네스·MCP·스킬이란

## 세 낱말의 뜻
- **하네스(harness)**: AI 모델 자체가 아니라, 모델을 감싸고 **무엇을 읽고·무엇을 할 수 있고·무엇을 물어봐야 하는지** 정하는 설정 묶음이다.
  같은 Claude 모델이라도 하네스 설정에 따라 파일을 지울 수도, 못 지울 수도 있다. 이 템플릿의 하네스는 네 가지로 이루어진다.
  1. **규칙 파일** — AI가 매번 읽는 지시문 (`AGENTS.md`, `CLAUDE.md`)
  2. **권한 설정** — 허용·질문·금지할 동작 목록 (`.claude/settings.json`, `.codex/config.toml`)
  3. **스킬** — 자주 하는 작업의 절차서 (`.agents/skills/`, `.claude/skills/`)
  4. **MCP** — 외부 도구 연결 (예시 파일만 넣음)
- **스킬(skill)**: `SKILL.md` 파일 하나에 "이 작업은 이 순서로 한다"를 적어 둔 절차서다. `/스킬이름`으로 부르거나, AI가 요청 내용을 보고 스스로 꺼내 쓴다.
- **MCP(Model Context Protocol)**: AI가 바깥 프로그램·웹 서비스(최신 문서 검색, 데이터베이스, 노션 등)를 쓸 수 있게 해 주는 연결 규격이다. USB 규격이 같으면 어느 컴퓨터에나 꽂히듯, MCP 서버 하나를 Claude·Copilot·Codex가 함께 쓸 수 있다. 다만 **등록하는 설정 파일의 형식은 도구마다 다르다.**

## 도구별로 읽는 파일 (이 템플릿 기준)

| 구분 | Claude Code | GitHub Copilot | OpenAI Codex |
|------|-------------|----------------|--------------|
| 규칙 파일 | `CLAUDE.md` → 안의 `@AGENTS.md` 줄로 `AGENTS.md`를 불러옴 | `AGENTS.md` (`CLAUDE.md`도 읽음) | `AGENTS.md` |
| 권한 설정 | `.claude/settings.json` | VS Code 기본값(명령 실행 때마다 물음) | `.codex/config.toml` (폴더를 신뢰해야 적용) |
| 스킬 위치 | `.claude/skills/` (복사본) | `.agents/skills/`, `.claude/skills/` | `.agents/skills/` (원본) |
| MCP 파일 | `.mcp.json` (키 `mcpServers`) | `.vscode/mcp.json` (키 `servers`) | `.codex/config.toml`의 `[mcp_servers.이름]` |

**규칙을 바꾸려면 `AGENTS.md` 하나만 고친다.** 세 도구 모두 결국 이 파일을 읽는다.
**스킬을 바꾸려면 `.agents/skills/`와 `.claude/skills/` 두 곳을 같이 고친다.** Claude Code가 `.agents/skills/`를 읽지 않아서 복사본을 둔다.

## 이 템플릿에 넣은 권한 설정
**Claude Code (`.claude/settings.json`)** — AI는 금지 → 질문 → 허용 순서로 규칙을 맞춰 본다.

| 구분 | 동작 | 이유 |
|------|------|------|
| 허용 (묻지 않음) | `git status`, `git diff`, `git log`, `git branch` | 읽기만 하므로 안전 |
| 질문 (매번 허락 창) | `git commit`, `git push`, `git reset`, `pip install`, `npm install` | 기록·인터넷·컴퓨터에 영향을 줌 |
| 금지 | `.env`·`secrets/` 읽기, `rm -rf`, `sudo`, 강제 푸시 | 비밀 유출·파일 삭제 방지 |

> 주의: 금지 규칙은 명령어 **글자**가 맞을 때만 막는다. 다른 방식으로 쓴 같은 명령은 못 막을 수 있으므로, 허락 창을 읽는 습관이 가장 확실한 안전장치다.

내 컴퓨터에서만 규칙을 바꾸고 싶으면 `.claude/settings.local.json`을 만든다. 이 파일은 GitHub에 올라가지 않는다(`.gitignore`).

**Codex (`.codex/config.toml`)**
- `approval_policy = "on-request"` — 필요할 때 학생에게 묻는다.
- `sandbox_mode = "workspace-write"` — 과제 폴더 안에서만 파일을 쓴다.

**Copilot (`.vscode/settings.json`)** — `AGENTS.md`와 스킬을 읽는 설정을 켜 두었다. 명령 자동 허용은 넣지 않았으므로 실행할 때마다 묻는다.

## 이 템플릿에 넣은 스킬
| 스킬 | 부르는 법 | 하는 일 |
|------|----------|---------|
| assignment-check | `/assignment-check` | 제출 전 요구사항·출처·개인정보·AI 사용 기록을 표로 점검 (파일은 안 고침) |
| explain-code | `/explain-code` | 코드·개념을 한 문장 요약 → 줄 설명 → 실제 값 따라가기 → 확인 질문 순서로 설명 |

**내 스킬 만들기**: `.agents/skills/내스킬/SKILL.md`를 만들고 아래처럼 쓴 뒤, 같은 폴더를 `.claude/skills/`에도 복사한다.
```markdown
---
name: my-summary
description: 읽기 자료를 A4 반쪽으로 요약한다. "요약해 줘" 요청에 쓴다.
---
1. 핵심 주장 3개를 뽑는다.
2. 주장마다 근거 문장을 원문에서 인용한다.
```

## MCP 켜기 (선택)
예시로 Context7(프로그래밍 라이브러리의 최신 문서를 찾아 주는 서버)을 넣어 두었다. 쓰려면:
- Claude Code: `.mcp.json.example` 파일 이름을 `.mcp.json`으로 바꾼다. 처음 쓸 때 승인 창이 뜬다.
- Copilot: `.vscode/mcp.json.example` → `.vscode/mcp.json`
- Codex: `.codex/config.toml` 맨 아래 두 줄의 `#`을 지운다.

MCP 서버는 내 파일·계정에 접근할 수 있으므로 **출처를 모르는 서버는 등록하지 않는다.** 등록한 `.mcp.json`은 `.gitignore`에 들어 있어 GitHub에 올라가지 않는다.

## 훅(hook) — 넣지 않았다
훅은 "파일을 저장할 때마다 이 명령을 자동 실행" 같은 자동 동작이다. 명령이 Windows와 Mac에서 다르게 동작해 오류가 나기 쉬우므로 이 템플릿에는 넣지 않았다. 익숙해진 뒤 Claude Code 문서 https://code.claude.com/docs/en/hooks-guide 를 보고 추가한다.

## 확인 체크
- [ ] `AGENTS.md`에 규칙 한 줄(예: "답 끝에 요약 한 줄을 붙인다")을 넣고, AI가 따르는지 확인했다.
- [ ] `/explain-code`를 한 번 실행했다.

출처: https://code.claude.com/docs/en/permissions · https://code.claude.com/docs/en/skills · https://code.claude.com/docs/en/mcp ·
https://code.visualstudio.com/docs/copilot/customization/agent-skills · https://learn.chatgpt.com/docs/agent-configuration/agents-md ·
https://learn.chatgpt.com/docs/config-file/config-basic (2026-11-11 열람)
