사용자가 입력한 키워드로 Claude 세션을 검색합니다.

키워드: $ARGUMENTS

아래 bash를 실행

```bash
for f in $(find ~/.claude/projects -name '*.jsonl' -not -path '*/subagents/*' -exec grep -l "$ARGUMENTS" {} + 2>/dev/null | sort -u); do
  SESSION_ID=$(basename "$f" .jsonl)
  CWD=$(grep -o '"cwd":"[^"]*"' "$f" | head -1 | sed 's/"cwd":"//;s/"//')
  SLUG=$(grep -o '"slug":"[^"]*"' "$f" | head -1 | sed 's/"slug":"//;s/"//')
  echo "세션 ID: $SESSION_ID"
  echo "슬러그: $SLUG"
  echo "작업 디렉토리: $CWD"
  echo "resume: cd $CWD && claude --resume $SESSION_ID --dangerously-skip-permissions"
done
```
