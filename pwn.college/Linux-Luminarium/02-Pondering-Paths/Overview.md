# Pondering Paths - Overview

**Module:** Linux Luminarium → Pondering Paths  
**문제 수:** 8개  
**주제:** 절대경로, 상대경로, 디렉토리 탐색

---

## 문제 목록

| # | Challenge | 핵심 기술 |
|---|-----------|-----------|
| 1 | [[01-The-Path-to-Success]] | 절대경로로 바이너리 실행 |
| 2 | [[02-Program-and-Absolute-Paths]] | /challenge/ 절대경로 |
| 3 | [[03-Position-thy-Paths]] | 경로 이해 |
| 4 | [[04-Implicit-Relative-Path]] | ./ 상대경로 |
| 5 | [[05-Explicit-Relative-Path]] | cd 후 실행 |
| 6 | [[06-Home-Sweet-Home]] | ~ 홈 디렉토리 |
| 7 | [[07-Changing-Directories]] | cd 명령어 |
| 8 | [[08-A-Puzzling-Path]] | 복합 경로 |

---

## 핵심 개념

```
절대 경로: /로 시작
  /challenge/run
  /home/hacker/file

상대 경로: 현재 위치 기준
  ./run           현재 디렉토리의 run
  ../file         상위 디렉토리의 file
  subdir/file     하위 디렉토리

특수 경로:
  ~               홈 디렉토리 (/home/hacker)
  .               현재 디렉토리
  ..              상위 디렉토리
```
