# Processes and Jobs - Overview

**Module:** Linux Luminarium → Processes and Jobs  
**문제 수:** 10개  
**주제:** 프로세스 관리, 잡 제어, 신호

---

## 문제 목록

| # | Challenge | 기술 |
|---|-----------|------|
| 1 | [[01-Listing-Processes]] | `ps` |
| 2 | [[02-Killing-Processes]] | `kill` |
| 3 | [[03-Interrupting-Processes]] | `Ctrl+C`, SIGINT |
| 4 | [[04-Suspending-Processes]] | `Ctrl+Z`, SIGSTOP |
| 5 | [[05-Resuming-Processes]] | `fg`, `bg` |
| 6 | [[06-Backgrounding-Processes]] | `&` |
| 7 | [[07-Foregrounding-Processes]] | `fg %n` |
| 8 | [[08-Starting-Backgrounded-Processes]] | 백그라운드 시작 |
| 9 | [[09-Process-Exit-Codes]] | `$?` |
| 10 | [[10-Signal-Sending]] | `kill -SIGNAL` |

---

## 핵심 개념

```bash
ps aux               # 모든 프로세스
ps -ef               # 상세 프로세스
top / htop           # 실시간 모니터
kill PID             # SIGTERM 전송
kill -9 PID          # SIGKILL
kill -l              # 신호 목록

# 잡 제어
Ctrl+C               # SIGINT (종료)
Ctrl+Z               # SIGSTOP (일시 중지)
Ctrl+\               # SIGQUIT
jobs                 # 잡 목록
fg %1                # 1번 잡 포그라운드
bg %1                # 1번 잡 백그라운드
command &            # 백그라운드 실행
wait                 # 모든 백그라운드 완료 대기
```
