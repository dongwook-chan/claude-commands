현재 대화를 fork하여 yolo 모드로 재개하는 명령어를 생성해주세요.

## 세션 ID 찾기

아래 스크립트를 실행하여 현재 세션 ID를 찾기:

```bash
FILE=$(ls -t ~/.claude/projects/*/*.jsonl | while read f; do grep -q "fork-yolo" "$f" && echo "$f" && break; done)
SESSION_ID=$(basename "$FILE" .jsonl)
echo "$SESSION_ID"
```

## 명령어 생성

찾은 세션 ID와 현재 작업 디렉토리(pwd)로 아래 형식의 명령어를 출력:

```
cd <현재_작업_디렉토리> && claude --dangerously-skip-permissions -r <SESSION_ID> --fork-session
```

## 출력

최종 명령어만 코드블록으로 출력해주세요. 사용자가 새 터미널에서 복사-붙여넣기로 바로 실행할 수 있도록.
