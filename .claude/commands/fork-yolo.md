현재 대화를 fork하여 yolo 모드로 재개하는 명령어를 생성해주세요.

## 세션 ID 찾기

1. 이 대화에서만 존재할 고유한 문자열을 하나 선택 (최근 메시지 내용 중 일부)
2. 아래 패턴으로 현재 프로젝트의 대화 파일에서 grep하여 세션 파일을 찾기:
   ```
   grep -l "고유문자열" ~/.claude/projects/*//*.jsonl
   ```
3. 파일명에서 세션 ID 추출 (파일명이 곧 `<session-id>.jsonl`)

## 명령어 생성

찾은 세션 ID로 아래 형식의 명령어를 출력:

```
cd <CWD> && claude --dangerously-skip-permissions -r <SESSION_ID> --fork-session
```

- CWD: `$ARGUMENTS`가 있으면 그 경로, 없으면 현재 작업 디렉토리 사용

## 출력

최종 명령어만 코드블록으로 출력해주세요. 사용자가 새 터미널에서 복사-붙여넣기로 바로 실행할 수 있도록.
