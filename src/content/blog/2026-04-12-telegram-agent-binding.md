---
title: OpenClaw Agent별 Telegram 연결 방법
date: 2026-04-12
description: 여러 에이전트를 각각 다른 텔레그램 봇에 연결하는 방법(openclaw.json 설정법)
tags:
  - OpenClaw
  - Telegram
  - Agent 연결
  - 설정법
---

# OpenClaw에서 Agent별로 Telegram 연결하기

OpenClaw를 사용하면 여러 에이전트(Agent)를 각기 다른 텔레그램 봇에 연결할 수 있습니다. 실제 예시와 함께 `openclaw.json` 설정 방법을 정리합니다.

## 1. 기본 구조 이해하기
텔레그램 연동을 위해서는 `openclaw.json`의 두 부분을 설정해야 합니다:

- `channels.telegram.accounts`: 연결할 봇(token별)
- `bindings`: accountId/agentId 매핑(어떤 봇이 어떤 에이전트로 동작할지)

---

## 2. 예시 openclaw.json 구조

### (1) channels, bindings
```json
"channels": {
  "telegram": {
    "enabled": true,
    "groups": {
      "*": { "requireMention": true }
    },
    "accounts": {
      "default": { "enabled": true, "botToken": "(토큰)" },
      "unaengbot": { "enabled": true, "botToken": "(토큰)" },
      "werdybot": { "enabled": true, "botToken": "(토큰)" }
    }
  }
},
"bindings": [
  { "type": "route", "agentId": "unaengbot", "match": { "channel": "telegram", "accountId": "unaengbot" } },
  { "type": "route", "agentId": "main", "match": { "channel": "telegram", "accountId": "default" } },
  { "type": "route", "agentId": "werdybot", "match": { "channel": "telegram", "accountId": "werdybot" } }
]
```

### (2) agents 설정
```json
"agents": {
  "defaults": {
    "workspace": "/Users/hye/.openclaw/workspace",
    "models": {
      "github-copilot/gpt-4o": {},
      "github-copilot/gpt-5-mini": {},
      "github-copilot/gpt-4.1": {}
    },
    "model": {
      "primary": "github-copilot/gpt-4.1"
    }
  },
  "list": [
    {
      "id": "main",
      "model": "github-copilot/gpt-4.1"
    },
    {
      "id": "unaengbot",
      "name": "UnaengBot",
      "workspace": "/Volumes/DataEx/openclaw/workspace-UnaengBot",
      "agentDir": "/Users/hyejoon/.openclaw/agents/unaengbot/agent",
      "model": "github-copilot/gpt-4.1"
    },
    {
      "id": "werdybot",
      "name": "WerdyBot",
      "workspace": "/Volumes/DataEx/openclaw/workspace-werdybot",
      "agentDir": "/Users/hyejoon/.openclaw/agents/werdybot/agent",
      "model": "github-copilot/gpt-4.1"
    }
  ]
}
```


---

## 3. Agent 추가 방법

OpenClaw에서 새로운 Agent를 만드는 방법은 매우 간단합니다.

### 3-1. agent 생성 명령 예시
아래와 같은 커맨드로 원하는 agent를 추가할 수 있습니다:

```bash
openclaw agents add UnaengBot --workspace /Volumes/DataEx/openclaw/workspace-UnaengBot --model gpt-4.1 --bind telegram --non-interactive
```
- `UnaengBot`: agent 이름
- `--workspace`: 에이전트의 작업 공간 경로
- `--model`: 기본 모델 지정
- `--bind telegram`: 텔레그램 채널로 연결
- `--non-interactive`: 묻지 않고 진행

**생성 후** openclaw.json의 agents 및 bindings 항목에서 정상적으로 추가됐는지, telegram/botToken 세팅이 맞는지 꼭 확인해 주세요.

### 3-2. 텔레그램 연결 과정 요약
1. **텔레그램 봇 생성**: BotFather로 각 agent에 쓸 봇을 미리 만듭니다.
2. **openclaw.json에 등록**: 계정명(예: werdybot, unaengbot)에 봇 토큰을 입력합니다.
3. **bindings에 매핑**: 봇 계정(accountId)과 agentId를 연결합니다.
    - 예시) `accountId: "werdybot"` → `agentId: "werdybot"`
    - 그룹/채널별 라우팅도 가능

#### 예시 상황 정리
- werdybot → werdybot agent 동작
- unaengbot → unaengbot agent 동작
- default(기본 봇) → main agent 동작

## 4. 실전 적용 체크리스트

- BotFather에서 각 botToken을 정확히 복사해 `openclaw.json`에 입력
- `bindings`에서 원하는 에이전트와 계정이 정확히 연결됐는지 확인
- OpenClaw를 재시작하여 변경 적용

---

## 5. 자주하는 질문(FAQ)

- **Q: 여러 개의 에이전트를 동시에 운영해도 되나요?**
  - 네, 각기 다른 계정/봇에 여러 agent를 매핑할 수 있습니다.
- **Q: 한 텔레그램 채팅방에서 여러 agent를 동작시킬 수 있나요?**
  - 각 에이전트별로 bot 계정이 다르다면 가능합니다. 단, 한 계정에 여러 agent를 매핑하려면 추가 라우팅 설정이 필요합니다.

---

OpenClaw 공식 문서 및 community도 참고하세요. 
- https://docs.openclaw.ai
