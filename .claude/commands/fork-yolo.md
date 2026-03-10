현재 대화를 fork하는 CLI 명령어를 생성해주세요.

다음 조건을 포함해야 합니다:
- `claude --dangerously-skip-permissions` (yolo 모드)
- `-p` 옵션으로 현재 작업 디렉토리(cwd)를 전달: `$ARGUMENTS`가 있으면 그 경로를, 없으면 현재 cwd를 사용
- `--resume` 옵션으로 현재 대화를 이어받기

명령어를 출력한 후, 사용자가 복사해서 새 터미널에서 실행할 수 있도록 안내해주세요.
