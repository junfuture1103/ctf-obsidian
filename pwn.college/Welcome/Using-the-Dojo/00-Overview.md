# Using the Dojo - Overview

**Platform:** pwn.college  
**Module:** Welcome → Using the Dojo  
**Total Challenges:** 10  
**Difficulty:** Beginner  

---

## 모듈 목표

pwn.college 플랫폼 사용법을 익히는 입문 모듈. Linux 환경, SSH 접속, 파일 시스템, 기본 명령어를 다룬다.

---

## 문제 목록

| # | Challenge | 핵심 개념 |
|---|-----------|-----------|
| 1 | [[01-Connecting-over-SSH]] | SSH 접속법 |
| 2 | [[02-Your-First-Flag]] | flag 파일 읽기 |
| 3 | [[03-Challenge-Programs]] | 바이너리 실행 |
| 4 | [[04-The-Flag-File]] | 파일 권한, cat |
| 5 | [[05-Pasting-into-the-Desktop]] | 웹 터미널/Desktop |
| 6 | [[06-Getting-a-Desktop]] | Desktop 환경 |
| 7 | [[07-Setting-Up-VSCode]] | VSCode SSH 연결 |
| 8 | [[08-Using-the-Shell]] | bash 기초 |
| 9 | [[09-Challenge-Files]] | 파일 탐색 |
| 10 | [[10-Talking-to-Programs]] | stdin/파이프 |

---

## 플랫폼 접속 정보

```
SSH: ssh -p 22 hacker@dojo.pwn.college
또는 웹 터미널: https://pwn.college/welcome/ → 우측 상단 "Start"
```

## 공통 지식

- Flag 형식: `pwn.college{...}`
- `/flag` 파일에 flag가 있는 경우가 많음
- `/challenge/` 디렉토리에 챌린지 바이너리가 있음
- 각 문제는 Docker 컨테이너로 격리됨
