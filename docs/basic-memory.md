# 이 저장소의 Basic Memory 활용 가이드

사용자가 제공한 세팅 글을 바탕으로, 이 저장소의 공통 지침 구조와 Windows 환경에 맞게 정리했다. 설치 명령과 도구 정보는 2026-11-20 공식 문서를 확인했다.

## 지금 적용된 것

- `AGENTS.md`와 `CLAUDE.md`가 공통 규칙인 [memory-workflow.md](../.claude/memory-workflow.md)를 참조한다.
- 현재 상태와 인수인계는 저장소의 `memory/`에 Markdown으로 기록한다.
- 기록은 Git 추적에서 제외된다. 여러 로컬 에이전트가 같은 폴더를 읽을 수 있다.
- Basic Memory 설치, MCP 등록, 클라우드 동기화는 아직 수행하지 않았다. 문서만으로 프로그램이나 연결이 생기지는 않는다.

## 사용법

이 저장소를 연 AI에게 다음처럼 요청한다.

- “기억 기록 읽고 지난번 작업 이어서 하자.”
- “오늘 결정한 내용이랑 다음 할 일을 저장해줘.”
- “이 결정이 바뀌었으니 기존 노트를 갱신해줘.”

에이전트는 시작할 때 `memory/index.md`와 관련 기록을 읽고, 의미 있는 작업을 마치면 인수인계를 남긴다. 지침을 읽지 않는 앱이나 파일 접근 권한이 없는 AI에는 자동으로 전달되지 않는다. 필요하면 “이 저장소의 AGENTS.md와 .claude/memory-workflow.md를 먼저 읽어줘”라고 알려준다.

## Basic Memory가 추가하는 기능

로컬 MD 기록은 설치 없이 바로 사용할 수 있다. Basic Memory를 연결하면 같은 폴더를 MCP로 검색하고 읽고 수정할 수 있다. 모든 대화를 자동으로 기억하는 장치는 아니므로 무엇을 남겼는지와 저장 성공 여부를 확인한다.

로컬 기록은 내 컴퓨터에 유지된다. 다만 연결한 AI가 노트를 읽으면 그 내용은 해당 AI의 처리 범위에 들어간다. 로컬 보관과 AI 서비스로의 내용 전달은 구분한다.

## Windows 로컬 설치 — 추후 실행

아래는 실행 예시이며 이번 작업에서는 실행하지 않았다. 공식 설치 안내는 Python 3.12 이상과 `uv`를 요구한다. `uv`가 없다면 [공식 설치 안내](https://docs.astral.sh/uv/getting-started/installation/)를 따른다.

```powershell
uv tool install basic-memory
basic-memory --version
```

그다음 **이 저장소 루트에서** 기존 `memory/`를 프로젝트로 등록한다.

```powershell
$notesPath = (Resolve-Path -LiteralPath '.\memory').Path
basic-memory project add ai-job-search "$notesPath"
basic-memory status --project ai-job-search
```

이미 같은 이름이 있다면 먼저 `basic-memory project list`로 경로를 확인한다. 다른 프로젝트를 덮어쓰거나 제거하지 않는다. 저장소 전체 대신 `memory/`만 등록해서 기억의 범위를 명확히 한다.

### Claude Code 연결 예시

```powershell
claude mcp add basic-memory basic-memory mcp --project ai-job-search
```

Claude Code의 `/mcp`에서 연결을 확인한다. 기존 서버가 있으면 먼저 설정을 확인한다.

### Claude Desktop / 로컬 stdio MCP를 지원하는 앱

다음은 기존 설정에 병합할 예시다. 설정 파일 전체를 교체하지 않는다.

```json
{
  "mcpServers": {
    "basic-memory": {
      "command": "basic-memory",
      "args": ["mcp", "--project", "ai-job-search"]
    }
  }
}
```

Claude Desktop의 Windows 설정 파일은 `%APPDATA%\Claude\claude_desktop_config.json`이다. 앱에서 실행 파일을 못 찾으면 PowerShell의 `Get-Command basic-memory`로 설치 위치를 확인하고 `command`에 전체 경로를 넣는다. 앱을 재시작한 뒤 실제 도구 목록을 확인한다. 다른 앱은 해당 앱의 MCP 설정 형식을 따른다.

### ChatGPT와 클라우드

로컬 폴더에 접근하는 코딩 에이전트와 일반 ChatGPT의 원격 MCP 연결은 별개다. 일반 ChatGPT에서 같은 기록을 연결하려면 지원되는 원격 MCP와 계정 설정이 필요하다. Basic Memory Cloud는 그 선택지 중 하나다. 클라우드에 옮기는 일은 로컬 MD 사용에 필수가 아니며, 이번에는 설정하지 않았다. 요금제와 지원 기능은 [공식 ChatGPT 연동 문서](https://docs.basicmemory.com/integrations/chatgpt)에서 다시 확인한다.

## 확인 방법

1. 로컬 파일 방식: AI가 `memory/index.md`를 읽고 현재 작업과 다음 행동을 설명하는지 확인한다.
2. MCP 연결 후: `ai-job-search` 프로젝트와 도구 목록을 조회하고 연결 폴더를 확인한다.
3. 짧은 시험 노트를 저장하고 `memory/`의 파일을 직접 읽어 내용이 일치하는지 확인한다.
4. 다른 AI에서도 동일한 노트를 찾아 읽는지 확인한다. 연결 성공과 기억 자동 사용은 별도로 검증한다.

노트가 검색되지 않으면 `basic-memory status --project ai-job-search`로 인덱스 상태를 확인한다. 설치나 인증 실패를 성공한 것으로 기록하지 않는다.

## 공식 문서

- [로컬 설치](https://docs.basicmemory.com/start-here/quickstart-local)
- [CLI와 프로젝트 관리](https://docs.basicmemory.com/reference/cli-reference)
- [Claude Code 연결](https://docs.basicmemory.com/integrations/claude-code)
- [MCP 도구 목록](https://docs.basicmemory.com/reference/mcp-tools-reference)

현재 공식 1.0 문서는 `bm_read`, `bm_search`, `bm_write` 등의 도구를 안내한다. 이전 버전 이름을 고정해서 사용하지 말고 연결된 서버의 도구 목록을 따른다.
