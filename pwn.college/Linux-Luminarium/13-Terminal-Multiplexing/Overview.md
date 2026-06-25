# Terminal Multiplexing - Overview

**Module:** Linux Luminarium → Terminal Multiplexing  
**문제 수:** 6개  
**주제:** tmux, screen - 터미널 세션 관리

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Detach-and-Attach]] | `tmux detach/attach` |
| 2 | [[02-Different-Windows]] | tmux 윈도우 |
| 3 | [[03-Different-Panes]] | tmux 패인 분할 |
| 4 | [[04-Connecting-over-SSH]] | SSH + tmux |
| 5 | [[05-Tmux-Scrollback]] | 스크롤백 |
| 6 | [[06-Screen-vs-Tmux]] | screen 비교 |

---

## tmux 핵심 단축키

```
# 세션 관리
tmux new -s name     # 새 세션
tmux attach -t name  # 세션 연결
tmux ls              # 세션 목록
tmux kill-session -t name

# tmux 내부 (Ctrl+b가 prefix)
Ctrl+b d    # detach (세션 유지하며 나오기)
Ctrl+b c    # 새 윈도우
Ctrl+b n    # 다음 윈도우
Ctrl+b p    # 이전 윈도우
Ctrl+b w    # 윈도우 목록
Ctrl+b %    # 세로 분할 (패인)
Ctrl+b "    # 가로 분할 (패인)
Ctrl+b 방향키  # 패인 이동
Ctrl+b [    # 스크롤백 모드 (q로 종료)
Ctrl+b ?    # 도움말
```
