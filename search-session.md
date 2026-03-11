사용자가 입력한 키워드로 Claude 세션을 검색합니다.

키워드: $ARGUMENTS

## 검색 절차

1. 아래 경로들에서 키워드를 검색합니다:
   - `~/.claude/projects/*/*.jsonl` (프로젝트별 세션)
   - `~/.claude/projects/*/*/*.jsonl` (하위 프로젝트 세션)

```bash
grep -rl "$ARGUMENTS" ~/.claude/projects/*/*.jsonl ~/.claude/projects/*/*/*.jsonl 2>/dev/null | grep -v '/subagents/' | sort -u || true
```

2. 매칭된 각 세션 파일에서 다음 정보를 추출합니다:

```bash
for f in $(grep -rl "$ARGUMENTS" ~/.claude/projects/*/*.jsonl ~/.claude/projects/*/*/*.jsonl 2>/dev/null | grep -v '/subagents/' | sort -u); do
  SESSION_ID=$(basename "$f" .jsonl)
  CWD=$(grep -o '"cwd":"[^"]*"' "$f" | head -1 | sed 's/"cwd":"//;s/"//')
  SLUG=$(grep -o '"slug":"[^"]*"' "$f" | head -1 | sed 's/"slug":"//;s/"//')
  echo "---"
  echo "세션 ID: $SESSION_ID"
  echo "슬러그: $SLUG"
  echo "작업 디렉토리: $CWD"
  echo "resume 명령어: cd $CWD && claude --resume $SESSION_ID --dangerously-skip-permissions"
done
```

3. 검색 결과를 사용자에게 정리해서 보여줍니다. resume 명령어는 세션 파일이 속한 프로젝트 경로가 아닌, 세션 내 `cwd` 값을 기준으로 생성합니다.
