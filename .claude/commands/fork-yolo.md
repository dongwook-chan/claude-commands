아래 스크립트를 실행하세요.

```bash
FILE=$(ls -t ~/.claude/projects/*/*.jsonl | while read f; do grep -q "fork-yolo" "$f" && echo "$f" && break; done)
SESSION_ID=$(basename "$FILE" .jsonl)
kitten @ launch --type=tab --location=after --cwd=$(pwd) claude --dangerously-skip-permissions -r $SESSION_ID --fork-session
```
