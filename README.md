# BJIN_TODO_VER_1

말로 편하게 던진 오늘 할 일이 자동으로 로그·태스크 목록·주간보고·발제문서까지 이어지는 개인 업무 기록 시스템입니다. Claude Code 플러그인으로 동작합니다.

## 이게 뭔가요

매일 "오늘 뭐 했어"를 채팅으로 말하면:
- 날짜별 원본 로그(`logs/WORK-LOG-*.md`)에 그대로 쌓이고
- 진행 중인 일 목록(`TASKS.md` + `tasks/*.md`)이 자동으로 갱신되고
- 주 단위로 팀원들 보고를 모아서 실제 이메일 형식으로 취합하거나(`todo-weekly-report`)
- 회사 공식 양식 발제문서(docx)로 만들어줍니다(`todo-briefing`)

이름·팀원·프로젝트 같은 개인정보는 코드에 없습니다 — 처음 설치하면 `todo-setup` 스킬이 몇 가지를 물어보고, 그 답으로 본인만의 `CLAUDE.md`/`REFERENCE.md`를 만들어 씁니다.

## 설치

Claude Code에서:

```
/plugin marketplace add <본인계정>/BJIN_TODO_VER_1
/plugin install bjin-todo@BJIN_TODO_VER_1
```

또는 클론해서 로컬 스킬로:

```
git clone https://github.com/<본인계정>/BJIN_TODO_VER_1.git
cp -r BJIN_TODO_VER_1/skills/* ~/.claude/skills/
cp -r BJIN_TODO_VER_1/references ~/.claude/  # 또는 프로젝트 폴더에
```

## 시작하기

업무 기록으로 쓸 폴더에서 Claude Code를 켜고:

```
todo 시스템 초기설정 해줘
```

몇 가지 질문(이름/직급/팀, 팀원, 프로젝트, 실제 보냈던 주간보고 이메일 예시 등)에 답하면 끝입니다. 그 다음부터는:

```
9/15 - 고객 미팅 2시간, 버그 3건 수정
```

이렇게만 말하면 알아서 기록합니다.

## 왜 실제 이메일 예시를 달라고 하나요

주간보고 형식은 회사마다 다 다릅니다. 일반적인 "핵심성과/이슈/차주계획" 같은 상상한 템플릿을 만드는 대신, 실제로 보냈던 이메일 1~3통을 보여주면 그 형식을 그대로 학습해서 씁니다 — 진짜 근거가 있는 형식이 훨씬 정확합니다.

## 구조

```
BJIN_TODO_VER_1/
├── .claude-plugin/plugin.json   # 플러그인 매니페스트
├── skills/
│   ├── todo-setup/              # 초기 설정 (개인정보 입력받아 개인화)
│   ├── todo-log/                # 모드 A: 일일 업무 기록 (기본값)
│   ├── todo-weekly-report/      # 모드 B: 팀 주간보고 취합
│   └── todo-briefing/           # 모드 C: 주간회의 발제문서(docx)
├── templates/                   # 초기 설정 시 채워지는 템플릿
└── references/
    ├── natural-writing-style.md   # 기계적 AI 문체 피하는 원칙
    └── docx-editing-guide.md      # 반복 docx 편집 시 표 손상 방지 가이드
```

설정을 마치면 사용자 본인 폴더에 아래가 새로 생깁니다(이 저장소에는 없음 — 전부 개인정보라서):

```
CLAUDE.md / TASKS.md / REFERENCE.md
tasks/*.md
logs/WORK-LOG-*.md
reference/주간보고_실제양식_참고.md
```

## 문체 원칙

이 스킬로 만든 문서는 `references/natural-writing-style.md` 원칙을 따라 기계적인 AI 문체(같은 구분자·같은 문장 공식 반복)를 피하도록 설계돼 있습니다. AI 탐지를 우회하려는 목적이 아니라, 순수하게 자연스러운 업무 문서를 만드는 게 목적입니다.

## 라이선스

MIT
