# Linux Luminarium - Overview

**Platform:** pwn.college  
**Dojo:** Linux Luminarium  
**총 모듈:** 17개 | **총 문제:** 128개  
**난이도:** Beginner → Intermediate  

---

## 모듈 목록

| # | Module | 문제 수 | 핵심 주제 |
|---|--------|---------|-----------|
| 1 | [[01-Hello-Hackers/Overview]] | 3 | 첫 실행, 절대 경로 |
| 2 | [[02-Pondering-Paths/Overview]] | 8 | 절대/상대 경로 |
| 3 | [[03-Comprehending-Commands/Overview]] | 15 | 기본 명령어 |
| 4 | [[04-Digesting-Documentation/Overview]] | 7 | man, --help |
| 5 | [[05-File-Globbing/Overview]] | 10 | 와일드카드 패턴 |
| 6 | [[06-Practicing-Piping/Overview]] | 15 | 파이프, 리다이렉션 |
| 7 | [[07-Shell-Variables/Overview]] | 8 | 변수, 환경변수 |
| 8 | [[08-Data-Manipulation/Overview]] | 6 | cut, sort, sed, awk |
| 9 | [[09-Processes-and-Jobs/Overview]] | 10 | 프로세스, 잡 제어 |
| 10 | [[10-Untangling-Users/Overview]] | 4 | 사용자, su, sudo |
| 11 | [[11-Perceiving-Permissions/Overview]] | 8 | 권한, SUID, sticky |
| 12 | [[12-Chaining-Commands/Overview]] | 12 | &&, \|\|, 서브쉘 |
| 13 | [[13-Terminal-Multiplexing/Overview]] | 6 | tmux, screen |
| 14 | [[14-Pondering-PATH/Overview]] | 5 | $PATH 조작 |
| 15 | [[15-Silly-Shebanigans/Overview]] | 6 | shebang, 스크립트 |
| 16 | [[16-Daring-Destruction/Overview]] | 5 | 파일 삭제, 보안 |

---

## 학습 순서

```
Hello Hackers → Pondering Paths → Comprehending Commands
→ Digesting Documentation → File Globbing → Practicing Piping
→ Shell Variables → Data Manipulation → Processes and Jobs
→ Untangling Users → Perceiving Permissions → Chaining Commands
→ Terminal Multiplexing → Pondering PATH → Silly Shebanigans
→ Daring Destruction
```

---

## 공통 패턴

모든 Linux Luminarium 문제:
- `/challenge/run` 또는 `/challenge/<name>` 실행
- 특정 방법으로 명령을 실행해야 flag 획득
- 잘못된 방법으로 실행하면 힌트 출력
