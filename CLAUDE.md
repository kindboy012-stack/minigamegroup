# CLAUDE.md — 프로젝트 작업 규칙

## GitHub 자동 커밋 규칙

파일을 추가하거나 수정할 때마다 반드시 GitHub 저장소에 자동으로 커밋한다.

- **저장소**: https://github.com/kindboy012-stack/minigamegroup
- **계정**: kindboy012-stack
- **브랜치**: main

### 커밋 방법 (git 미설치 환경)

git이 설치되지 않은 경우 `gh api`로 파일을 커밋한다.

```powershell
# 파일 업로드/업데이트
$bytes = [System.IO.File]::ReadAllBytes("파일경로")
$b64 = [Convert]::ToBase64String($bytes)
$tmp = "$env:TEMP\gh_commit.json"

# 신규 파일
[System.IO.File]::WriteAllText($tmp, '{"message":"커밋메시지","content":"' + $b64 + '"}', [System.Text.UTF8Encoding]::new($false))
gh api "repos/kindboy012-stack/minigamegroup/contents/파일명" --method PUT --input $tmp

# 기존 파일 수정 (SHA 필요)
$sha = (gh api "repos/kindboy012-stack/minigamegroup/contents/파일명" | ConvertFrom-Json).sha
[System.IO.File]::WriteAllText($tmp, '{"message":"커밋메시지","sha":"' + $sha + '","content":"' + $b64 + '"}', [System.Text.UTF8Encoding]::new($false))
gh api "repos/kindboy012-stack/minigamegroup/contents/파일명" --method PUT --input $tmp
```

### 커밋 메시지 규칙
- 신규 파일: `feat: add 파일명`
- 수정: `fix: 변경내용 요약` 또는 `update: 변경내용 요약`
- 삭제: `chore: remove 파일명`

## 프로젝트 구조

| 파일 | 설명 |
|------|------|
| `index.html` | 게임 허브 홈페이지 |
| `minesweeper.html` | 지뢰찾기 |
| `snake.html` | 뱀 게임 |
| `memory.html` | 카드 짝 맞추기 |
| `breakout.html` | 벽돌 깨기 |
| `2048.html` | 2048 |
