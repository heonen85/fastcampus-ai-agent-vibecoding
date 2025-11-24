# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FastCampus AI Agent 바이브코딩 강의 자료 및 실습 코드 저장소입니다. Claude Code, MCP(Model Context Protocol), AI Agent 개발을 다루는 6개 Part로 구성되어 있습니다.

**강의 자료**: https://goobong.gitbook.io/fastcampus

## Repository Structure

```
Part1_AI_에이전트와_Claude_Code_기초/    # Claude Code 설치, 설정, 커스터마이징
Part2_Agent_개념과_아키텍처/            # Agent 개념, LLM API, MCP Client
Part3_바이브코딩으로_Hybrid_Search_RAG/ # PostgreSQL Hybrid Search, Langgraph RAG
Part4_바이브코딩으로_MCP_server_구현/   # MCP Server 개발 (calculate, random, recruit)
Part5_AI_Agent_프로젝트_3개/            # CS Slackbot, Seoul API MCP, Cookiecutter
Part6_바이브코딩과_AI_agent_best_practice/ # Best practices, git worktree
```

## File Structure

```
.
├── .claude/                              # Claude Code 커스터마이징 설정
│   ├── agents/                           # Sub Agent 정의
│   │   ├── code-reviewer.md
│   │   ├── lecture-content-generator.md
│   │   ├── subway-menu-recommender.md
│   │   └── ultimate-planner.md
│   ├── commands/                         # Slash Command 정의
│   │   ├── create-linear-issues.md
│   │   ├── optimize.md
│   │   ├── sync-slack-tasks.md
│   │   └── update-slash-command.md
│   ├── hooks/                            # Hook 스크립트
│   │   └── youtube_transcript.sh
│   └── output-styles/                    # Output Style 정의
│       ├── deep-research.md
│       └── one-word.md
├── Part1_AI_에이전트와_Claude_Code_기초/
│   ├── Chapter1_강의_소개/
│   ├── Chapter2_Claude_Code_설치와_설정/
│   ├── Chapter3_커스터마이징_기초/
│   └── Chapter4_Slack_MCP_서버_실습/
├── Part2_Agent_개념과_아키텍처/
│   ├── Chapter1_Agent_개념_이해하기/
│   ├── Chapter2_LLM_API_호출_이해하기/
│   ├── Chapter3_MCP_Client_사용하기/
│   └── Chapter4_바이브코딩으로_MCP_AI_에이전트_만들기/
│       └── playwright-mcp-client/        # MCP Client 구현 실습
├── Part3_바이브코딩으로_Hybrid_Search_RAG_구현하기/
│   ├── Chapter1~3/                       # 강의 자료
│   └── search_app/                       # 핵심 실습 프로젝트
│       ├── hybrid_search.py              # BM25 + Vector 하이브리드 검색
│       ├── langgraph_rag.py              # Langgraph Workflow RAG
│       ├── load_data.py                  # 데이터 로드 스크립트
│       └── agent_app/                    # Agent RAG (Next.js + FastAPI)
├── Part4_바이브코딩으로_MCP_server_구현하기/
│   ├── Chapter1_MCP_server_이해하기/
│   ├── Chapter2_바이브코딩으로_MCP_server_구현하기/
│   │   ├── calculate-mcp-server/         # 계산기 MCP Server
│   │   └── random-mcp-server/            # 랜덤값 MCP Server
│   └── Chapter3_우리_회사_DB를_쿼리하는_MCP_SERVER_구현하기/
│       └── recruit-mcp-server/           # PostgreSQL 연동 MCP Server
├── Part5_AI_Agent_프로젝트_3개/
│   ├── Chapter1_바이브코딩으로_CS_슬랙봇_구현하기/
│   │   ├── main.py                       # FastAPI 엔트리포인트
│   │   ├── Dockerfile
│   │   └── tests/
│   ├── Chapter2_바이브코딩으로_서울시_문화행사_조회하는_MCP_SERVER_만들기/
│   │   └── src/seoul_culture_mcp/        # FastMCP 서버 구현
│   └── Chapter3_바이브코딩으로_공공_MCP_자동_생성하고_에이전트_연결하기/
│       ├── template/data-seoul-mcp/      # Cookiecutter 템플릿
│       ├── culturalevents-mcp-server/    # 생성된 MCP Server 예시
│       └── womenfamilyfoundation-mcp-server/
├── Part6_바이브코딩과_AI_agent_best_practice/
│   └── data-go-mcp-servers/              # 공공데이터 MCP 서버 모음
│       ├── src/                          # 개별 MCP 서버들
│       └── template/                     # Cookiecutter 템플릿
├── .mcp.json                             # 프로젝트 MCP 서버 설정
├── pyproject.toml                        # 루트 Python 프로젝트 설정
├── wt                                    # Git Worktree 자동화 스크립트
└── CLAUDE.md                             # 이 파일
```

## Development Commands

### Python Projects (uv package manager)

```bash
# 의존성 설치
uv sync

# 개발 의존성 포함 설치
uv sync --all-groups

# 스크립트 실행
uv run python <script.py>

# 패키지 추가
uv add <package-name>
uv add --dev <package-name>

# 테스트
uv run pytest
uv run pytest --cov

# 코드 품질
uv run ruff format .
uv run ruff check --fix .
uv run pyright
```

### Node.js Projects (pnpm preferred)

```bash
pnpm install
pnpm dev
```

### Git Worktree

병렬 작업용 worktree 자동 생성 스크립트:

```bash
./wt <branch-name>
# 예: ./wt feature/new-feature
```

## Key Implementation Projects

### Part3: Hybrid Search RAG (`search_app/`)
- PostgreSQL + pgvector + pg_search 기반 하이브리드 검색
- BM25 키워드 검색 + 벡터 유사도 검색을 RRF로 결합
- Langgraph Workflow RAG (`langgraph_rag.py`)
- Agent RAG with OpenAI Function Calling (`agent_app/`)

### Part5/Chapter1: CS Slackbot
- FastAPI + Claude Agent SDK + Notion MCP
- Google Cloud Run 배포
- Slack Event Subscription 처리

### Part5/Chapter3: Seoul Open Data MCP Generator
- Cookiecutter 템플릿으로 MCP 서버 자동 생성
- FastMCP 프레임워크 사용

## MCP Configuration

루트의 `.mcp.json`에 MCP 서버 설정:
- notion: HTTP 타입 (`https://mcp.notion.com/mcp`)
- slack: npx로 실행
- playwright: stdio 타입
- linear: SSE 타입

## Custom Claude Code Configuration

### Slash Commands (`.claude/commands/`)
- `/update-slash-command`: 기존 슬래시 커맨드 수정 워크플로우

### Sub Agents (`.claude/agents/`)
- `code-reviewer`: 코드 리뷰 전문 에이전트
- `lecture-content-generator`: 한국어 강의 자료 생성 에이전트
- `subway-menu-recommender`: 서브웨이 메뉴 추천 에이전트
- `ultimate-planner`: Linear 이슈 분석 및 계획 에이전트

### Output Styles (`.claude/output-styles/`)
- `deep-research`: 심층 리서치 스타일
- `one-word`: 한 단어 응답 스타일

## Development Guidelines

### TDD (Test-Driven Development)
- 테스트 먼저 작성 후 구현
- 구현 후 반드시 테스트 실행

### Atomic Commits
- 한 번에 하나의 논리적 변경만 커밋
- 관련 파일만 staging
- **`git push` 금지** - 로컬에서만 작업

### Conventional Commits
```
<type>(<scope>): <subject>
# 예: feat(api): add date range filter
# 예: fix(server): handle API timeout
```

## Language & Documentation

- 강의 자료: 한국어
- 코드 및 기술 용어: 영어
- 코드 주석: 한국어 또는 영어 (일관성 유지)

## Environment Variables

각 프로젝트 디렉토리의 `.env` 또는 `.env.local` 파일에 설정:
- `DATABASE_URL`: PostgreSQL 연결 문자열
- `OPENAI_API_KEY`: OpenAI API 키
- `ANTHROPIC_API_KEY`: Claude API 키
- `SLACK_BOT_TOKEN`, `SLACK_SIGNING_SECRET`: Slack 연동
- `NOTION_API_KEY`: Notion MCP 연동
- `TAVILY_API_KEY`: 웹 검색 API (선택)
- `SEOUL_API_KEY`: 서울시 공공데이터 API

## Notes

- Python 3.10+ 필요
- uv 패키지 매니저 사용 (pip 사용 금지)
- Docker 빌드 시 `--platform linux/amd64` 필수 (Cloud Run 배포용)
